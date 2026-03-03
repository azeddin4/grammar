---
Language: Framer Motion
Version: 12.4.7
Fidelity: 100% (Physical Disk Reference + Deep d.ts Analysis)
State_ID:  BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/framer-motion/package.json"
Grammar_Lock: "@root/hashes/grammar/framer-motion.hash.md"
---

/** [Project].Grammar.FramerMotion - Linguistic DNA anchor for Framer Motion */

## [SDK_Discovery_Map]
/** === framer-motion (Core) === */
/** @Ref: @root/node_modules/framer-motion/dist/types/index.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/types/client.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/dom.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/m.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/mini.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/dom-mini.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/projection.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/debug.d.ts */
/** @Ref: @root/node_modules/framer-motion/dist/types.d-CQ4vRM6h.d.ts */

## [SDK_Imports / Namespaces]
```ts
import { motion, AnimatePresence, useAnimation, useScroll, useTransform, useSpring, useMotionValue, useMotionValueEvent, useVelocity, useInView, useDragControls, MotionConfig, LazyMotion, domAnimation, domMax, m, Reorder } from "framer-motion"
// Standalone DOM API (non-React):
import { animate, animateMini, scroll, scrollInfo, inView, createScopedAnimate, distance, distance2D, stagger, type AnimationSequence } from "framer-motion/dom"
```

## [Core_Primitives]
```ts
// types.d-CQ4vRM6h.d.ts: Core motion props interface.
// MotionProps extends MotionNodeOptions — accepts MotionValues for ANY CSS/transform property.
interface MotionProps extends MotionNodeOptions {
  style?: MotionStyle;            // Enhanced CSS + transforms. Accepts MotionValue<T> for any property.
  children?: React.ReactNode | MotionValue<number> | MotionValue<string>;
  initial?: Target | VariantLabels | boolean;   // State on mount (false = inherit from parent).
  animate?: AnimationControls | Target | VariantLabels | boolean;
  exit?: Target | VariantLabels;                 // State when removed from AnimatePresence.
  transition?: Transition;                        // Spring/tween/inertia config.
  variants?: Variants;                            // Named state definitions for orchestration.
  whileHover?: Target | VariantLabels;
  whileTap?: Target | VariantLabels;
  whileDrag?: Target | VariantLabels;
  whileFocus?: Target | VariantLabels;
  whileInView?: Target | VariantLabels;
  layout?: boolean | "position" | "size" | "preserve-aspect";
  layoutId?: string;                              // Shared layout animation identifier.
  drag?: boolean | "x" | "y";
  dragConstraints?: RefObject<Element> | { top?: number; left?: number; right?: number; bottom?: number };
  dragElastic?: boolean | number | { top?: number; left?: number; right?: number; bottom?: number };
  dragMomentum?: boolean;
  onAnimationStart?: (definition: AnimationDefinition) => void;
  onAnimationComplete?: (definition: AnimationDefinition) => void;
  onDragStart?: (event: MouseEvent | TouchEvent, info: PanInfo) => void;
  onDrag?: (event: MouseEvent | TouchEvent, info: PanInfo) => void;
  onDragEnd?: (event: MouseEvent | TouchEvent, info: PanInfo) => void;
  onViewportEnter?: (entry: IntersectionObserverEntry) => void;
  onViewportLeave?: (entry: IntersectionObserverEntry) => void;
}

// MotionStyle: MakeMotion<CSSProperties> — every CSS property can accept a MotionValue.
// Transforms (x, y, z, rotate, scale, skew, perspective) are first-class props, NOT in style.transform.
interface MotionStyle extends MotionCSS, MotionTransform, MotionSVGProps {}

// VariantLabels: string | string[] — references to variant keys.
type VariantLabels = string | string[];

// PanInfo: Detailed gesture data for drag/pan handlers.
interface PanInfo {
  point: { x: number; y: number };
  delta: { x: number; y: number };
  offset: { x: number; y: number };
  velocity: { x: number; y: number };
}

// AnimatePresenceProps: Controls mount/unmount animation orchestration.
interface AnimatePresenceProps {
  mode?: "sync" | "popLayout" | "wait";  // sync = simultaneous, wait = sequential, popLayout = layout-aware.
  initial?: boolean;          // false = disable enter animations on initial mount.
  onExitComplete?: () => void;
  custom?: any;               // Passed to exit variants as second argument.
}

// ForwardRefComponent: The actual type of motion.div, motion.span, etc.
type ForwardRefComponent<T, P> = { readonly $$typeof: symbol } & ((props: P & RefAttributes<T>) => JSX.Element);

// HTMLMotionComponents: { [K in HTMLElements]: ForwardRefComponent<HTMLElements[K], HTMLMotionProps<K>> }
// SVGMotionComponents: { [K in SVGElements]: ForwardRefComponent<SVGElement, SVGMotionProps<SVGElement>> }
// SVG elements: animate, circle, defs, desc, ellipse, g, image, line, filter, marker, mask, path, pattern, polygon, polyline, rect, stop, svg, text, tspan, use, view, clipPath, feBlend, etc.
```

