---
Language: Hono
Version: 4.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/hono/package.json"
Grammar_Lock: "@root/hashes/grammar/hono.hash.md"
---

/** [Project].Grammar.Hono - Linguistic DNA anchor for Hono 4.x */

## [SDK_Discovery_Map]
/** === Core Types (9 definition files) === */
/** @Ref: @root/node_modules/hono/dist/types/index.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/hono.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/hono-base.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/context.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/request.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/compose.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/http-exception.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/router.d.ts */
/** @Ref: @root/node_modules/hono/dist/types/types.d.ts */

## [SDK_Imports / Namespaces]
```ts
import { Hono } from "hono"
import type { Context, Next, MiddlewareHandler, Handler, Env, Schema, TypedResponse, HonoRequest, Input, BlankEnv, BlankSchema, BlankInput, RouterRoute, HandlerResponse, Endpoint, KnownResponseFormat, ResponseFormat, FetchEventLike } from "hono"
import type { StatusCode, ContentfulStatusCode, RedirectStatusCode } from "hono/utils/http-status"
import type { BodyData, ParseBodyOptions } from "hono/utils/body"
import type { ValidationTargets } from "hono"
import { HTTPException } from "hono/http-exception"

// Middleware
import { cors } from "hono/cors"
import { logger } from "hono/logger"
import { prettyJSON } from "hono/pretty-json"
import { secureHeaders } from "hono/secure-headers"
import { basicAuth } from "hono/basic-auth"
import { bearerAuth } from "hono/bearer-auth"
import { jwt, sign, verify } from "hono/jwt"
import { compress } from "hono/compress"
import { cache } from "hono/cache"
import { etag } from "hono/etag"
import { timing } from "hono/timing"
import { bodyLimit } from "hono/body-limit"
import { csrf } from "hono/csrf"
import { ipRestriction } from "hono/ip-restriction"

// Validators
import { validator } from "hono/validator"
import { zValidator } from "@hono/zod-validator"

// RPC client
import { hc } from "hono/client"
import type { InferRequestType, InferResponseType } from "hono/client"

// Helpers
import { html, raw } from "hono/html"
import { stream, streamSSE, streamText } from "hono/streaming"
import { createFactory, createMiddleware } from "hono/factory"
import { setCookie, getCookie, deleteCookie } from "hono/cookie"
import { cloneRawRequest } from "hono/request"  // clone consumed request

// Adapters
import { serve } from "@hono/node-server"
import { handle } from "hono/vercel"
import { handle } from "hono/aws-lambda"
import { fire } from "hono/service-worker"         // Service Worker API (non-ES module)
```

