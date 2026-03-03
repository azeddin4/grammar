---
Language: Express
Version: 5.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/express/package.json"
Grammar_Lock: "@root/hashes/grammar/express.hash.md"
---

/** [Project].Grammar.Express - Linguistic DNA anchor for Express 5.x */

## [SDK_Discovery_Map]
/** === @types/express === */
/** @Ref: @root/node_modules/@types/express/index.d.ts */
/** === @types/express-serve-static-core (1252 lines — the real type engine) === */
/** @Ref: @root/node_modules/@types/express-serve-static-core/index.d.ts */

## [SDK_Imports / Namespaces]
```ts
import express from "express"
import type { Application, Request, Response, NextFunction, Router, RequestHandler, ErrorRequestHandler, CookieOptions } from "express"
import type { ParamsDictionary, ParamsFlatDictionary, Params, Query, Send, PathParams, RouteParameters, IRouter, IRoute, IRouterMatcher, IRouterHandler, ILayer, MediaType, ByteRange, RequestHandlerParams, Errback, SendFileOptions, DownloadOptions, Locals, RequestRanges } from "express-serve-static-core"
```

## [Core_Primitives]
```ts
// Application (express-serve-static-core index.d.ts L900+)
const app: Application = express()

// Request<P, ResBody, ReqBody, ReqQuery, Locals> (index.d.ts L402-669)
interface Request<P = ParamsDictionary, ResBody = any, ReqBody = any, ReqQuery = ParsedQs, LocalsObj extends Record<string, any> = Record<string, any>> extends http.IncomingMessage {
  // Route parameters
  params: P
  query: ReqQuery
  body: ReqBody

  // Request info
  readonly protocol: string
  readonly secure: boolean
  readonly ip: string | undefined
  readonly ips: string[]
  readonly hostname: string
  readonly host: string
  readonly path: string
  readonly subdomains: string[]
  readonly fresh: boolean
  readonly stale: boolean
  readonly xhr: boolean
  method: string
  originalUrl: string
  url: string
  baseUrl: string

  // Headers
  get(name: "set-cookie"): string[] | undefined
  get(name: string): string | undefined
  header(name: string): string | undefined

  // Content negotiation
  accepts(): string[]
  accepts(type: string): string | false
  acceptsCharsets(...charset: string[]): string | false
  acceptsEncodings(...encoding: string[]): string | false
  acceptsLanguages(...lang: string[]): string | false
  is(type: string | string[]): string | false | null

  // Range parsing
  range(size: number, options?: RangeParserOptions): RangeParserRanges | RangeParserResult | undefined

  // Cookies & misc
  cookies: any
  signedCookies: any
  app: Application
  route: any
  res?: Response
  next?: NextFunction
}

// Response<ResBody, Locals, StatusCode> (index.d.ts L690-1050)
interface Response<ResBody = any, LocalsObj extends Record<string, any> = Record<string, any>, StatusCode extends number = number> extends http.ServerResponse {
  status(code: StatusCode): this
  sendStatus(code: StatusCode): this
  send: Send<ResBody, this>
  json: Send<ResBody, this>
  jsonp: Send<ResBody, this>
  links(links: any): this
  redirect(url: string): void
  redirect(status: number, url: string): void
  render(view: string, locals?: Record<string, any>, callback?: (err: Error, html: string) => void): void
  cookie(name: string, val: string | any, options?: CookieOptions): this
  clearCookie(name: string, options?: CookieOptions): this
  set(field: string, value?: string | string[]): this
  header(field: string, value?: string | string[]): this
  get(field: string): string | undefined
  type(type: string): this
  contentType(type: string): this
  format(obj: Record<string, () => void>): this
  attachment(filename?: string): this
  append(field: string, value?: string | string[]): this
  vary(field: string): this
  location(url: string): this
  sendFile(path: string, options?: SendFileOptions, fn?: Errback): void
  download(path: string, filename?: string, options?: DownloadOptions, fn?: Errback): void
  locals: LocalsObj
  charset: string
  app: Application
  statusCode: number
}

// NextFunction (index.d.ts L26-38)
interface NextFunction {
  (err?: any): void
  (deferToNext: "router"): void   // break out of router
  (deferToNext: "route"): void    // skip to next route
}

// RequestHandler (index.d.ts L55-68)
interface RequestHandler<P = ParamsDictionary, ResBody = any, ReqBody = any, ReqQuery = ParsedQs, LocalsObj extends Record<string, any> = Record<string, any>> {
  (req: Request<P, ResBody, ReqBody, ReqQuery, LocalsObj>, res: Response<ResBody, LocalsObj>, next: NextFunction): unknown
}

// ErrorRequestHandler (index.d.ts L70-81)
type ErrorRequestHandler<P = ParamsDictionary, ResBody = any, ReqBody = any, ReqQuery = ParsedQs, LocalsObj extends Record<string, any> = Record<string, any>> =
  (err: any, req: Request<P, ResBody, ReqBody, ReqQuery, LocalsObj>, res: Response<ResBody, LocalsObj>, next: NextFunction) => unknown

// CookieOptions (index.d.ts L351-380)
interface CookieOptions {
  maxAge?: number; signed?: boolean; expires?: Date; httpOnly?: boolean
  path?: string; domain?: string; secure?: boolean
  sameSite?: boolean | "lax" | "strict" | "none"
  priority?: "low" | "medium" | "high"
  partitioned?: boolean
  encode?: (val: string) => string
}

// Route parameter extraction (template literal types, index.d.ts L96-122)
type RouteParameters<Route extends string | RegExp>  // Extracts :params from route strings
// e.g., RouteParameters<"/user/:id/posts/:postId"> = { id: string; postId: string }
// Wildcard: RouteParameters<"/files/*filepath"> = { filepath: string[] }
// Optional group: RouteParameters<"/user/:id{/post/:postId}"> = { id: string } & Partial<{ postId: string }>

// PathParams (index.d.ts L83)
type PathParams = string | RegExp | Array<string | RegExp>

// RequestHandlerParams — union of handler types for middleware chaining
type RequestHandlerParams<P, ResBody, ReqBody, ReqQuery, LocalsObj> =
  | RequestHandler<P, ResBody, ReqBody, ReqQuery, LocalsObj>
  | ErrorRequestHandler<P, ResBody, ReqBody, ReqQuery, LocalsObj>
  | Array<RequestHandler<P> | ErrorRequestHandler<P>>

// Module augmentation — extend Express interfaces globally
declare global {
  namespace Express {
    interface Request {}     // extend req
    interface Response {}    // extend res
    interface Locals {}      // extend res.locals
    interface Application {} // extend app
  }
}
interface Locals extends Express.Locals {}  // merged with res.locals

// Send type alias (index.d.ts L678)
type Send<ResBody = any, T = Response<ResBody>> = (body?: ResBody) => T

// MediaType (index.d.ts L671-676)
interface MediaType { value: string; quality: number; type: string; subtype: string }

// ByteRange (index.d.ts L382-385)
interface ByteRange { start: number; end: number }

// SendFileOptions / DownloadOptions (index.d.ts L680-688)
interface SendFileOptions extends SendOptions { headers?: Record<string, unknown> }
interface DownloadOptions extends SendOptions { headers?: Record<string, unknown> }
```