## [Architectural_Laws]
- **Projection_Rule**: Layout animations use "projection" (delta-based transforms). Set `layout` prop on `motion` components to enable. Projection corrects scale distortion on children automatically.
- **Tree_Shaking_Strategy**: Use `m` component with `LazyMotion` + `domAnimation` (lighter) or `domMax` (full features). The `motion` component includes ALL features — use only in apps where bundle size is not critical.
- **MotionValue_Identity**: `MotionValue` updates do NOT trigger React re-renders. They mutate the DOM directly. Use for high-frequency properties (scroll, drag, coordinates).
- **Variant_Propagation**: Parent variants automatically flow to children unless child explicitly defines its own `animate`. Children can reference parent variant labels in `variants` for staggered orchestration with `staggerChildren`, `delayChildren`.
- **AnimatePresence_Exit_Rule**: `AnimatePresence` must be the direct parent wrapping the conditional render. The child MUST have a unique `key` prop for exit detection.
- **Transform_Independence**: x, y, z, rotate, rotateX, rotateY, rotateZ, scale, scaleX, scaleY, skew, skewX, skewY, and perspective are independent props — NOT nested in `style.transform`.
- **Server_Rendering_Safety**: Initial animations use `initial` prop. On SSR, `initial` renders the starting state. Set `initial={false}` to skip mount animation.
- **Gesture_Hierarchy**: whileHover < whileTap < whileDrag — more specific gesture states override less specific ones.

## [Syntax_Rules] | [Naming_Conventions]
- `motion.tag`: Standard proxy for animated HTML/SVG elements (motion.div, motion.svg, motion.path, etc.).
- `m.tag`: Lightweight tree-shakeable alternative. Requires `LazyMotion` parent.
- `variants`: Object-based state definitions. Keys are state names, values are `Target` objects.
- `whileHover/whileTap/whileDrag/whileFocus/whileInView`: Inline gesture handlers.
- `layoutId`: String identifier for shared layout animation between components.
- `custom`: Dynamic value passed to variant functions for parameterized animations.
- `staggerChildren/delayChildren/staggerDirection`: Orchestration timing within variants.

## [Prohibited_Patterns]
- NO heavy logic inside `useTransform` callbacks — keep mapping functions pure and lightweight.
- NO `initial={false}` on `AnimatePresence` unless specifically disabling mount animations globally.
- NO `motion` component without `LazyMotion` when bundle size matters — use `m` instead.
- NO manual `style.transform` strings — use individual transform props (x, y, rotate, scale).
- NO `AnimatePresence` wrapping non-keyed children — each animated child needs a unique `key`.
- NO `useAnimation` for simple state-driven animations — prefer `animate` prop with variants.
- NO `MotionValue` in dependency arrays — they don't trigger re-renders, use `useMotionValueEvent`.

