---
Language: TanStack React Query
Version: 5.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/@tanstack/react-query/package.json"
Grammar_Lock: "@root/hashes/grammar/tanstack-react-query.hash.md"
---

/** [Project].Grammar.TanStackReactQuery - Linguistic DNA anchor for TanStack React Query 5.x */

## [SDK_Discovery_Map]
/** === Modern Build (entry point + 23 module files) === */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/index.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/types.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useInfiniteQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useMutation.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useQueries.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useSuspenseQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useSuspenseInfiniteQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useSuspenseQueries.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/usePrefetchQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/usePrefetchInfiniteQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useIsFetching.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useMutationState.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/useBaseQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/queryOptions.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/infiniteQueryOptions.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/mutationOptions.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/suspense.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/errorBoundaryUtils.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/QueryClientProvider.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/QueryErrorResetBoundary.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/HydrationBoundary.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/modern/IsRestoringProvider.d.ts */
/** === Legacy Build (backward compat, same modules) === */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/index.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/types.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useInfiniteQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useMutation.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useQueries.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useSuspenseQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useSuspenseInfiniteQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useSuspenseQueries.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/usePrefetchQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/usePrefetchInfiniteQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useIsFetching.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useMutationState.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/useBaseQuery.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/queryOptions.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/infiniteQueryOptions.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/mutationOptions.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/suspense.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/errorBoundaryUtils.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/QueryClientProvider.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/QueryErrorResetBoundary.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/HydrationBoundary.d.ts */
/** @Ref: @root/node_modules/@tanstack/react-query/build/legacy/IsRestoringProvider.d.ts */

## [SDK_Imports / Namespaces]
```ts
// Re-exports from @tanstack/query-core (via modern/index.d.ts L1)
import { QueryClient, QueryCache, MutationCache, QueryObserver, InfiniteQueryObserver, MutationObserver, QueriesObserver, focusManager, onlineManager, notifyManager, hashKey, keepPreviousData, skipToken, streamedQuery, dehydrate, hydrate, CancelledError } from "@tanstack/react-query"
import type { QueryKey, QueryFunction, QueryFunctionContext, QueryFilters, MutationFilters, QueryOptions, MutationOptions, InfiniteData, DefaultError, QueryMeta, MutationMeta, MutationKey, Updater, DehydratedState, DehydrateOptions, HydrateOptions, QueryState, MutationState, FetchStatus, QueryStatus, MutationStatus, NetworkMode, DataTag, SkipToken, StaleTime, NotifyOnChangeProps, QueryPersister, MutationScope, MutationFunctionContext } from "@tanstack/react-query"

// React hooks (modern/index.d.ts L2-22)
import { useQuery, useInfiniteQuery, useMutation, useQueries, useSuspenseQuery, useSuspenseInfiniteQuery, useSuspenseQueries, usePrefetchQuery, usePrefetchInfiniteQuery, useIsFetching, useIsMutating, useMutationState, useQueryClient, useQueryErrorResetBoundary, useIsRestoring } from "@tanstack/react-query"

// Option factories
import { queryOptions, infiniteQueryOptions, mutationOptions } from "@tanstack/react-query"

// Type helpers (modern/types.d.ts)
import type { UseQueryOptions, UseQueryResult, DefinedUseQueryResult, UseInfiniteQueryOptions, UseInfiniteQueryResult, DefinedUseInfiniteQueryResult, UseMutationOptions, UseMutationResult, UseSuspenseQueryOptions, UseSuspenseQueryResult, UseSuspenseInfiniteQueryOptions, UseSuspenseInfiniteQueryResult, UseMutateFunction, UseMutateAsyncFunction, UsePrefetchQueryOptions, QueriesOptions, QueriesResults, SuspenseQueriesOptions, SuspenseQueriesResults, UseBaseQueryOptions } from "@tanstack/react-query"

// Components
import { QueryClientProvider, QueryClientContext, HydrationBoundary, QueryErrorResetBoundary, IsRestoringProvider } from "@tanstack/react-query"
import type { QueryClientProviderProps, HydrationBoundaryProps, QueryErrorResetBoundaryProps } from "@tanstack/react-query"
```

