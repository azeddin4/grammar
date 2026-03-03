---
Language: React
Version: 19.x
Fidelity: 100% (Physical Disk Reference)
State_ID: BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/react/package.json"
Grammar_Lock: "@root/hashes/grammar/react.hash.md"
---

/** [Project].Grammar.React - Linguistic DNA anchor for React 19.x */

## [SDK_Discovery_Map]
/** === @types/react (13 definition files) === */
/** @Ref: @root/node_modules/@types/react/index.d.ts */
/** @Ref: @root/node_modules/@types/react/global.d.ts */
/** @Ref: @root/node_modules/@types/react/jsx-runtime.d.ts */
/** @Ref: @root/node_modules/@types/react/jsx-dev-runtime.d.ts */
/** @Ref: @root/node_modules/@types/react/canary.d.ts */
/** @Ref: @root/node_modules/@types/react/experimental.d.ts */
/** @Ref: @root/node_modules/@types/react/compiler-runtime.d.ts */
/** @Ref: @root/node_modules/@types/react/ts5.0/index.d.ts */
/** @Ref: @root/node_modules/@types/react/ts5.0/global.d.ts */
/** @Ref: @root/node_modules/@types/react/ts5.0/jsx-runtime.d.ts */
/** @Ref: @root/node_modules/@types/react/ts5.0/jsx-dev-runtime.d.ts */
/** @Ref: @root/node_modules/@types/react/ts5.0/canary.d.ts */
/** @Ref: @root/node_modules/@types/react/ts5.0/experimental.d.ts */

## [SDK_Imports / Namespaces]
```ts
import React from "react"
import { useState, useEffect, useContext, useRef, useMemo, useCallback, useReducer,
  useId, useTransition, useDeferredValue, useSyncExternalStore, useInsertionEffect,
  useImperativeHandle, useLayoutEffect, useDebugValue, useOptimistic, useActionState,
  use, useEffectEvent, startTransition, createContext, forwardRef, memo, lazy,
  createRef, act, cache } from "react"
import type { FC, FunctionComponent, ReactNode, ReactElement, JSX, RefObject,
  ComponentProps, ComponentPropsWithRef, ComponentPropsWithoutRef, ComponentRef,
  PropsWithChildren, PropsWithoutRef, ForwardRefRenderFunction, ForwardedRef,
  Dispatch, SetStateAction, Reducer, ReducerWithoutAction, DependencyList,
  EffectCallback, Context, ExoticComponent, MemoExoticComponent,
  SuspenseProps, Usable, ReactPromise, TransitionStartFunction,
  SyntheticEvent, MouseEvent, KeyboardEvent, ChangeEvent, FocusEvent,
  SubmitEvent, TouchEvent, DragEvent, PointerEvent, WheelEvent,
  AnimationEvent, TransitionEvent, ClipboardEvent, InputEvent, ToggleEvent,
  EventHandler, MouseEventHandler, KeyboardEventHandler, ChangeEventHandler,
  SubmitEventHandler, FocusEventHandler, PointerEventHandler,
  HTMLAttributes, HTMLProps, DetailedHTMLProps, SVGProps, DOMAttributes,
  CSSProperties, Ref, RefCallback, Component, PureComponent,
  ComponentClass, ComponentLifecycle, ErrorInfo, ActivityProps } from "react"
```

