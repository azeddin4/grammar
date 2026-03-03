---
Language: Drizzle ORM
Version: 0.45.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/drizzle-orm/package.json"
Grammar_Lock: "@root/hashes/grammar/drizzle-orm.hash.md"
---

/** [Project].Grammar.DrizzleORM - Linguistic DNA anchor for Drizzle ORM 0.45.x */

## [SDK_Discovery_Map]
/** === Core (25 definition files) === */
/** @Ref: @root/node_modules/drizzle-orm/index.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/column.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/column-builder.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/table.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/table.utils.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/relations.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/operations.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/errors.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/entity.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/alias.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/batch.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/casing.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/logger.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/migrator.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/query-promise.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/runnable-query.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/session.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/subquery.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/selection-proxy.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/primary-key.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/view-common.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/tracing.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/tracing-utils.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/utils.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/version.d.ts */
/** === pg-core — PostgreSQL dialect (21 definition files) === */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/index.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/table.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/db.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/dialect.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/schema.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/session.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/indexes.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/foreign-keys.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/primary-keys.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/unique-constraint.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/checks.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/policies.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/roles.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/sequence.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/expressions.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/subquery.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/view.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/view-base.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/view-common.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/alias.d.ts */
/** @Ref: @root/node_modules/drizzle-orm/pg-core/utils.d.ts */

## [SDK_Imports / Namespaces]
```ts
// Schema definition (pg-core)
import { pgTable, pgSchema, pgEnum, pgView, pgMaterializedView, pgSequence, pgPolicy, pgRole } from "drizzle-orm/pg-core"
import { uuid, text, varchar, integer, serial, bigint, bigserial, boolean, timestamp, date, time, interval, json, jsonb, real, doublePrecision, numeric, smallint, smallserial, char, cidr, inet, macaddr, macaddr8, vector, point, line, geometry } from "drizzle-orm/pg-core"
import { primaryKey, foreignKey, uniqueIndex, index, check } from "drizzle-orm/pg-core"

// Query building (core)
import { eq, ne, gt, gte, lt, lte, like, ilike, notLike, notIlike, inArray, notInArray, isNull, isNotNull, between, notBetween, exists, notExists, and, or, not, sql, asc, desc, count, sum, avg, min, max } from "drizzle-orm"

// Relations (relations.d.ts)
import { relations, type One, type Many } from "drizzle-orm"

// Type inference (table.d.ts, utils.d.ts)
import type { InferSelectModel, InferInsertModel } from "drizzle-orm"

// Database instance
import { drizzle } from "drizzle-orm/node-postgres"
import { drizzle } from "drizzle-orm/postgres-js"
import { drizzle } from "drizzle-orm/neon-http"
import { drizzle } from "drizzle-orm/vercel-postgres"
```

## [Core_Primitives]
```ts
// Table definition (pg-core/table.d.ts)
const users = pgTable("users", {
  id: uuid("id").defaultRandom().primaryKey(),
  email: varchar("email", { length: 255 }).notNull().unique(),
  name: text("name"),
  role: text("role", { enum: ["admin", "user"] }).default("user").notNull(),
  age: integer("age"),
  score: real("score"),
  metadata: jsonb("metadata").$type<Record<string, unknown>>(),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
  updatedAt: timestamp("updated_at", { withTimezone: true }).$onUpdate(() => new Date()),
})

// Type inference (THE core pattern)
type User = InferSelectModel<typeof users>         // query result type
type NewUser = InferInsertModel<typeof users>       // insert input type

// Column (column.d.ts — 69 lines)
abstract class Column<T> {
  readonly table: Table
  readonly name: string
  readonly primary: boolean
  readonly notNull: boolean
  readonly default: T['data'] | SQL | undefined
  readonly hasDefault: boolean
  readonly isUnique: boolean
  readonly dataType: T['dataType']
  readonly columnType: T['columnType']
  readonly generated?: GeneratedColumnConfig
}

// Relations (relations.d.ts — 216 lines)
const usersRelations = relations(users, ({ one, many }) => ({
  profile: one(profiles, { fields: [users.id], references: [profiles.userId] }),
  posts: many(posts),
}))

// Relation types
class One<TTableName, TIsNullable>    // { fields, references }
class Many<TTableName>                // { relationName }
class Relations<TTableName, TConfig>  // table + config function

// DBQueryConfig (relations.d.ts L102-124)
type DBQueryConfig = {
  columns?: { [K in keyof Columns]?: boolean }
  with?: { [K in keyof Relations]?: true | DBQueryConfig }
  extras?: Record<string, SQL.Aliased> | ((fields, operators) => Record<string, SQL.Aliased>)
  where?: SQL | ((fields, operators) => SQL)      // 'many' only
  orderBy?: ValueOrArray<Column | SQL>             // 'many' only
  limit?: number | Placeholder                     // 'many' only
  offset?: number | Placeholder                    // root 'many' only
}

// Enum (pg-core)
const roleEnum = pgEnum("role", ["admin", "user", "moderator"])
const role = roleEnum("role").default("user").notNull()

// Schema (pg-core/schema.d.ts)
const mySchema = pgSchema("my_schema")
const users = mySchema.table("users", { ... })

// Sequence (pg-core/sequence.d.ts)
const idSeq = pgSequence("id_seq", { startWith: 1, increment: 1 })

// Index (pg-core/indexes.d.ts)
pgTable("users", { ... }, (table) => [
  uniqueIndex("email_idx").on(table.email),
  index("name_idx").on(table.name),
])

// Vector extension columns (pg-core/columns/vector_extension/)
vector("embedding", { dimensions: 1536 })    // pgvector float32 vector
halfvec("embedding", { dimensions: 1536 })   // pgvector float16 vector
sparsevec("embedding", { dimensions: 1536 }) // pgvector sparse vector
bit("flags", { dimensions: 8 })              // bit string

// RLS Policies & Roles (pg-core/policies.d.ts, roles.d.ts)
const adminRole = pgRole("admin")
pgPolicy("users_select", { for: "select", to: adminRole, using: sql`auth.uid() = id` })

// Generated columns (column-builder.d.ts)
integer("total").generatedAlwaysAs(sql`price * quantity`)
integer("id").generatedAlwaysAsIdentity({ startWith: 1, increment: 1 })
integer("id").generatedByDefaultAsIdentity()

// Custom column type (pg-core/columns/custom.d.ts)
const tsvector = customType<{ data: string }>({ dataType: () => "tsvector" })

// Count shorthand
const count = await db.$count(users, eq(users.role, "admin"))
```

