---
Language: Fastify
Version: 5.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/fastify/package.json"
Grammar_Lock: "@root/hashes/grammar/fastify.hash.md"
---

/** [Project].Grammar.Fastify - Linguistic DNA anchor for Fastify 5.x */

## [SDK_Discovery_Map]
/** === Core (16 definition files) === */
/** @Ref: @root/node_modules/fastify/fastify.d.ts */
/** @Ref: @root/node_modules/fastify/types/instance.d.ts */
/** @Ref: @root/node_modules/fastify/types/request.d.ts */
/** @Ref: @root/node_modules/fastify/types/reply.d.ts */
/** @Ref: @root/node_modules/fastify/types/route.d.ts */
/** @Ref: @root/node_modules/fastify/types/hooks.d.ts */
/** @Ref: @root/node_modules/fastify/types/plugin.d.ts */
/** @Ref: @root/node_modules/fastify/types/register.d.ts */
/** @Ref: @root/node_modules/fastify/types/schema.d.ts */
/** @Ref: @root/node_modules/fastify/types/type-provider.d.ts */
/** @Ref: @root/node_modules/fastify/types/content-type-parser.d.ts */
/** @Ref: @root/node_modules/fastify/types/errors.d.ts */
/** @Ref: @root/node_modules/fastify/types/logger.d.ts */
/** @Ref: @root/node_modules/fastify/types/context.d.ts */
/** @Ref: @root/node_modules/fastify/types/server-factory.d.ts */
/** @Ref: @root/node_modules/fastify/types/utils.d.ts */

## [SDK_Imports / Namespaces]
```ts
import Fastify from "fastify"
import type { FastifyInstance, FastifyRequest, FastifyReply, FastifySchema, FastifyPluginAsync, FastifyPluginCallback, FastifyPluginOptions, FastifyError, FastifyListenOptions, FastifyRegisterOptions, FastifyTypeProvider, FastifyTypeProviderDefault, FastifyBaseLogger, RouteShorthandOptions, RouteHandlerMethod, RouteGenericInterface, FastifyServerOptions, FastifyHttp2Options, FastifyHttp2SecureOptions, FastifyLoggerOptions, RegisterOptions, RawServerDefault, RawRequestDefaultExpression, RawReplyDefaultExpression, preHandlerHookHandler, preValidationHookHandler, preSendHookHandler, onRequestHookHandler, onResponseHookHandler, onErrorHookHandler, preParsingHookHandler, onTimeoutHookHandler, preSerializationHookHandler, onSendHookHandler, onReadyHookHandler, onListenHookHandler, onCloseHookHandler } from "fastify"
```