## [Core_Primitives]
```ts
// Component types (index.d.ts L1030-1086)
type FC<P = {}> = FunctionComponent<P>
interface FunctionComponent<P = {}> {
  (props: P): ReactNode | Promise<ReactNode>  // React 19: async components
  displayName?: string
}

// Class components (index.d.ts L910-983) — legacy but supported
class Component<P = {}, S = {}, SS = any> {
  constructor(props: P)
  setState<K extends keyof S>(state: ((prev: Readonly<S>, props: Readonly<P>) => Pick<S, K> | S | null) | (Pick<S, K> | S | null), callback?: () => void): void
  forceUpdate(callback?: () => void): void
  render(): ReactNode
  readonly props: Readonly<P>
  state: Readonly<S>
  context: unknown
  static contextType?: Context<any>
}
class PureComponent<P = {}, S = {}, SS = any> extends Component<P, S, SS> {}

// Ref types
interface RefObject<T> { current: T }
type RefCallback<T> = (instance: T | null) => void
type Ref<T> = RefCallback<T> | RefObject<T> | null
type ForwardedRef<T> = ((instance: T | null) => void) | RefObject<T | null> | null

// Node types
type ReactNode = ReactElement | string | number | bigint | boolean | null | undefined | Iterable<ReactNode> | Promise<ReactNode>

// Context (index.d.ts L586-625)
interface Context<T> { Provider: Provider<T>; Consumer: Consumer<T>; displayName?: string }
function createContext<T>(defaultValue: T): Context<T>

// Exotic components
const Suspense: ExoticComponent<SuspenseProps>
const Profiler: ExoticComponent<ProfilerProps>
const StrictMode: ExoticComponent<{ children?: ReactNode }>
const Fragment: ExoticComponent<{ children?: ReactNode }>

// Activity (React 19.2+, index.d.ts L1986-2006)
const Activity: ExoticComponent<ActivityProps>
interface ActivityProps { mode?: "hidden" | "visible"; name?: string; children: ReactNode }

// Top-level type utilities
type ElementType<P = any> = { [K in Tag]: P extends IntrinsicElements[K] ? K : never }[Tag] | ComponentType<P>
type ComponentType<P = {}> = ComponentClass<P> | FunctionComponent<P>
type JSXElementConstructor<P> = ((props: P) => ReactNode | Promise<ReactNode>) | (new(props: P) => Component<any>)
type ContextType<C extends Context<any>> = C extends Context<infer T> ? T : never
interface ReactPortal extends ReactElement { children: ReactNode }

// ReactPromise status tracking (index.d.ts L1938-1960)
interface PendingReactPromise<T> extends PromiseLike<T> { status: "pending" }
interface FulfilledReactPromise<T> extends PromiseLike<T> { status: "fulfilled"; value: T }
interface RejectedReactPromise<T> extends PromiseLike<T> { status: "rejected"; reason: unknown }
type ReactPromise<T> = UntrackedReactPromise<T> | PendingReactPromise<T> | FulfilledReactPromise<T> | RejectedReactPromise<T>
```

## [Core_Hooks]
```ts
// State (index.d.ts L1689-1697)
function useState<S>(initialState: S | (() => S)): [S, Dispatch<SetStateAction<S>>]
function useState<S = undefined>(): [S | undefined, Dispatch<SetStateAction<S | undefined>>]

// Reducer (index.d.ts L1708-1726)
function useReducer<S, A extends AnyActionArg>(reducer: (prev: S, ...args: A) => S, initialState: S): [S, ActionDispatch<A>]
function useReducer<S, I, A extends AnyActionArg>(reducer: (prev: S, ...args: A) => S, initialArg: I, init: (i: I) => S): [S, ActionDispatch<A>]

// Effects (index.d.ts L1775-1791)
function useEffect(effect: EffectCallback, deps?: DependencyList): void
function useLayoutEffect(effect: EffectCallback, deps?: DependencyList): void
function useInsertionEffect(effect: EffectCallback, deps?: DependencyList): void  // CSS-in-JS
function useEffectEvent<T extends Function>(callback: T): T  // React 19.2

// Refs (index.d.ts L1737-1761)
function useRef<T>(initialValue: T): RefObject<T>
function useRef<T>(initialValue: T | null): RefObject<T | null>
function useImperativeHandle<T, R extends T>(ref: Ref<T> | undefined, init: () => R, deps?: DependencyList): void

// Context
function useContext<T>(context: Context<T>): T

// Memoization (index.d.ts L1813-1821)
function useCallback<T extends Function>(callback: T, deps: DependencyList): T
function useMemo<T>(factory: () => T, deps: DependencyList): T

// Transitions (index.d.ts L1861-1885)
function useTransition(): [boolean, TransitionStartFunction]
function useDeferredValue<T>(value: T, initialValue?: T): T
function startTransition(scope: TransitionFunction): void

// React 19 hooks
function useId(): string
function useOptimistic<State>(passthrough: State): [State, (action: State | ((pending: State) => State)) => void]
function useOptimistic<State, Action>(passthrough: State, reducer: (state: State, action: Action) => State): [State, (action: Action) => void]

// useActionState (index.d.ts L1966-1975) — React 19 form actions
function useActionState<State>(action: (state: Awaited<State>) => State | Promise<State>, initialState: Awaited<State>, permalink?: string): [state: Awaited<State>, dispatch: () => void, isPending: boolean]
function useActionState<State, Payload>(action: (state: Awaited<State>, payload: Payload) => State | Promise<State>, initialState: Awaited<State>, permalink?: string): [state: Awaited<State>, dispatch: (payload: Payload) => void, isPending: boolean]

// use() hook (index.d.ts L1962-1964) — React 19
type Usable<T> = ReactPromise<T> | Context<T>
function use<T>(usable: Usable<T>): T

// External store (index.d.ts L1924-1928)
function useSyncExternalStore<Snapshot>(subscribe: (onStoreChange: () => void) => () => void, getSnapshot: () => Snapshot, getServerSnapshot?: () => Snapshot): Snapshot

// Debug
function useDebugValue<T>(value: T, format?: (value: T) => any): void

// Cache (index.d.ts L1978)
function cache<CachedFunction extends Function>(fn: CachedFunction): CachedFunction
function cacheSignal(): null | CacheSignal  // React 19.2: abort signal for cached computations
```