## [Core_Primitives]
```ts
// QueryClient (query-core/queryClient.d.ts)
const queryClient = new QueryClient({
  queryCache?: new QueryCache({ onError?, onSuccess?, onSettled? }),
  mutationCache?: new MutationCache({ onError?, onSuccess?, onMutate?, onSettled? }),
  defaultOptions?: {
    queries?: { staleTime?, gcTime?, retry?, retryDelay?, refetchOnWindowFocus?, refetchOnReconnect?, refetchOnMount?, refetchInterval?, refetchIntervalInBackground?, networkMode?, structuralSharing?, notifyOnChangeProps?, experimental_prefetchInRender? },
    mutations?: { retry?, retryDelay?, networkMode?, gcTime?, scope? },
    dehydrate?: DehydrateOptions,
    hydrate?: HydrateOptions,
  }
})

// QueryCache (query-core/queryCache.d.ts) — global observer
const queryCache = new QueryCache({
  onError?: (error, query) => void,          // fires when ANY query errors
  onSuccess?: (data, query) => void,         // fires when ANY query succeeds
  onSettled?: (data, error, query) => void,  // fires when ANY query settles
})
queryCache.subscribe((event) => {})  // event.type: 'added' | 'removed' | 'updated' | 'observerAdded' | 'observerRemoved' | 'observerResultsUpdated' | 'observerOptionsUpdated'
queryCache.getAll(): Query[]
queryCache.find(filters): Query | undefined
queryCache.findAll(filters?): Query[]
queryCache.clear(): void

// MutationCache (query-core/mutationCache.d.ts) — global observer
const mutationCache = new MutationCache({
  onError?: (error, variables, onMutateResult, mutation, context) => void,
  onSuccess?: (data, variables, onMutateResult, mutation, context) => void,
  onMutate?: (variables, mutation, context) => void,
  onSettled?: (data, error, variables, onMutateResult, mutation, context) => void,
})
mutationCache.subscribe((event) => {})  // event.type: 'added' | 'removed' | 'updated' | 'observerAdded' | 'observerRemoved' | 'observerOptionsUpdated'
mutationCache.getAll(): Mutation[]
mutationCache.find(filters): Mutation | undefined
mutationCache.findAll(filters?): Mutation[]
mutationCache.resumePausedMutations(): Promise<unknown>

// Query key pattern (THE foundational concept)
type QueryKey = readonly unknown[]
// Convention: ["entity", "action", { filters }]
// e.g., ["users", "list", { role: "admin" }]
// e.g., ["users", "detail", userId]

// DataTag — type-safe query key tagging (query-core/types.d.ts)
type DataTag<TType, TValue, TError = UnsetMarker> = TType & { [dataTagSymbol]: TValue; [dataTagErrorSymbol]: TError }
// Usage: const key = ["users"] as DataTag<["users"], User[]> // getQueryData infers User[]

// QueryState (query-core/query.d.ts)
interface QueryState<TData, TError> {
  data: TData | undefined
  dataUpdateCount: number
  dataUpdatedAt: number
  error: TError | null
  errorUpdateCount: number
  errorUpdatedAt: number
  fetchFailureCount: number
  fetchFailureReason: TError | null
  fetchMeta: FetchMeta | null
  isInvalidated: boolean
  status: QueryStatus     // 'pending' | 'error' | 'success'
  fetchStatus: FetchStatus // 'fetching' | 'paused' | 'idle'
}

// MutationState (query-core/mutation.d.ts)
interface MutationState<TData, TError, TVariables, TOnMutateResult> {
  context: TOnMutateResult | undefined
  data: TData | undefined
  error: TError | null
  failureCount: number
  failureReason: TError | null
  isPaused: boolean
  status: MutationStatus  // 'idle' | 'pending' | 'success' | 'error'
  variables: TVariables | undefined
  submittedAt: number
}

// QueryFilters (query-core/utils.d.ts)
interface QueryFilters<TQueryKey extends QueryKey = QueryKey> {
  type?: 'all' | 'active' | 'inactive'
  exact?: boolean
  predicate?: (query: Query) => boolean
  queryKey?: TQueryKey
  stale?: boolean
  fetchStatus?: FetchStatus
}

// MutationFilters (query-core/utils.d.ts)
interface MutationFilters<TData, TError, TVariables, TOnMutateResult> {
  exact?: boolean
  predicate?: (mutation: Mutation) => boolean
  mutationKey?: MutationKey
  status?: MutationStatus
}

// MutationScope — serial execution grouping
interface MutationScope { id: string }

// MutationFunctionContext — v5 context parameter
interface MutationFunctionContext { client: QueryClient; meta: MutationMeta | undefined; mutationKey?: MutationKey }

// queryOptions factory (modern/queryOptions.d.ts)
const userQueryOptions = (userId: string) => queryOptions({
  queryKey: ["users", "detail", userId] as const,
  queryFn: () => fetchUser(userId),
  staleTime: 5 * 60 * 1000,
})
// Type helpers from queryOptions:
type DefinedInitialDataOptions   // when initialData is provided
type UndefinedInitialDataOptions // when initialData is NOT provided
type UnusedSkipTokenOptions      // when skipToken is not used

// infiniteQueryOptions factory (modern/infiniteQueryOptions.d.ts)
const postsInfiniteOptions = infiniteQueryOptions({
  queryKey: ["posts", "infinite"],
  queryFn: ({ pageParam }) => fetchPosts(pageParam),
  initialPageParam: 0,
  getNextPageParam: (lastPage, pages) => lastPage.nextCursor,
  getPreviousPageParam: (firstPage) => firstPage.prevCursor,
})
// Type helpers: DefinedInitialDataInfiniteOptions, UndefinedInitialDataInfiniteOptions, UnusedSkipTokenInfiniteOptions

// mutationOptions factory (modern/mutationOptions.d.ts)
const createUserMutation = mutationOptions({
  mutationFn: (data: CreateUserInput) => createUser(data),
  onSuccess: (data, variables, onMutateResult, context) => { context.client.invalidateQueries({ queryKey: ["users"] }) },
  scope: { id: "user-mutations" },  // serialize mutations with same scope
})

// StaleTime — supports 'static' for never-stale + function form
type StaleTime = number | 'static'
type StaleTimeFunction = StaleTime | ((query: Query) => StaleTime)

// Enabled — supports function form for conditional fetching
type Enabled = boolean | ((query: Query) => boolean)

// streamedQuery (query-core/streamedQuery.d.ts) — streaming data from AsyncIterables
const streamingOptions = queryOptions({
  queryKey: ["stream"],
  queryFn: streamedQuery({
    streamFn: async function*(ctx) { yield* fetchStream(ctx.signal) },
    refetchMode: 'reset' | 'append' | 'replace',  // default: 'reset'
    reducer: (acc, chunk) => acc + chunk,            // optional custom reducer
    initialValue: "",                                // required with reducer
  }),
})
```