## [Architectural_Laws]
- **Export_Law**: Export router factories. Export typed middleware. Export error handler as last `app.use()`.
- **Transformation_Law**: Middleware chain: `app.use()` → `router.METHOD()` → handler. Request flows through middleware stack in order. Each middleware calls `next()` to pass control. Error middleware has 4 params: `(err, req, res, next)`.
- **Propagation_Law**: Errors thrown/passed via `next(err)` skip to error middleware. Use `express.json()`, `express.urlencoded()`, `express.static()` built-in middleware. Express 5 returns Promises from handlers (no need for `asyncHandler` wrapper).

## [Syntax_Rules] | [Naming_Conventions]
- camelCase: middleware functions, route handlers
- kebab-case: URL paths (`/api/user-profiles`)
- `:param`: route parameters (`/users/:id`)
- `*name`: wildcard parameters (`/files/*filepath`) — Express 5 named wildcards

## [Prohibited_Patterns]
- NO untyped `req.body` — type via `Request<P, ResBody, ReqBody, ReqQuery>`
- NO error swallowing — always call `next(err)` or send response
- NO `res.send()` after `res.end()` — check `res.headersSent`
- NO synchronous blocking in middleware — use async/await (Express 5)
- NO `app.listen()` in module — export app, call listen in entry point

## [Deprecated_Definitions]
```ts
// Express 5 changes from Express 4:
// @deprecated req.host — use req.hostname (host without port)
// @deprecated app.del() — use app.delete()
// @deprecated res.json(status, body) — use res.status(status).json(body)
// @deprecated res.send(status, body) — use res.status(status).send(body)
// @deprecated req.param(name) — use req.params, req.query, or req.body directly
// @deprecated string-based regexp in routes — use RegExp objects
```