## [Event_System]
```ts
// Base (index.d.ts L2020-2036)
interface BaseSyntheticEvent<E = object, C = any, T = any> {
  nativeEvent: E; currentTarget: C; target: T
  bubbles: boolean; cancelable: boolean; defaultPrevented: boolean
  eventPhase: number; isTrusted: boolean; timeStamp: number; type: string
  preventDefault(): void; stopPropagation(): void; persist(): void
  isDefaultPrevented(): boolean; isPropagationStopped(): boolean
}
interface SyntheticEvent<T = Element, E = Event> extends BaseSyntheticEvent<E, EventTarget & T, EventTarget> {}

// Typed events (index.d.ts L2047-2216)
MouseEvent<T>      // button, clientX/Y, pageX/Y, screenX/Y, altKey, ctrlKey, metaKey, shiftKey
KeyboardEvent<T>   // key, code, charCode, keyCode, altKey, ctrlKey, metaKey, repeat
ChangeEvent<T>     // target: EventTarget & T
InputEvent<T>      // data: string
FocusEvent<T>      // relatedTarget
SubmitEvent<T>     // target: EventTarget & HTMLFormElement
DragEvent<T>       // dataTransfer: DataTransfer
PointerEvent<T>    // pointerId, pressure, pointerType: "mouse"|"pen"|"touch"
TouchEvent<T>      // touches, targetTouches, changedTouches
WheelEvent<T>      // deltaX, deltaY, deltaZ, deltaMode
AnimationEvent<T>  // animationName, elapsedTime, pseudoElement
TransitionEvent<T> // propertyName, elapsedTime, pseudoElement
ClipboardEvent<T>  // clipboardData: DataTransfer
ToggleEvent<T>     // oldState, newState: "closed"|"open" (React 19.2+)

// Handler types (index.d.ts L2222-2249)
type EventHandler<E> = (event: E) => void
type MouseEventHandler<T = Element> = EventHandler<MouseEvent<T>>
type KeyboardEventHandler<T = Element> = EventHandler<KeyboardEvent<T>>
type ChangeEventHandler<T = Element> = EventHandler<ChangeEvent<T>>
type SubmitEventHandler<T = Element> = EventHandler<SubmitEvent<T>>
type FocusEventHandler<T = Element> = EventHandler<FocusEvent<T>>
type PointerEventHandler<T = Element> = EventHandler<PointerEvent<T>>
type ToggleEventHandler<T = Element> = EventHandler<ToggleEvent<T>>
```

## [Architectural_Laws]
- **Export_Law**: One component per file. Co-locate hooks with components. Extract shared hooks to `hooks/` directory with `use` prefix. Props as `type` not `interface` for union flexibility.
- **Transformation_Law**: Server Components render on server (default in React 19). Client Components must be marked `"use client"`. Props flow down, events flow up. State colocation principle: keep state as close to where it's used as possible.
- **Propagation_Law**: Use Error Boundaries (`componentDidCatch` / `getDerivedStateFromError`) for component-level error handling. Use Suspense boundaries for async loading states. Errors in event handlers are NOT caught by Error Boundaries.

## [Syntax_Rules] | [Naming_Conventions]
- PascalCase: components, types, interfaces
- camelCase: hooks (`useState`, `useFetch`), event handlers (`handleClick`, `onSubmit`)
- `use` prefix: mandatory for all hooks
- `handle` prefix: event handler implementations
- `on` prefix: event handler props
- `.tsx` extension for JSX files

## [Prohibited_Patterns]
- NO `useEffect` for data fetching — use `use()`, Suspense, or framework data loading
- NO direct DOM manipulation — use refs only for imperative focus/scroll/measure
- NO `forceUpdate()` in function components — restructure state
- NO index as key in dynamic lists — use stable unique identifiers
- NO state mutation — always return new references
- NO conditional hooks — hooks must be called in same order every render
- NO `useEffect` to sync props to state — derive during render

