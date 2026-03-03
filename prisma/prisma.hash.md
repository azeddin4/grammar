---
Language: Prisma
Version: 7.4.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/@prisma/client/package.json"
Grammar_Lock: "@root/hashes/grammar/prisma.hash.md"
---

/** [Project].Grammar.Prisma - Linguistic DNA anchor for Prisma 7.4.x */

## [SDK_Discovery_Map]
/** === @prisma/client (9 definition files) === */
/** @Ref: @root/node_modules/@prisma/client/index.d.ts */
/** @Ref: @root/node_modules/@prisma/client/default.d.ts */
/** @Ref: @root/node_modules/@prisma/client/edge.d.ts */
/** @Ref: @root/node_modules/@prisma/client/extension.d.ts */
/** @Ref: @root/node_modules/@prisma/client/sql.d.ts */
/** @Ref: @root/node_modules/@prisma/client/runtime/client.d.ts */
/** @Ref: @root/node_modules/@prisma/client/runtime/index-browser.d.ts */
/** @Ref: @root/node_modules/@prisma/client/runtime/wasm-compiler-edge.d.ts */
/** @Ref: @root/node_modules/@prisma/client/scripts/default-index.d.ts */
/** === prisma CLI types === */
/** @Ref: @root/node_modules/prisma/package.json */

## [SDK_Imports / Namespaces]
```ts
import { PrismaClient } from "@prisma/client"
import type { Prisma } from "@prisma/client"
// Edge runtime
import { PrismaClient } from "@prisma/client/edge"
// SQL tagged template
import { sql, raw, join, empty, sqltag } from "@prisma/client/sql"
// Extension types
import type { PrismaClientExtends } from "@prisma/client/extension"
```

## [Core_Primitives]
```ts
// Client instantiation (singleton pattern)
const prisma = new PrismaClient({
  log?: Array<"query" | "info" | "warn" | "error" | { level: string; emit: "stdout" | "event" }>,
  datasources?: { db: { url: string } },
  errorFormat?: "pretty" | "colorless" | "minimal",
})

// Generated model types (per schema.prisma — in default.d.ts)
type User = { id: string; email: string; name: string | null; createdAt: Date }

// Input types (generated)
type UserCreateInput = { email: string; name?: string | null; posts?: PostCreateNestedManyWithoutAuthorInput }
type UserUpdateInput = { email?: StringFieldUpdateOperationsInput; name?: NullableStringFieldUpdateOperationsInput }
type UserWhereInput = { AND?: UserWhereInput[]; OR?: UserWhereInput[]; NOT?: UserWhereInput; id?: StringFilter; email?: StringFilter; ... }
type UserWhereUniqueInput = { id?: string; email?: string } & { AND?: UserWhereInput; ... }
type UserOrderByWithRelationInput = { id?: SortOrder; email?: SortOrder; createdAt?: SortOrder }
type UserSelect = { id?: boolean; email?: boolean; name?: boolean; posts?: boolean | PostFindManyArgs }
type UserInclude = { posts?: boolean | PostFindManyArgs }

// Filter types
type StringFilter = { equals?: string; in?: string[]; notIn?: string[]; lt?: string; lte?: string; gt?: string; gte?: string; contains?: string; startsWith?: string; endsWith?: string; mode?: QueryMode; not?: NestedStringFilter }
type IntFilter = { equals?: number; in?: number[]; notIn?: number[]; lt?: number; lte?: number; gt?: number; gte?: number; not?: NestedIntFilter }
type DateTimeFilter = { equals?: Date; in?: Date[]; notIn?: Date[]; lt?: Date; lte?: Date; gt?: Date; gte?: Date; not?: NestedDateTimeFilter }
enum SortOrder { asc = "asc", desc = "desc" }
enum QueryMode { default = "default", insensitive = "insensitive" }
```

## [Architectural_Laws]
- **Export_Law**: Singleton PrismaClient in `lib/prisma.ts`. In dev, store on `globalThis` to survive HMR: `globalThis.__prisma ??= new PrismaClient()`. Export typed model types from generated client.
- **Transformation_Law**: Use `select` to narrow return shape. Use `include` for relations. Use Prisma-generated types for input/output — never define manual interfaces for DB models.
- **Propagation_Law**: Prisma throws `PrismaClientKnownRequestError` with typed `code` field (P2002 = unique violation, P2025 = record not found). Always catch and map to appropriate HTTP status. Use `$transaction` for atomicity.

## [Syntax_Rules] | [Naming_Conventions]
- PascalCase: model names in schema (`model User`)
- camelCase: field names, relation fields, client methods
- snake_case: database column names (mapped via `@map`)
- Plural: `prisma.user` delegate (singular), relations as plural (`posts`)
- File: `schema.prisma` at project root or `prisma/` directory