## [Core_Primitives]
```ts
// Server creation (fastify.d.ts)
const app = Fastify({
  logger?: boolean | FastifyLoggerOptions,
  disableRequestLogging?: boolean,
  caseSensitive?: boolean,
  ignoreTrailingSlash?: boolean,
  ignoreDuplicateSlashes?: boolean,
  maxParamLength?: number,
  bodyLimit?: number,
  connectionTimeout?: number,
  keepAliveTimeout?: number,
  pluginTimeout?: number,
  requestIdHeader?: string | false,
  requestIdLogLabel?: string,
  genReqId?: (req) => string,
  trustProxy?: boolean | string | string[] | number,
  ajv?: { customOptions?, plugins? },
  serializerOpts?: { schema?, ajv?, rpiOpts? },
  http2?: boolean,
  https?: { key, cert, ... },
  serverFactory?: ServerFactory,
  return503OnClosing?: boolean,
  forceCloseConnections?: boolean | "idle",
})

// FastifyRequest<RouteGeneric> (types/request.d.ts)
interface FastifyRequest<RouteGeneric extends RouteGenericInterface = RouteGenericInterface> {
  id: string
  params: RouteGeneric["Params"]
  raw: RawRequestDefaultExpression
  query: RouteGeneric["Querystring"]
  body: RouteGeneric["Body"]
  headers: RouteGeneric["Headers"]
  log: FastifyBaseLogger
  server: FastifyInstance
  url: string
  method: string
  routerPath: string
  routerMethod: string
  routeOptions: { url: string; method: string; bodyLimit: number; logLevel: string }
  ip: string
  ips?: string[]
  hostname: string
  protocol: "http" | "https"
  is404: boolean
  socket: Socket
  context: FastifyContext
  getValidationFunction(schema: { httpPart: string }): ValidateFunction
  compileValidationSchema(schema: object, httpPart?: string): ValidateFunction
  validateInput(input: unknown, schema: object | string, httpPart?: string): boolean
}

// FastifyReply (types/reply.d.ts)
interface FastifyReply {
  raw: RawReplyDefaultExpression
  code(statusCode: number): this
  status(statusCode: number): this
  statusCode: number
  header(key: string, value: string): this
  headers(values: Record<string, string>): this
  getHeader(key: string): string | undefined
  getHeaders(): Record<string, string | string[]>
  removeHeader(key: string): this
  hasHeader(key: string): boolean
  type(contentType: string): this
  redirect(url: string, code?: number): this
  callNotFound(): void
  serialize(payload: unknown): string
  serializer(fn: (payload: unknown) => string): this
  send(payload?: unknown): this
  then(onfulfilled, onrejected): Promise<void>
  elapsedTime: number
  log: FastifyBaseLogger
  request: FastifyRequest
  server: FastifyInstance
}

// RouteGenericInterface (types/route.d.ts)
interface RouteGenericInterface {
  Body?: unknown
  Querystring?: unknown
  Params?: unknown
  Headers?: unknown
  Reply?: unknown
}

// Type Provider (types/type-provider.d.ts) — Zod/TypeBox integration
interface FastifyTypeProvider { readonly input: unknown; readonly output: unknown }
interface FastifyTypeProviderDefault extends FastifyTypeProvider { readonly output: this["input"] }

// FastifyInstance — 5 generic parameters (types/instance.d.ts)
interface FastifyInstance<
  RawServer = RawServerDefault,
  RawRequest = RawRequestDefaultExpression<RawServer>,
  RawReply = RawReplyDefaultExpression<RawServer>,
  Logger = FastifyBaseLogger,
  TypeProvider = FastifyTypeProviderDefault
> {
  server: RawServer
  pluginName: string
  prefix: string
  version: string
  log: Logger
  listeningOrigin: string
  addresses(): AddressInfo[]
  withTypeProvider<Provider extends FastifyTypeProvider>(): FastifyInstance<...Provider>  // switch type provider
  initialConfig: Readonly<{ connectionTimeout?, keepAliveTimeout?, bodyLimit?, caseSensitive?, http2?, ... }>  // frozen initial config
  supportedMethods: string[]  // list of HTTP methods
}

// FastifyListenOptions (types/instance.d.ts)
interface FastifyListenOptions {
  port?: number               // default: 0 (random)
  host?: string               // default: localhost
  path?: string               // IPC socket path
  backlog?: number            // default: 511
  exclusive?: boolean
  readableAll?: boolean       // IPC pipe readable for all users
  writableAll?: boolean       // IPC pipe writable for all users
  ipv6Only?: boolean          // disable dual-stack
  signal?: AbortSignal        // abort listener
  listenTextResolver?: (address: string) => string
}
```

## [Hooks_Lifecycle]
```ts
// Request lifecycle hooks (types/hooks.d.ts) — IN ORDER
onRequest     → preParsing  → preValidation → preHandler →
// route handler executes here
preSerialization → onSend   → onResponse

// Hook signatures
app.addHook("onRequest", async (request, reply) => {})
app.addHook("preParsing", async (request, reply, payload) => { return modifiedPayload })
app.addHook("preValidation", async (request, reply) => {})
app.addHook("preHandler", async (request, reply) => {})
app.addHook("preSerialization", async (request, reply, payload) => { return modifiedPayload })
app.addHook("onSend", async (request, reply, payload) => { return modifiedPayload })
app.addHook("onResponse", async (request, reply) => {})
app.addHook("onError", async (request, reply, error) => {})
app.addHook("onTimeout", async (request, reply) => {})          // fires when connectionTimeout exceeded
app.addHook("onRequestAbort", async (request) => {})            // fires when client closes connection early

// Application lifecycle hooks
app.addHook("onReady", async () => {})          // before server starts listening
app.addHook("onListen", async () => {})         // after server starts listening
app.addHook("onClose", async (instance) => {})  // on server close
app.addHook("preClose", async () => {})         // before close begins
app.addHook("onRoute", (routeOptions) => {})    // sync — when route registered
app.addHook("onRegister", (instance, opts) => {}) // sync — when plugin encapsulation context created
```