## [Deprecated_Definitions]
```ts
// @deprecated Class component lifecycle (index.d.ts L1264-1357)
componentWillMount?(): void                    // use componentDidMount or constructor
UNSAFE_componentWillMount?(): void
componentWillReceiveProps?(nextProps): void     // use getDerivedStateFromProps
UNSAFE_componentWillReceiveProps?(nextProps): void
componentWillUpdate?(nextProps, nextState): void // use getSnapshotBeforeUpdate
UNSAFE_componentWillUpdate?(nextProps, nextState): void

// @deprecated Component types
interface ClassicComponent<P, S> extends Component<P, S>  // use functional components
interface ClassicComponentClass<P> extends ComponentClass<P>

// @deprecated Ref types
interface MutableRefObject<T> { current: T }   // use RefObject<T> instead

// @deprecated FormEvent (index.d.ts L2077-2083)
interface FormEvent<T = Element>               // use ChangeEvent, InputEvent, or SubmitEvent

// @deprecated PropTypes (removed from React, exists as separate package)
static propTypes?: any                         // use TypeScript types instead

// @deprecated PropsWithRef — just an alias for Props
type PropsWithRef<Props> = Props

// @deprecated captureOwnerStack — dev-only (React 19.1+)
function captureOwnerStack(): string | null
```

## [Standard_Library_Signatures]
```ts
// Component utilities
forwardRef<T, P = {}>(render: ForwardRefRenderFunction<T, PropsWithoutRef<P>>): ForwardRefExoticComponent<PropsWithoutRef<P> & RefAttributes<T>>
memo<P extends object>(Component: FC<P>, propsAreEqual?: (prev: Readonly<P>, next: Readonly<P>) => boolean): NamedExoticComponent<P>
lazy<T extends ComponentType<any>>(load: () => Promise<{ default: T }>): LazyExoticComponent<T>
createRef<T>(): RefObject<T | null>

// Element creation (index.d.ts L457-537)
createElement(type: string | FunctionComponent | ComponentClass, props?: object | null, ...children: ReactNode[]): ReactElement
cloneElement(element: ReactElement, props?: object, ...children: ReactNode[]): ReactElement
isValidElement<P>(object: {} | null | undefined): object is ReactElement<P>

// Children API (index.d.ts L724-733)
Children.map<T, C>(children: C, fn: (child: C, index: number) => T): Array<T>
Children.forEach<C>(children: C, fn: (child: C, index: number) => void): void
Children.count(children: any): number
Children.only<C>(children: C): C
Children.toArray(children: ReactNode): Array<ReactNode>

// Testing
act(callback: () => void): void
act<T>(callback: () => T | Promise<T>): Promise<T>

// Type utilities
ComponentProps<T>              // extract props from component or intrinsic element
ComponentPropsWithRef<T>       // includes ref
ComponentPropsWithoutRef<T>    // excludes ref
ComponentRef<T>                // ref type for component
PropsWithChildren<P>           // P & { children?: ReactNode }
CSSProperties                 // CSS style object type

// JSX namespace (jsx-runtime.d.ts)
namespace JSX {
  type Element = ReactElement<any, any>
  interface IntrinsicElements { div: DetailedHTMLProps<HTMLAttributes<HTMLDivElement>, HTMLDivElement>; ... }
}
```

## [Tactical_Patterns]
### Server Components (React 19)
- **Async Components**: `async function Page() { const data = await fetch(...); return <div>{data}</div> }` — no `useEffect` needed.
- **"use client" Boundary**: Mark client components explicitly. Server Components are default.
- **"use server" Actions**: Mark server functions for form actions: `async function submit(formData: FormData) { "use server"; ... }`.
- **use() Hook**: `const data = use(promise)` — unwrap promises/context inside render. Works with Suspense.

### Form Actions (React 19)
- **useActionState**: `const [state, dispatch, isPending] = useActionState(action, initialState)` — progressive enhancement.
- **useOptimistic**: `const [optimistic, addOptimistic] = useOptimistic(state)` — optimistic UI updates before server confirms.
- **Form action prop**: `<form action={serverAction}>` — native form submission with server actions.

### Performance Patterns
- **Transition Updates**: `const [isPending, startTransition] = useTransition()` — mark non-urgent updates.
- **Deferred Values**: `const deferred = useDeferredValue(value)` — deprioritize expensive re-renders.
- **Memoization**: `memo()` for components, `useMemo()` for values, `useCallback()` for functions.
- **Lazy Loading**: `const LazyComponent = lazy(() => import('./Component'))` — code splitting.

### Ref Patterns (React 19)
- **Ref Cleanup**: `ref={(node) => { setup(node); return () => cleanup(node) }}` — callback refs can return cleanup.
- **Ref as Prop**: Function components accept `ref` directly in props (no `forwardRef` needed in React 19).

### Context Patterns (React 19)
- **Direct Provider**: `<ThemeContext value="dark">` — Context itself is the Provider (no `.Provider` needed).