## [Prohibited_Patterns]
- NO `new PrismaClient()` per request — singleton or connection pool
- NO raw SQL without parameterization — use `$queryRaw` with tagged template
- NO `any` casts on query results — use generated types
- NO manual type definitions for models — always use `Prisma.UserGetPayload<T>`
- NO `findFirst` without `where` in production — risks returning random record

## [Standard_Library_Signatures]
```ts
// CRUD operations
prisma.user.findUnique({ where: { id }, select?, include? }): Promise<User | null>
prisma.user.findUniqueOrThrow({ where: { id } }): Promise<User>
prisma.user.findFirst({ where?, orderBy?, select?, include?, skip?, cursor? }): Promise<User | null>
prisma.user.findFirstOrThrow({ where? }): Promise<User>
prisma.user.findMany({ where?, orderBy?, select?, include?, skip?, take?, cursor?, distinct? }): Promise<User[]>
prisma.user.create({ data, select?, include? }): Promise<User>
prisma.user.createMany({ data: UserCreateInput[], skipDuplicates? }): Promise<BatchPayload>
prisma.user.createManyAndReturn({ data, select? }): Promise<User[]>
prisma.user.update({ where, data, select?, include? }): Promise<User>
prisma.user.updateMany({ where, data }): Promise<BatchPayload>
prisma.user.upsert({ where, create, update, select?, include? }): Promise<User>
prisma.user.delete({ where, select?, include? }): Promise<User>
prisma.user.deleteMany({ where? }): Promise<BatchPayload>
prisma.user.count({ where?, cursor?, skip?, take? }): Promise<number>
prisma.user.aggregate({ where?, _count?, _sum?, _avg?, _min?, _max? }): Promise<AggregateUser>
prisma.user.groupBy({ by, where?, having?, _count?, _sum?, _avg?, _min?, _max?, orderBy?, skip?, take? }): Promise<GroupByUser[]>

// Transactions (runtime/client.d.ts)
prisma.$transaction<T>(fn: (tx: PrismaClient) => Promise<T>, options?: { maxWait?, timeout?, isolationLevel? }): Promise<T>
prisma.$transaction<T>(queries: PrismaPromise<T>[]): Promise<T[]>  // batch

// Raw queries (sql.d.ts)
prisma.$queryRaw<T>(query: TemplateStringsArray | Prisma.Sql, ...values: any[]): Promise<T[]>
prisma.$executeRaw(query: TemplateStringsArray | Prisma.Sql, ...values: any[]): Promise<number>
prisma.$queryRawTyped<T>(query: TypedSql<T>): Promise<T[]>  // typesafe SQL (v5.9+)

// Client extensions (extension.d.ts)
const xprisma = prisma.$extends({
  model?: { user: { customMethod() {} } },
  client?: { customClientMethod() {} },
  query?: { user: { findMany({ model, operation, args, query }) {} } },
  result?: { user: { fullName: { needs: { firstName: true, lastName: true }, compute(user) { return `${user.firstName} ${user.lastName}` } } } },
})

// Lifecycle
prisma.$connect(): Promise<void>
prisma.$disconnect(): Promise<void>
prisma.$on(event: "query" | "info" | "warn" | "error", callback): void
```

## [Error_Modeling]
```ts
// PrismaClientKnownRequestError (runtime/client.d.ts)
class PrismaClientKnownRequestError extends Error {
  code: string         // P2002, P2025, etc.
  meta?: Record<string, unknown>
  clientVersion: string
}
// Common codes:
// P2002 — Unique constraint violation
// P2003 — Foreign key constraint violation
// P2025 — Record not found (findUniqueOrThrow, update, delete)
// P2014 — Relation violation
// P2000 — Value too long

class PrismaClientUnknownRequestError extends Error {}
class PrismaClientRustPanicError extends Error {}
class PrismaClientInitializationError extends Error { errorCode?: string }
class PrismaClientValidationError extends Error {}

// Sentinel types for JSON fields (runtime/client.d.ts)
Prisma.DbNull     // JSON column IS NULL in database
Prisma.JsonNull   // JSON column contains literal null value
Prisma.AnyNull    // matches either DbNull or JsonNull

// Decimal type
Prisma.Decimal    // arbitrary-precision decimal (from @prisma/client-runtime-utils)

// Type-safe query args reuse
Prisma.validator<Prisma.UserFindManyArgs>()({ where: { role: "admin" } })

// Payload type helper (infer result type from query args)
type UserWithPosts = Prisma.UserGetPayload<{ include: { posts: true } }>

// Omit feature (v5.13+) — exclude fields from default selection
// prisma.user.findMany({ omit: { password: true } })
// Global omit in client: new PrismaClient({ omit: { user: { password: true } } })
```