## [Hooks_API]
```ts
// useQuery (modern/useQuery.d.ts) — full return type: QueryObserverResult (25+ fields)
const {
  data,                  // TData | undefined
  error,                 // TError | null
  status,                // 'pending' | 'error' | 'success'
  fetchStatus,           // 'fetching' | 'paused' | 'idle'
  isLoading,             // isFetching && isPending (first fetch)
  isPending,             // no cached data, no finished attempt
  isFetching,            // queryFn executing (includes background refetch)
  isError,               // status === 'error'
  isSuccess,             // status === 'success'
  isStale,               // data invalidated or older than staleTime
  isRefetching,          // isFetching && !isPending
  isLoadingError,        // failed on first fetch
  isRefetchError,        // failed on refetch (has stale data)
  isPaused,              // wanted to fetch but paused (offline)
  isFetched,             // has been fetched at least once
  isFetchedAfterMount,   // fetched after this component mounted
  isPlaceholderData,     // showing placeholder data
  isEnabled,             // observer is enabled
  dataUpdatedAt,         // timestamp of last success
  errorUpdatedAt,        // timestamp of last error
  errorUpdateCount,      // total error count
  failureCount,          // consecutive failure count
  failureReason,         // last failure reason
  refetch,               // (options?: RefetchOptions) => Promise<QueryObserverResult>
  promise,               // stable Promise<TData> (experimental_prefetchInRender)
} = useQuery({
  queryKey: QueryKey,
  queryFn: QueryFunction<TData, TQueryKey> | SkipToken,
  enabled?: boolean | ((query) => boolean),         // supports function form
  staleTime?: number | 'static' | ((query) => StaleTime),
  gcTime?: number,                       // default: 5min (was cacheTime in v4)
  refetchOnWindowFocus?: boolean | 'always' | ((query) => boolean | 'always'),
  refetchOnReconnect?: boolean | 'always' | ((query) => boolean | 'always'),
  refetchOnMount?: boolean | 'always' | ((query) => boolean | 'always'),
  refetchInterval?: number | false | ((query) => number | false | undefined),
  refetchIntervalInBackground?: boolean,  // continue interval while backgrounded
  retry?: boolean | number | ((failureCount, error) => boolean),
  retryDelay?: number | ((attemptIndex, error) => number),
  retryOnMount?: boolean,                 // retry on mount if error cached
  select?: (data: TData) => TSelected,
  initialData?: TData | (() => TData),
  initialDataUpdatedAt?: number | (() => number | undefined),
  placeholderData?: TData | ((previousData, previousQuery) => TData) | typeof keepPreviousData,
  networkMode?: 'online' | 'always' | 'offlineFirst',
  meta?: QueryMeta,
  throwOnError?: boolean | ((error, query) => boolean),
  notifyOnChangeProps?: Array<keyof QueryObserverResult> | 'all' | (() => ...),  // control re-renders
  structuralSharing?: boolean | ((oldData, newData) => unknown),  // deep equality optimization
  persister?: QueryPersister,             // custom persistence layer
  subscribed?: boolean,                   // false to unsubscribe from cache updates (react-query specific)
  experimental_prefetchInRender?: boolean, // enable React.use(query.promise)
})

// useInfiniteQuery (modern/useInfiniteQuery.d.ts)
const { data, fetchNextPage, fetchPreviousPage, hasNextPage, hasPreviousPage, isFetchingNextPage, isFetchingPreviousPage, isFetchNextPageError, isFetchPreviousPageError, ... } = useInfiniteQuery({
  ...queryOptions,
  initialPageParam: TPageParam,
  getNextPageParam: (lastPage, allPages, lastPageParam, allPageParams) => TPageParam | undefined | null,
  getPreviousPageParam?: (firstPage, allPages, firstPageParam, allPageParams) => TPageParam | undefined | null,
  maxPages?: number,
  subscribed?: boolean,
})
// data.pages: TData[]        data.pageParams: TPageParam[]

// useMutation (modern/useMutation.d.ts) — v5 callbacks receive MutationFunctionContext
const { mutate, mutateAsync, data, error, isIdle, isPending, isSuccess, isError, reset, variables, context, submittedAt, failureCount, failureReason, isPaused, status } = useMutation({
  mutationFn: (variables: TVariables, context: MutationFunctionContext) => Promise<TData>,
  mutationKey?: MutationKey,
  onMutate?: (variables, context: MutationFunctionContext) => Promise<TOnMutateResult> | TOnMutateResult,
  onSuccess?: (data, variables, onMutateResult, context: MutationFunctionContext) => void,
  onError?: (error, variables, onMutateResult, context: MutationFunctionContext) => void,
  onSettled?: (data, error, variables, onMutateResult, context: MutationFunctionContext) => void,
  retry?: number | boolean | ((failureCount, error) => boolean),
  retryDelay?: number | ((attemptIndex, error) => number),
  gcTime?: number,
  networkMode?: NetworkMode,
  meta?: MutationMeta,
  scope?: MutationScope,      // { id: string } — serialize mutations with same scope
  throwOnError?: boolean | ((error) => boolean),
})
// mutate(variables, { onSuccess?, onError?, onSettled? })   — per-call overrides
// mutateAsync returns Promise<TData> (throwable)

// useSuspenseQuery (modern/useSuspenseQuery.d.ts) — data is ALWAYS defined
const { data } = useSuspenseQuery({ queryKey, queryFn })
// No isLoading, isPending, isPlaceholderData, enabled, placeholderData, throwOnError
// queryFn cannot be skipToken

// useSuspenseInfiniteQuery (modern/useSuspenseInfiniteQuery.d.ts)
const { data, fetchNextPage, hasNextPage } = useSuspenseInfiniteQuery({ queryKey, queryFn, initialPageParam, getNextPageParam })

// useQueries (modern/useQueries.d.ts) — parallel queries
const results = useQueries({ queries: [queryOptions1, queryOptions2, queryOptions3], combine?: (results) => combinedResult })

// useSuspenseQueries (modern/useSuspenseQueries.d.ts) — parallel suspense queries
const results = useSuspenseQueries({ queries: [...], combine? })

// usePrefetchQuery (modern/usePrefetchQuery.d.ts)
usePrefetchQuery({ queryKey, queryFn, staleTime })  // triggers prefetch during render

// usePrefetchInfiniteQuery (modern/usePrefetchInfiniteQuery.d.ts)
usePrefetchInfiniteQuery({ queryKey, queryFn, initialPageParam, getNextPageParam })

// useIsFetching (modern/useIsFetching.d.ts)
const fetchingCount = useIsFetching(filters?: QueryFilters)  // number of active fetches

// useIsMutating — number of active mutations
const mutatingCount = useIsMutating(filters?: MutationFilters)

// useMutationState (modern/useMutationState.d.ts) — observe all mutations
const mutations = useMutationState({ filters?: MutationFilters, select?: (mutation) => TResult })

// useQueryClient (modern/QueryClientProvider.d.ts)
const queryClient = useQueryClient(queryClient?: QueryClient)  // optional override

// useQueryErrorResetBoundary (modern/QueryErrorResetBoundary.d.ts)
const { clearReset, isReset, reset } = useQueryErrorResetBoundary()

// useIsRestoring (modern/IsRestoringProvider.d.ts) — SSR hydration detection
const isRestoring = useIsRestoring()
```