## [Core_Primitives]
```ts
// App creation (hono.d.ts, hono-base.d.ts)
const app = new Hono<{ Bindings: Env; Variables: Vars }>({
  strict?: boolean,          // distinguish trailing slash (default: true)
  router?: Router,           // RegExpRouter, TrieRouter, SmartRouter, LinearRouter, PatternRouter
  getPath?: (req, options?) => string,  // custom path resolution (e.g., host-based routing)
})

// Env type (generic type parameter)
type Env = {
  Bindings?: object   // platform bindings (CF Workers KV, D1, R2, etc.)
  Variables?: object  // per-request variables via c.set/c.get
}
// e.g., type AppEnv = { Bindings: { DATABASE_URL: string }; Variables: { user: User } }

// ContextVariableMap — module augmentation for global variables
declare module 'hono' {
  interface ContextVariableMap { logger: Logger; requestId: string }  // accessible via c.get() / c.var globally
}

// Context (context.d.ts — the heart of Hono, 456 lines)
interface Context<E extends Env = any, P extends string = any, I extends Input = {}> {
  // Request
  req: HonoRequest<P, I["out"]>
  
  // Response builders — all return TypedResponse<T, U, format> for RPC inference
  json<T, U extends ContentfulStatusCode>(data: T, status?: U, headers?: HeaderRecord): Response & TypedResponse<JSONParsed<T>, U, 'json'>
  text<T extends string, U extends ContentfulStatusCode>(text: T, status?: U, headers?: HeaderRecord): Response & TypedResponse<T, U, 'text'>
  html<T extends string | Promise<string>>(html: T, status?: ContentfulStatusCode, headers?: HeaderRecord): T extends string ? Response : Promise<Response>
  body<T extends Data, U extends ContentfulStatusCode>(data: T, status?: U, headers?: HeaderRecord): Response & TypedResponse<T, U, 'body'>
  redirect<T extends RedirectStatusCode = 302>(location: string | URL, status?: T): Response & TypedResponse<undefined, T, 'redirect'>
  notFound(): ReturnType<NotFoundHandler>
  newResponse(data: Data | null, status?: StatusCode, headers?: HeaderRecord): Response
  status(code: StatusCode): void
  
  // Headers
  header(name: 'Content-Type', value?: BaseMime, options?: { append?: boolean }): void
  header(name: ResponseHeader, value?: string, options?: { append?: boolean }): void
  header(name: string, value?: string, options?: { append?: boolean }): void
  
  // Variables (type-safe per-request storage)
  set<Key extends keyof E["Variables"]>(key: Key, value: E["Variables"][Key]): void
  get<Key extends keyof E["Variables"]>(key: Key): E["Variables"][Key]
  var: Readonly<ContextVariableMap & E['Variables']>  // shorthand readonly access
  
  // Layout & Rendering
  render: Renderer                           // returns Response via layout
  setRenderer(renderer: Renderer): void      // set custom renderer in middleware
  setLayout(layout: Layout): Layout          // set layout function
  getLayout(): Layout | undefined            // get current layout
  
  // Platform
  env: E["Bindings"]
  executionCtx: ExecutionContext             // CF Workers/Deno Deploy
  event: FetchEventLike                      // Service Worker-style FetchEvent
  
  // Error
  error?: Error
  
  // Finalized response
  finalized: boolean
  res: Response
}

// ExecutionContext (context.d.ts)
interface ExecutionContext {
  waitUntil(promise: Promise<unknown>): void       // extend lifetime beyond response
  passThroughOnException(): void                   // pass to origin on error
  props: any                                        // Wrangler 4.x compat
}

// Data type — valid response body types
type Data = string | ArrayBuffer | ReadableStream | Uint8Array<ArrayBuffer>

// StatusCode types (hono/utils/http-status)
type StatusCode = ContentfulStatusCode | RedirectStatusCode | 100 | 101 | ...
type ContentfulStatusCode = 200 | 201 | 202 | ... | 400 | 401 | 403 | 404 | 500 | ...  // non-redirect HTTP codes
type RedirectStatusCode = 301 | 302 | 303 | 307 | 308

// TypedResponse — phantom type for RPC type inference
type TypedResponse<T = unknown, U extends StatusCode = StatusCode, F extends ResponseFormat = ResponseFormat> = { _data: T; _status: U; _format: F }
type KnownResponseFormat = 'json' | 'text' | 'redirect'
type ResponseFormat = KnownResponseFormat | string

// HonoRequest (request.d.ts — 314 lines)
interface HonoRequest<P extends string = "/", I extends Input['out'] = {}> {
  url: string
  method: string
  path: string
  raw: Request  // Web Standard Request
  routeIndex: number
  bodyCache: Partial<{ json: any; text: string; arrayBuffer: ArrayBuffer; blob: Blob; formData: FormData; parsedBody: BodyData }>
  
  param<P2 extends ParamKeys<P>>(key: P2): string          // required param
  param<P2 extends RemoveQuestion<ParamKeys<P>>>(key: P2): string | undefined  // optional param (:name?)
  param(): Record<string, string>                           // all params
  query(key: string): string | undefined
  query(): Record<string, string>
  queries(key: string): string[] | undefined        // multi-value: ?tags=A&tags=B
  queries(): Record<string, string[]>
  header(name: RequestHeader): string | undefined   // typed request headers
  header(name: string): string | undefined
  header(): Record<RequestHeader | string, string>  // all headers
  
  parseBody<Options extends Partial<ParseBodyOptions>, T extends BodyData<Options>>(options?: Options): Promise<T>
  json<T = any>(): Promise<T>
  text(): Promise<string>
  arrayBuffer(): Promise<ArrayBuffer>
  blob(): Promise<Blob>
  formData(): Promise<FormData>
  
  valid<T extends keyof I & keyof ValidationTargets>(target: T): InputToDataByTarget<I, T>
  addValidatedData(target: keyof ValidationTargets, data: {}): void  // used by validators
  
  matchedRoutes: RouterRoute[]  // @deprecated — use matchedRoutes helper from 'hono/route'
  routePath: string             // @deprecated — use routePath helper from 'hono/route'
}

// cloneRawRequest (request.d.ts) — clone even after body consumed
cloneRawRequest(req: HonoRequest): Promise<Request>  // handles consumed body via cache

// ValidationTargets (types.d.ts) — all supported validation targets
interface ValidationTargets<T extends FormValue = ParsedFormValue, P extends string = string> {
  json: any
  form: Record<string, T | T[]>
  query: Record<string, string | string[]>
  param: Record<P, P extends `${string}?` ? string | undefined : string>
  header: Record<RequestHeader | string, string>
  cookie: Record<string, string>
}

// Schema type system (types.d.ts) — powers RPC inference
type Schema = { [Path: string]: { [Method: `$${Lowercase<string>}`]: Endpoint } }
type Endpoint = { input: any; output: any; outputFormat: ResponseFormat; status: StatusCode }
type ToSchema<M, P, I, RorO>  // maps handler response to schema entry
type MergeSchemaPath<OrigSchema, SubPath>  // merges route() sub-schemas into parent
type ExtractSchema<T>         // extract schema from HonoBase instance

// Input type (types.d.ts)
type Input = { in?: {}; out?: {}; outputFormat?: ResponseFormat }

// Handler types (types.d.ts)
type Handler<E, P, I, R> = (c: Context<E, P, I>, next: Next) => R
type MiddlewareHandler<E, P, I, R> = (c: Context<E, P, I>, next: Next) => Promise<R | void>
type H = Handler | MiddlewareHandler  // union type for route registration
type Next = () => Promise<void>
type HandlerResponse<O> = Response | TypedResponse<O> | Promise<Response | TypedResponse<O>> | Promise<void>

// Error types (types.d.ts)
type ErrorHandler<E> = (err: Error | HTTPResponseError, c: Context<E>) => Response | Promise<Response>
type NotFoundHandler<E> = (c: Context<E>) => NotFoundResponse | Promise<NotFoundResponse>
interface HTTPResponseError extends Error { getResponse: () => Response }
// Module augmentation for custom NotFoundResponse:
// declare module 'hono' { interface NotFoundResponse extends Response, TypedResponse<string, 404, 'text'> {} }

// HTTPException (http-exception.d.ts)
class HTTPException extends Error {
  readonly status: ContentfulStatusCode  // not just StatusCode — no redirects
  readonly res?: Response
  getResponse(): Response
  constructor(status?: ContentfulStatusCode, options?: { message?: string; res?: Response; cause?: unknown })
}
```