## [Standard_Library_Signatures]
```ts
// Router (IRouter — index.d.ts L230-302)
const router: Router = express.Router({ mergeParams?: boolean, caseSensitive?: boolean, strict?: boolean })

// IRouterMatcher (index.d.ts L125-178) — typed path parameters
router.get<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.post<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.put<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.delete<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.patch<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.options<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.head<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.all<Route extends string>(path: Route, ...handlers: RequestHandler<RouteParameters<Route>>[]): this
router.use(...handlers: RequestHandler[]): this
router.use(path: PathParams, ...handlers: RequestHandler[]): this
router.param(name: string, handler: RequestParamHandler): this
router.route<T extends string>(prefix: T): IRoute<T>

// ILayer (index.d.ts L304-313)
interface ILayer { route?: IRoute; name: string; params?: Record<string, any>; keys: string[]; path?: string; method: string; regexp: RegExp; handle: RequestHandler }
router.stack: ILayer[]

// Built-in middleware
express.json(options?: { limit?, type?, strict?, reviver?, inflate? }): RequestHandler
express.urlencoded(options?: { extended?, limit?, type?, parameterLimit? }): RequestHandler
express.static(root: string, options?: { dotfiles?, etag?, extensions?, fallthrough?, index?, lastModified?, maxAge?, redirect?, setHeaders? }): RequestHandler
express.raw(options?): RequestHandler
express.text(options?): RequestHandler

// Application settings
app.set("trust proxy", true | string | number)
app.set("view engine", "ejs" | "pug" | "handlebars")
app.set("views", "./views")
app.set("env", "production" | "development")
app.set("etag", boolean | "weak" | "strong" | Function)
app.set("query parser", "simple" | "extended" | Function)
app.set("subdomain offset", number)  // default: 2
app.set("case sensitive routing", boolean)
app.set("strict routing", boolean)
app.set("json escape", boolean)
app.set("json replacer", Function)
app.set("json spaces", number)
app.get("setting"): any  // retrieves setting value
app.enable("setting"): Application
app.disable("setting"): Application
app.enabled("setting"): boolean
app.disabled("setting"): boolean
app.locals: Record<string, any>  // app-level locals, persist for app lifetime

// Application lifecycle
app.listen(port: number, callback?: () => void): http.Server
app.listen(port: number, host: string, callback?: () => void): http.Server
app.mountpath: string | string[]  // sub-app mount path(s)
app.on("mount", (parent: Application) => void)  // emitted when sub-app mounted
app.path(): string  // canonical path of app

// Extended HTTP methods on IRouter (index.d.ts L272-292)
router.checkout   router.copy   router.lock   router.merge   router.mkactivity
router.mkcol   router.move   router["m-search"]   router.notify   router.propfind
router.proppatch   router.purge   router.report   router.search   router.subscribe
router.trace   router.unlock   router.unsubscribe   router.link   router.unlink
```

## [Tactical_Patterns]
```ts
// Type-safe route params via template literal inference
app.get('/users/:userId/posts/:postId', (req, res) => {
  req.params.userId   // string — auto-inferred from route
  req.params.postId   // string
})

// Typed request body with generics
app.post<{ id: string }, { success: boolean }, { name: string }>('/users/:id',
  express.json(),
  (req, res) => {
    req.body.name    // string
    req.params.id    // string
    res.json({ success: true })  // { success: boolean }
  }
)

// Module augmentation for custom properties
declare global { namespace Express { interface Request { user?: User } } }
app.use((req, res, next) => { req.user = authenticateUser(req); next() })

// Error middleware (must have 4 params)
app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
  res.status(500).json({ error: err.message })
})

// Route chaining
app.route('/users/:id')
  .get((req, res) => res.json(getUser(req.params.id)))
  .put((req, res) => res.json(updateUser(req.params.id, req.body)))
  .delete((req, res) => res.sendStatus(204))

// Content negotiation via format()
res.format({
  'text/plain': () => res.send('hello'),
  'text/html': () => res.send('<b>hello</b>'),
  'application/json': () => res.json({ message: 'hello' }),
  default: () => res.status(406).send('Not Acceptable')
})

// Stack introspection
router.stack.forEach((layer: ILayer) => {
  console.log(layer.name, layer.path, layer.method, layer.regexp)
})
```