## [Architectural_Laws]
- **Export_Law**: Define query options outside components using `queryOptions()` factory. Export query keys as const arrays. Export mutation options using `mutationOptions()` factory. Co-locate query options with their fetcher functions.
- **Transformation_Law**: Stale-while-revalidate by default. Data caches are de-duplicated by query key. Use `select` for derived data. Use `placeholderData: keepPreviousData` for pagination. Use `structuralSharing` for deep equality optimization.
- **Propagation_Law**: Use `useSuspenseQuery` with Suspense boundaries. Use `QueryErrorResetBoundary` with Error boundaries. Use `onError` callbacks in mutations. Use `throwOnError` to bubble to error boundaries. Use `MutationScope` for serial mutation execution.
- **Cache_Law**: `gcTime` controls garbage collection (default 5min). `staleTime` controls freshness (default 0). `'static'` staleTime means data is never considered stale. Use `QueryCache`/`MutationCache` global callbacks for app-wide side effects.

## [Syntax_Rules] | [Naming_Conventions]
- camelCase: query/mutation key segments (`["users", "detail", userId]`)
- Query keys: hierarchical arrays, broadest scope first (`["users"] > ["users", "detail", id]`)
- Query function: receives `{ queryKey, signal, meta, client, pageParam? }` context
- Mutation function: receives `(variables, { client, meta, mutationKey? })` context
- skipToken: use instead of `enabled: false` to disable query while preserving type safety