## [Architectural_Laws]
- **Export_Law**: Export app instance and typed routes for RPC client. Use `export type AppType = typeof app` for hc() client inference. Export middleware via `createMiddleware<E>()` factory.
- **Transformation_Law**: Web Standard API based — Request/Response everywhere. Works on every runtime: Cloudflare Workers, Deno, Bun, Node.js, AWS Lambda, Vercel Edge. Middleware composition via `app.use()`. Type-safe RPC via `hc<AppType>()`. TypedResponse phantom types drive compile-time inference.
- **Propagation_Law**: Throw `HTTPException` for HTTP errors. Use `.onError()` for global error handling. Use `.notFound()` for 404 handler. Errors in middleware propagate to error handler.
- **Schema_Law**: Route handlers produce `TypedResponse<T, StatusCode, Format>`. The type system auto-merges schemas via `ToSchema` and `MergeSchemaPath`. RPC client `hc<AppType>()` infers from merged schema.
- **Variable_Law**: `c.set()/c.get()` are type-safe via Env['Variables']. Use `ContextVariableMap` module augmentation for global variables accessible in all handlers.

## [Syntax_Rules] | [Naming_Conventions]
- camelCase: routes, middleware, handlers
- kebab-case: URL paths
- PascalCase: types, Hono app
- `:param`: required path parameter (`:id`)
- `:param?`: optional path parameter — returns `string | undefined`
- `:param{regex}`: regex-constrained path parameter
- `*`: wildcard syntax
- `$method`: Schema key convention (e.g., `$get`, `$post`) — always `$` + lowercase method

## [Prohibited_Patterns]
- NO Node.js-specific APIs in edge-targeted code — Hono is Web Standard
- NO `c.json()` without `return` — response must be returned
- NO mutation of `c.res` after `c.json()`/`c.text()` — already finalized
- NO untyped `c.req.body` — use `c.req.json<T>()` or validators
- NO `c.req.matchedRoutes` — deprecated, use `matchedRoutes` from 'hono/route'
- NO `app.fire()` — deprecated, use `fire` from 'hono/service-worker'
- NO returning `void` from final handler — must return Response