## [Architectural_Laws]
- **Export_Law**: Export plugins as `FastifyPluginAsync`. Use `fastify-plugin` for plugins that should NOT create encapsulation context. Export route schemas as typed const objects.
- **Transformation_Law**: Plugin-based architecture. Each `register()` call creates an encapsulation context. Use type providers (Zod, TypeBox) for schema-to-type inference. Decorators extend instance/request/reply types.
- **Propagation_Law**: Errors handled via `setErrorHandler`. Hooks short-circuit on `reply.send()`. Use `setNotFoundHandler` for 404. Fastify validates request/response schemas by default using Ajv.

## [Syntax_Rules] | [Naming_Conventions]
- camelCase: route handlers, hook names, plugin names
- kebab-case: URL paths, plugin package names
- PascalCase: type interfaces, type providers

## [Prohibited_Patterns]
- NO Express-style `next()` — Fastify uses async/await or reply chaining
- NO `app.use()` for Fastify plugins — use `app.register()` (Express compat via `@fastify/express`)
- NO mutation of raw request/reply outside hooks
- NO `reply.send()` without `return reply` in async handlers

## [Standard_Library_Signatures]
```ts
// Route registration (types/instance.d.ts)
app.get<RouteGeneric>(url: string, opts?: RouteShorthandOptions, handler: RouteHandlerMethod): FastifyInstance
app.post<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.put<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.delete<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.patch<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.head<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.options<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.all<RouteGeneric>(url: string, opts?, handler): FastifyInstance
app.route<RouteGeneric>(opts: RouteOptions): FastifyInstance
// WebDAV methods: propfind, proppatch, mkcalendar, mkcol, copy, move, lock, unlock, trace, report, search

// Route introspection
app.hasRoute(opts: { method, url, constraints? }): boolean    // check if route exists
app.findRoute(opts: { method, url, constraints? }): FindResult  // find route details
app.printRoutes(opts?: PrintRoutesOptions): string            // radix tree visualization
app.printPlugins(): string                                     // plugin tree visualization

// Custom HTTP methods
app.addHttpMethod(method: string, opts?: { hasBody: boolean }): FastifyInstance
app.supportedMethods: string[]  // ['GET', 'HEAD', 'POST', ...]

// Plugin registration (types/register.d.ts, types/plugin.d.ts)
app.register(plugin: FastifyPluginAsync, opts?: FastifyRegisterOptions): FastifyInstance & SafePromiseLike
app.register(plugin: FastifyPluginCallback, opts?: FastifyRegisterOptions): FastifyInstance & SafePromiseLike
app.after(): FastifyInstance & SafePromiseLike  // execute after current plugin
app.hasPlugin(name: string): boolean

// Type Provider switching
app.withTypeProvider<ZodTypeProvider>(): FastifyInstance<..., ZodTypeProvider>

// Decorators (types/instance.d.ts) — type-safe with getter/setter pattern
app.decorate<T>(name: string | symbol, value: T | { getter: () => T; setter?: (v: T) => void }, deps?: string[]): FastifyInstance
app.decorateRequest<T>(name: string | symbol, value: T, deps?: string[]): FastifyInstance
app.decorateReply<T>(name: string | symbol, value: T, deps?: string[]): FastifyInstance
app.getDecorator<T>(name: string | symbol): T  // retrieve decorator value
app.hasDecorator(name: string | symbol): boolean
app.hasRequestDecorator(name: string | symbol): boolean
app.hasReplyDecorator(name: string | symbol): boolean

// Content type parser (types/content-type-parser.d.ts)
app.addContentTypeParser(contentType: string | string[], opts, parser: (req, body, done) => void): void
app.hasContentTypeParser(contentType: string): boolean
app.removeContentTypeParser(contentType: string | string[] | RegExp): void
app.removeAllContentTypeParsers(): void
app.getDefaultJsonParser(onProtoAction, onConstructorAction): FastifyBodyParser
app.defaultTextParser: FastifyBodyParser<string>

// Schema & Serialization (types/schema.d.ts)
app.addSchema(schema: object): FastifyInstance
app.getSchemas(): Record<string, object>
app.getSchema(schemaId: string): object
app.setValidatorCompiler<T>(compiler: FastifySchemaCompiler<T>): FastifyInstance
app.setSerializerCompiler<T>(compiler: FastifySerializerCompiler<T>): FastifyInstance
app.setSchemaController(opts: FastifySchemaControllerOptions): FastifyInstance
app.setReplySerializer(fn: (payload: unknown, statusCode: number) => string): FastifyInstance
app.setSchemaErrorFormatter(formatter: SchemaErrorFormatter): FastifyInstance
app.validatorCompiler: FastifySchemaCompiler | undefined
app.serializerCompiler: FastifySerializerCompiler | undefined

// Error handling
app.setErrorHandler<TError>(handler: (this: FastifyInstance, error: TError, request: FastifyRequest, reply: FastifyReply) => any): FastifyInstance
app.setNotFoundHandler(handler: RouteHandlerMethod): FastifyInstance
app.setNotFoundHandler(opts: { preValidation?, preHandler? }, handler: RouteHandlerMethod): FastifyInstance
app.errorHandler: (error, request, reply) => void  // access default error handler

// Request ID & Logging
app.setGenReqId(fn: (req: RawRequest) => string): FastifyInstance
app.childLoggerFactory: FastifyChildLoggerFactory
app.setChildLoggerFactory(factory: FastifyChildLoggerFactory): FastifyInstance

// Custom constraints
app.addConstraintStrategy(strategy: ConstraintStrategy): void
app.hasConstraintStrategy(name: string): boolean

// Lifecycle
app.listen(opts: FastifyListenOptions): Promise<string>
app.listen(opts: FastifyListenOptions, callback: (err, address) => void): void
app.ready(): FastifyInstance & SafePromiseLike<undefined>
app.close(): Promise<undefined>
app[Symbol.asyncDispose](): Promise<undefined>  // using declaration support
app.inject(opts: InjectOptions | string): Promise<LightMyRequestResponse>  // for testing
app.inject(): LightMyRequestChain  // chainable testing API
app.routing(req, res): void  // manual routing
```