## [Prohibited_Patterns]
- NO direct state management with query data — use `select` for transformations or `queryClient.setQueryData` for updates
- NO `queryFn: skipToken` in suspense queries — skipToken is excluded from suspense types
- NO `enabled: false` in suspense queries — enabled is excluded from suspense types
- NO `async () => fetch(...)` without checking `response.ok` — query-core does NOT reject on HTTP errors
- NO stale closures in `setQueryData` updater — always use the functional form `(old) => newValue`
- NO mutation key collisions when using `scope` — mutations with the same scope.id are serialized

## [Standard_Library_Signatures]
```ts
// QueryClient methods (from @tanstack/query-core — queryClient.d.ts)
queryClient.invalidateQueries({ queryKey?, exact?, predicate?, type?, stale?, fetchStatus?, refetchType?: 'active'|'inactive'|'all'|'none' }): Promise<void>
queryClient.refetchQueries({ queryKey?, exact?, predicate?, type? }, { cancelRefetch?, throwOnError? }): Promise<void>
queryClient.cancelQueries({ queryKey?, exact?, predicate? }, { revert?, silent? }): Promise<void>
queryClient.removeQueries({ queryKey?, exact?, predicate? }): void
queryClient.resetQueries({ queryKey?, exact?, predicate? }): Promise<void>
queryClient.getQueryData<T>(queryKey: QueryKey): T | undefined  // supports DataTag inference
queryClient.setQueryData<T>(queryKey: QueryKey, updater: T | ((old: T | undefined) => T | undefined), options?: { updatedAt? }): T | undefined
queryClient.getQueriesData<T>(filters: QueryFilters): [QueryKey, T | undefined][]
queryClient.setQueriesData<T>(filters: QueryFilters, updater: Updater<T | undefined, T | undefined>): [QueryKey, T | undefined][]
queryClient.getQueryState(queryKey: QueryKey): QueryState | undefined
queryClient.ensureQueryData(options: { ...FetchQueryOptions, revalidateIfStale? }): Promise<TData>
queryClient.ensureInfiniteQueryData(options: { ...FetchInfiniteQueryOptions, revalidateIfStale? }): Promise<InfiniteData<TData>>
queryClient.prefetchQuery(options: FetchQueryOptions): Promise<void>
queryClient.prefetchInfiniteQuery(options: FetchInfiniteQueryOptions): Promise<void>
queryClient.fetchQuery(options: FetchQueryOptions): Promise<TData>
queryClient.fetchInfiniteQuery(options: FetchInfiniteQueryOptions): Promise<InfiniteData<TData>>
queryClient.isFetching(filters?: QueryFilters): number
queryClient.isMutating(filters?: MutationFilters): number
queryClient.getQueryDefaults(queryKey: QueryKey): QueryObserverOptions
queryClient.setQueryDefaults(queryKey: QueryKey, options: Partial<QueryObserverOptions>): void
queryClient.getMutationDefaults(mutationKey: MutationKey): MutationObserverOptions
queryClient.setMutationDefaults(mutationKey: MutationKey, options: MutationObserverOptions): void
queryClient.getDefaultOptions(): DefaultOptions
queryClient.setDefaultOptions(options: DefaultOptions): void
queryClient.getQueryCache(): QueryCache
queryClient.getMutationCache(): MutationCache
queryClient.mount(): void      // start listening to focus/online events
queryClient.unmount(): void    // stop listening
queryClient.resumePausedMutations(): Promise<unknown>
queryClient.clear(): void

// Dehydration / Hydration (query-core/hydration.d.ts)
const dehydratedState: DehydratedState = dehydrate(queryClient, {
  shouldDehydrateQuery?: (query) => boolean,     // default: only successful queries
  shouldDehydrateMutation?: (mutation) => boolean,
  shouldRedactErrors?: (error) => boolean,
  serializeData?: (data) => any,
})
hydrate(queryClient, dehydratedState, {
  defaultOptions?: { deserializeData?, queries?, mutations? }
})
interface DehydratedState { mutations: DehydratedMutation[]; queries: DehydratedQuery[] }

// Managers (singletons)
focusManager.setFocused(focused?: boolean): void   // manually set focus state
focusManager.isFocused(): boolean
focusManager.setEventListener(setup: (setFocused) => cleanup): void  // custom focus listener
onlineManager.setOnline(online: boolean): void     // manually set online state
onlineManager.isOnline(): boolean
onlineManager.setEventListener(setup: (setOnline) => cleanup): void  // custom online listener
notifyManager.setBatchNotifyFunction(fn): void     // custom batching (e.g., React.unstable_batchedUpdates)

// Utility functions
hashKey(queryKey: QueryKey | MutationKey): string    // deterministic hash
partialMatchKey(a: QueryKey, b: QueryKey): boolean   // b partially matches a
keepPreviousData<T>(previousData: T | undefined): T | undefined  // placeholder data helper
skipToken  // unique symbol to disable queryFn while preserving types

// CancelledError (query-core/retryer.d.ts)
class CancelledError extends Error { revert?: boolean; silent?: boolean }

// SSR / Hydration (modern/HydrationBoundary.d.ts)
<QueryClientProvider client={queryClient}><HydrationBoundary state={dehydratedState}>{children}</HydrationBoundary></QueryClientProvider>

// Error Reset Boundary (modern/QueryErrorResetBoundary.d.ts)
<QueryErrorResetBoundary>{({ clearReset, isReset, reset }) => (<ErrorBoundary onReset={reset} fallbackRender={({ resetErrorBoundary }) => ...}><Component /></ErrorBoundary>)}</QueryErrorResetBoundary>

// IsRestoringProvider — wrap in SSR restoration context
<IsRestoringProvider value={isRestoring}>{children}</IsRestoringProvider>

// Devtools (separate package)
import { ReactQueryDevtools } from "@tanstack/react-query-devtools"
<ReactQueryDevtools initialIsOpen={false} />
```