## [Architectural_Laws]
- **Export_Law**: Schema definitions in `db/schema.ts`. Relations co-located with schema. DB instance in `db/index.ts`. Export inferred types for use throughout app. Migrations via `drizzle-kit`.
- **Transformation_Law**: Use SQL-like query builder for complex queries. Use relational queries (`db.query.*`) for nested data with `with`. Use `.$type<T>()` for JSON column typing. Inference-first: derive types from schema, never define manually.
- **Propagation_Law**: Database errors bubble as driver-specific errors. Use transactions for atomicity. Use `sql` tagged template for raw SQL when query builder is insufficient.

## [Syntax_Rules] | [Naming_Conventions]
- camelCase: TypeScript identifiers (`users`, `createdAt`)
- snake_case: database column names (passed as first arg to column functions)
- PascalCase: inferred types (`User`, `NewUser`)
- Suffix pattern: `usersRelations`, `roleEnum`

## [Prohibited_Patterns]
- NO manual type definitions for models — use `InferSelectModel<typeof table>` / `InferInsertModel<typeof table>`
- NO string-based column references — use column objects from schema
- NO raw SQL without `sql` tagged template — prevents injection
- NO relation queries without passing schema to `drizzle()` constructor

## [Standard_Library_Signatures]
```ts
// Query builder (pg-core/db.d.ts)
db.select().from(users).where(eq(users.id, id))
db.select({ id: users.id, email: users.email }).from(users)
db.select().from(users).leftJoin(posts, eq(users.id, posts.authorId))
db.select().from(users).where(and(eq(users.role, "admin"), gt(users.age, 18)))
db.select().from(users).orderBy(asc(users.createdAt)).limit(10).offset(20)
db.select({ count: count() }).from(users).where(eq(users.role, "admin"))

// Insert
db.insert(users).values({ email: "a@b.com", name: "Alice" }).returning()
db.insert(users).values([...bulk]).onConflictDoNothing()
db.insert(users).values(data).onConflictDoUpdate({ target: users.email, set: { name: "Updated" } })

// Update
db.update(users).set({ name: "Bob" }).where(eq(users.id, id)).returning()

// Delete
db.delete(users).where(eq(users.id, id)).returning()

// Relational queries (with schema passed to drizzle)
db.query.users.findMany({ with: { posts: true }, where: eq(users.role, "admin"), orderBy: [desc(users.createdAt)], limit: 10 })
db.query.users.findFirst({ where: eq(users.id, id), with: { profile: true, posts: { with: { comments: true }, limit: 5 } } })

// Transactions
db.transaction(async (tx) => {
  const user = await tx.insert(users).values(data).returning()
  await tx.insert(posts).values({ authorId: user[0].id, ... })
})

// Batch (batch.d.ts)
const [allUsers, allPosts] = await db.batch([
  db.select().from(users),
  db.select().from(posts),
])

// Operators (relations.d.ts L68-91)
eq, ne, gt, gte, lt, lte       // comparison
like, ilike, notLike, notIlike  // pattern
inArray, notInArray             // array membership
isNull, isNotNull               // null checks
between, notBetween             // range
exists, notExists               // subquery existence
and, or, not                    // logical combinators
sql                             // raw SQL escape hatch
asc, desc                       // ordering

// Subqueries
const sq = db.select({ avgAge: avg(users.age) }).from(users).as("sq")
db.select().from(users).where(gt(users.age, sq.avgAge))

// Prepared statements
const prepared = db.select().from(users).where(eq(users.id, sql.placeholder("id"))).prepare("get_user")
await prepared.execute({ id: "123" })
```