## [Tactical_Patterns]
```ts
// Type Provider with Zod
import { serializerCompiler, validatorCompiler, ZodTypeProvider } from 'fastify-type-provider-zod'
const app = Fastify().withTypeProvider<ZodTypeProvider>()
app.setValidatorCompiler(validatorCompiler)
app.setSerializerCompiler(serializerCompiler)
app.get('/users/:id', {
  schema: { params: z.object({ id: z.string() }), response: { 200: z.object({ name: z.string() }) } }
}, async (req) => ({ name: req.params.id }))  // fully typed

// Plugin encapsulation with fastify-plugin
import fp from 'fastify-plugin'
export default fp(async (fastify, opts) => {
  fastify.decorate('db', new Database())  // shared across encapsulation
}, { name: 'db-plugin' })

// Decorator getter/setter pattern
app.decorateRequest('user', {
  getter() { return this.headers['x-user'] },
})

// Route-level hooks via opts
app.get('/protected', {
  preHandler: async (req, reply) => { if (!req.headers.auth) reply.code(401).send() }
}, handler)

// Testing with inject()
const response = await app.inject({ method: 'GET', url: '/users/1' })
assert.equal(response.statusCode, 200)
assert.deepStrictEqual(response.json(), { name: 'Alice' })

// Route introspection
console.log(app.printRoutes({ method: 'GET', includeMeta: true }))
console.log(app.hasRoute({ method: 'GET', url: '/users/:id' }))
```