## [Tactical_Patterns]
```ts
// Optimistic Updates (mutation + cache rollback)
const mutation = useMutation({
  mutationFn: updateTodo,
  onMutate: async (newTodo) => {
    await queryClient.cancelQueries({ queryKey: ["todos"] })
    const previous = queryClient.getQueryData(["todos"])
    queryClient.setQueryData(["todos"], (old) => [...old, newTodo])
    return { previous }  // returned as onMutateResult
  },
  onError: (err, newTodo, onMutateResult) => {
    queryClient.setQueryData(["todos"], onMutateResult.previous)
  },
  onSettled: () => queryClient.invalidateQueries({ queryKey: ["todos"] }),
})

// Dependent queries (enabled as function)
const { data: user } = useQuery({ queryKey: ["user", id], queryFn: () => fetchUser(id) })
const { data: projects } = useQuery({
  queryKey: ["projects", user?.id],
  queryFn: () => fetchProjectsByUser(user!.id),
  enabled: (query) => !!user?.id && query.state.dataUpdateCount === 0,  // v5 function form
})

// Pagination with keepPreviousData
const { data, isPlaceholderData } = useQuery({
  queryKey: ["projects", page],
  queryFn: () => fetchProjects(page),
  placeholderData: keepPreviousData,  // show previous page while fetching
})

// Prefetching on hover
const prefetchUser = (id: string) => queryClient.prefetchQuery(userQueryOptions(id))
<Link onMouseEnter={() => prefetchUser(id)} />

// Streaming with streamedQuery
const { data: chunks } = useQuery({
  queryKey: ["ai-response"],
  queryFn: streamedQuery({ streamFn: (ctx) => aiStream(ctx.signal), refetchMode: 'reset' }),
})

// React.use() integration (experimental)
const query = useQuery({ queryKey: ["data"], queryFn: fetchData, experimental_prefetchInRender: true })
const data = React.use(query.promise)  // inside Suspense boundary
```