## [Standard_Library_Signatures]
```ts
// Hooks — MotionValue Primitives
function useMotionValue<T>(initial: T): MotionValue<T>;     // Creates a reactive animation value.
function useTransform<T, U>(value: MotionValue<T>, transformer: (v: T) => U): MotionValue<U>;
function useTransform<T>(value: MotionValue<number>, inputRange: number[], outputRange: T[]): MotionValue<T>;
function useSpring(source: MotionValue<number> | number, config?: SpringOptions): MotionValue<number>;
function useVelocity(value: MotionValue<number>): MotionValue<number>;  // Tracks velocity of a MotionValue.

// Hooks — Scroll & Viewport
function useScroll(options?: ScrollOptions): { scrollX: MotionValue<number>; scrollY: MotionValue<number>; scrollXProgress: MotionValue<number>; scrollYProgress: MotionValue<number> };
function useInView(ref: RefObject<Element>, options?: InViewOptions): boolean;

// Hooks — Control & Events
function useAnimation(): AnimationControls;  // Imperative control: controls.start("variant"), controls.stop().
function useMotionValueEvent<V, E>(value: MotionValue<V>, event: E, callback: (...) => void): void;
function useDragControls(): DragControls;    // Programmatic drag initiation.

// Transition Types
interface Transition {
  type?: "spring" | "tween" | "inertia" | "keyframes";
  duration?: number;          // Seconds (NOT milliseconds).
  delay?: number;             // Seconds.
  ease?: Easing | Easing[];   // "easeIn", "easeOut", "easeInOut", "linear", cubic-bezier array.
  stiffness?: number;         // Spring stiffness.
  damping?: number;           // Spring damping.
  mass?: number;              // Spring mass.
  bounce?: number;            // 0 = no bounce, 1 = full bounce.
  restDelta?: number;         // Pixel distance from target to "snap".
  repeat?: number;            // Repeat count. Infinity for infinite.
  repeatType?: "loop" | "reverse" | "mirror";
  repeatDelay?: number;
  when?: "beforeChildren" | "afterChildren";
  staggerChildren?: number;   // Delay between each child variant start (seconds).
  delayChildren?: number;     // Delay before children start (seconds).
}

// Utility Components
function AnimatePresence(props: AnimatePresenceProps): JSX.Element;
function MotionConfig(props: { transition?: Transition; reducedMotion?: "user" | "always" | "never" }): JSX.Element;
function LazyMotion(props: { features: FeatureBundle | (() => Promise<FeatureBundle>); strict?: boolean }): JSX.Element;

// Reorder Components
interface ReorderGroupProps<T> {
  values: T[];
  onReorder: (newValues: T[]) => void;
  axis?: "x" | "y";
  as?: string;
}
// Reorder.Group + Reorder.Item: Drag-to-reorder lists.

// === Standalone DOM API (from dom.d.ts — non-React, imperative) ===

// animate(): Imperative standalone animation. Works on DOM elements, MotionValues, or objects.
// animate(element, keyframes, options): Animate DOM elements directly.
// animate(motionValue, keyframes, options): Animate MotionValue instances.
// animate(sequence, options): Timeline-based animation sequence.
// animate(object, target, options): Animate plain JS objects.
// Returns AnimationPlaybackControlsWithThen (.then(), .stop(), .pause(), .play(), .time, .speed, .duration).
declare const animate: {
  (sequence: AnimationSequence, options?: SequenceOptions): AnimationPlaybackControlsWithThen;
  (element: ElementOrSelector, keyframes: DOMKeyframesDefinition, options?: AnimationOptions): AnimationPlaybackControlsWithThen;
  (value: MotionValue<number>, keyframes: number[], options?: ValueAnimationTransition<number>): AnimationPlaybackControlsWithThen;
  <O extends {}>(object: O, target: ObjectTarget<O>, options?: AnimationOptions): AnimationPlaybackControlsWithThen;
};

// animateMini(): Lightweight animation — smaller bundle. DOM elements only.
declare const animateMini: (element: ElementOrSelector, keyframes: DOMKeyframesDefinition, options?: AnimationOptions) => AnimationPlaybackControlsWithThen;

// AnimationSequence: Timeline-based orchestration with labels and relative timing.
type SequenceTime = number | "<" | `+${number}` | `-${number}` | `${string}`;
// "<" = start at same time as previous. "+0.5" = 0.5s after previous. "-0.2" = 0.2s before previous ends.
type Segment = DOMSegment | MotionValueSegment | ObjectSegment | SequenceLabel | FunctionSegment;
type AnimationSequence = Segment[];  // Array of [target, keyframes, options?] tuples + labels.
// Example: animate([["h1", { opacity: 1 }], ["p", { y: 0 }, { at: "<" }]], { duration: 1 })

// scroll(): Scroll-linked animation. Links animation progress to scroll position.
declare function scroll(onScroll: OnScroll | AnimationPlaybackControls, options?: ScrollOptions): VoidFunction;
// Usage: scroll(animate("h1", { opacity: [0, 1] }))  — links animation to page scroll.
// scroll((progress) => { ... }, { target: el, offset: ["start end", "end start"] })

// scrollInfo(): Raw scroll information without animation binding.
declare function scrollInfo(onScroll: OnScrollInfo, options?: ScrollInfoOptions): VoidFunction;

// inView(): Standalone intersection observer. Returns cleanup function.
declare function inView(
  elementOrSelector: ElementOrSelector,
  onStart: (element: Element, entry: IntersectionObserverEntry) => void | ViewChangeHandler,
  options?: InViewOptions
): VoidFunction;
// InViewOptions: { root, margin, amount: "some" | "all" | number }

// createScopedAnimate(): Factory for scoped animation functions (within AnimationScope).
declare function createScopedAnimate(options?: { scope?: AnimationScope; reduceMotion?: boolean }): typeof animate;

// Utility functions:
declare const distance: (a: number, b: number) => number;      // 1D distance between two numbers.
declare function distance2D(a: Point, b: Point): number;        // 2D Euclidean distance.
```