## [Standard_Library_Signatures]
```ts
// Route registration — supports up to 10 chained middleware with full type-safety
app.get(path: string, ...handlers: H[]): Hono   // H = Handler | MiddlewareHandler
app.post(path: string, ...handlers: H[]): Hono
app.put(path: string, ...handlers: H[]): Hono
app.delete(path: string, ...handlers: H[]): Hono
app.patch(path: string, ...handlers: H[]): Hono
app.options(path: string, ...handlers: H[]): Hono
app.all(path: string, ...handlers: H[]): Hono
app.on(method: string | string[], path: string | string[], ...handlers: H[]): Hono  // custom methods

// Middleware — up to 10 chained middleware handlers per path
app.use(path?: string, ...middleware: MiddlewareHandler[]): Hono

// Grouping / Mounting
app.route(path: string, subApp: Hono): Hono          // merge sub-app schema at path
app.basePath(path: string): Hono                     // prefix all routes
app.mount(path: string, handler: (req: Request, ...args: any) => Response | Promise<Response>, options?: MountOptions): Hono  // mount external framework handler

// MountOptions
type MountOptions = MountOptionHandler | { optionHandler?: (c: Context) => unknown; replaceRequest?: ((req: Request) => Request) | false }

// App methods
app.fetch(request: Request, env?: Bindings, executionCtx?: ExecutionContext): Response | Promise<Response>  // entry point
app.request(input: Request | string | URL, init?: RequestInit, env?: Bindings): Response | Promise<Response>  // testing helper

// Error handling
app.onError((err: Error | HTTPResponseError, c: Context) => Response | Promise<Response>): Hono
app.notFound((c: Context) => Response | Promise<Response>): Hono

// Zod validation (via @hono/zod-validator) — validates 6 targets
app.post("/", zValidator("json", z.object({ name: z.string() })), (c) => {
  const { name } = c.req.valid("json")  // fully typed via ValidationTargets
  return c.json({ name })
})
// Validation targets: 'json' | 'form' | 'query' | 'param' | 'header' | 'cookie'

// RPC client (hono/client)
const client = hc<AppType>("http://localhost:8787")
const res = await client.api.users.$get()          // typed request
const data = await res.json()                       // typed response
type ReqType = InferRequestType<typeof client.api.users.$post>
type ResType = InferResponseType<typeof client.api.users.$post>
type ResType200 = InferResponseType<typeof client.api.users.$post, 200>  // status-specific

// Streaming (hono/streaming)
app.get("/stream", (c) => stream(c, async (stream) => {
  await stream.write("chunk 1")
  await stream.write("chunk 2")
  stream.onAbort(() => { /* cleanup */ })
}))
app.get("/sse", (c) => streamSSE(c, async (stream) => {
  await stream.writeSSE({ data: JSON.stringify({ msg: "hello" }), event: "update", id: "1" })
}))
app.get("/text-stream", (c) => streamText(c, async (stream) => {
  await stream.write("token 1")
  await stream.sleep(100)
  await stream.write("token 2")
}))

// Cookies (hono/cookie)
setCookie(c, "name", "value", { path: "/", httpOnly: true, maxAge: 3600, sameSite: "Strict", secure: true })
getCookie(c, "name"): string | undefined
getCookie(c): Record<string, string>     // all cookies
deleteCookie(c, "name", opts?)

// Fetch handler (for platforms)
export default app                         // Cloudflare Workers / Bun / Deno
export default { port: 3000, fetch: app.fetch } // Bun
```

## [Tactical_Patterns]
```ts
// Custom middleware with typed variables
const authMiddleware = createMiddleware<{ Variables: { user: User } }>(async (c, next) => {
  const token = c.req.header('Authorization')?.replace('Bearer ', '')
  if (!token) throw new HTTPException(401, { message: 'Unauthorized' })
  c.set('user', await verifyToken(token))
  await next()
})

// Custom renderer (Layout pattern)
app.use('*', async (c, next) => {
  c.setRenderer((content, props) => c.html(`<html><body>${content}</body></html>`))
  await next()
})
app.get('/', (c) => c.render('Hello!'))  // rendered inside layout

// Module augmentation for global ContextVariableMap
declare module 'hono' { interface ContextVariableMap { db: Database } }
app.use('*', async (c, next) => { c.set('db', new Database()); await next() })
app.get('/', (c) => c.var.db.query('...'))  // typed access

// Mounting external frameworks
app.mount('/express', expressApp)  // mount Express/itty-router/etc at path
app.mount('/app', otherApp, { replaceRequest: (req) => req })  // pass-through request

// Host-based routing
const app = new Hono({ getPath: (req) => '/' + req.headers.get('host') + new URL(req.url).pathname })
app.get('/www1.example.com/hello', (c) => c.text('hello www1'))

// waitUntil for background work
app.get('/log', async (c) => {
  c.executionCtx.waitUntil(analytics.track('pageview'))  // doesn't block response
  return c.text('Done')
})

// Clone consumed request for forwarding
app.post('/forward', validator('json', (d) => d), async (c) => {
  c.req.valid('json')  // body consumed
  const cloned = await cloneRawRequest(c.req)  // still works
  return fetch('http://backend', cloned)
})

// Extract schema for testing
type AppSchema = ExtractSchema<typeof app>
type AppSchemaFor200 = ExtractSchemaForStatusCode<typeof app, 200>
```