## [Tactical_Patterns]

### Layout Orchestration
- **Layout_Inheritance**: Variants propagate from parent to child. Override with explicit child `animate`.
- **Shared_Layout**: `layoutId` animates between two different component instances sharing an identity (e.g., tab indicator, card expand).
- **Presence_Exit**: `AnimatePresence` wraps the conditional render. Child needs unique `key`. Uses `exit` prop.
- **Stagger_Children**: Parent variant `transition: { staggerChildren: 0.1 }` staggers child animations sequentially.
- **Layout_Scroll_Correction**: `layoutScroll` on scrollable containers prevents scroll offset from breaking layout animations.

### Performance & Scoping
- **Motion_Values**: Use `useMotionValue` for high-frequency updates (cursor tracking, scroll parallax). Bypasses React render cycle entirely.
- **External_Controls**: `useAnimation()` for imperative start/stop. Useful for programmatic animation triggers (scroll events, API responses).
- **Reduce_Motion**: Always respect `reducedMotion` in `MotionConfig`. Set to `"always"` to force reduced, `"user"` (default) to follow OS setting.
- **GPU_Promotion**: x, y, scale, rotate use hardware-accelerated transforms. Prefer these over top/left/width/height for 60fps animations.
- **Will_Change**: framer-motion auto-applies `will-change` during animations. Do NOT manually set `will-change` on motion components.

### Animation Composition
- **Dynamic_Variants**: Use functions as variant values: `variants={{ active: (custom) => ({ x: custom * 100 }) }}`. Pass `custom` prop.
- **Keyframes**: Arrays in animate: `animate={{ x: [0, 100, 0] }}` creates multi-step keyframe animations.
- **Path_Drawing**: SVG `pathLength`, `pathOffset`, `pathSpacing` for reveal/draw effects on `motion.path`.
- **Spring_Physics**: Default animation type. `type: "spring"` with `stiffness`, `damping`, `mass` for natural motion. `type: "tween"` for CSS-like easing.

### Standalone DOM Animations (Non-React)
- **animate(element, keyframes, options)**: Directly animate DOM elements without React. `animate(".box", { opacity: 1 }, { duration: 0.5 })`.
- **Timeline Sequences**: `animate([["h1", { opacity: 1 }], ["p", { y: 0 }, { at: "<" }]])` — `"<"` means start simultaneously.
- **Scroll-Linked**: `scroll(animate(".progress", { scaleX: [0, 1] }))` — binds animation progress to scroll position.
- **Scroll Offsets**: `scroll(callback, { target: el, offset: ["start end", "end start"] })` — trigger between viewport intersections.
- **inView Detection**: `inView(".card", (el) => { animate(el, { opacity: 1 }); return () => { /* leave handler */ } })` — cleanup function pattern.
- **animateMini**: Smaller bundle alternative to `animate`. DOM elements only. No sequences or MotionValues.
- **Scoped Animations**: `const scopedAnimate = createScopedAnimate({ scope })` — animations scoped to a container element.
- **Stagger**: `animate("li", { opacity: 1 }, { delay: stagger(0.1) })` — stagger delay across multiple elements.
