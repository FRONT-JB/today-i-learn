# React Hooks

**[Types](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L20)**

[mixed types?](https://medium.com/@2woongjae/typescript-%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%98-flow-%ED%83%90%ED%97%98%EA%B8%B0-3-literal-types-mixed-types-6ae5b29d1548)

```javascript
// Used to track hooks called during a render

type HookLogEntry = {
  primitive: string,
  stackError: Error,
  value: mixed,
  ...
};

let hookLog: Array<HookLogEntry> = [];

// Primitives

type BasicStateAction<S> = ((S) => S) | S;

type Dispatch<A> = (A) => void;

let primitiveStackCache: null | Map<string, Array<any>> = null;

type Hook = {
  memoizedState: any,
  next: Hook | null,
};

type BasicStateAction<S> = ((S) => S) | S;

function nextHook(): null | Hook {
  const hook = currentHook;
  if (hook !== null) {
    currentHook = hook.next;
  }
  return hook;
}

export type Dispatcher = {|
  getCacheSignal?: () => AbortSignal,
  getCacheForType?: <T>(resourceType: () => T) => T,
  readContext<T>(context: ReactContext<T>): T,
  useState<S>(initialState: (() => S) | S): [S, Dispatch<BasicStateAction<S>>],
  useReducer<S, I, A>(
    reducer: (S, A) => S,
    initialArg: I,
    init?: (I) => S
  ): [S, Dispatch<A>],
  useContext<T>(context: ReactContext<T>): T,
  useRef<T>(initialValue: T): {| current: T |},
  useEffect(
    create: () => (() => void) | void,
    deps: Array<mixed> | void | null
  ): void,
  useInsertionEffect(
    create: () => (() => void) | void,
    deps: Array<mixed> | void | null
  ): void,
  useLayoutEffect(
    create: () => (() => void) | void,
    deps: Array<mixed> | void | null
  ): void,
  useCallback<T>(callback: T, deps: Array<mixed> | void | null): T,
  useMemo<T>(nextCreate: () => T, deps: Array<mixed> | void | null): T,
  useImperativeHandle<T>(
    ref: {| current: T | null |} | ((inst: T | null) => mixed) | null | void,
    create: () => T,
    deps: Array<mixed> | void | null
  ): void,
  useDebugValue<T>(value: T, formatterFn: ?(value: T) => mixed): void,
  useDeferredValue<T>(value: T): T,
  useTransition(): [
    boolean,
    (callback: () => void, options?: StartTransitionOptions) => void
  ],
  useMutableSource<Source, Snapshot>(
    source: MutableSource<Source>,
    getSnapshot: MutableSourceGetSnapshotFn<Source, Snapshot>,
    subscribe: MutableSourceSubscribeFn<Source, Snapshot>
  ): Snapshot,
  useSyncExternalStore<T>(
    subscribe: (() => void) => () => void,
    getSnapshot: () => T,
    getServerSnapshot?: () => T
  ): T,
  useId(): string,
  useCacheRefresh?: () => <T>(?() => T, ?T) => void,

  unstable_isNewReconciler?: boolean,
|};
```

<br />

**[Dispatcher](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L24)**

```javascript
type BasicStateAction<S> = ((S) => S) | S;
type Dispatch<A> = (A) => void;

function resolveDispatcher() {
  const dispatcher = ReactCurrentDispatcher.current;
  if (__DEV__) {
    if (dispatcher === null) {
      console.error(
        "Invalid hook call. Hooks can only be called inside of the body of a function component. This could happen for" +
          " one of the following reasons:\n" +
          "1. You might have mismatching versions of React and the renderer (such as React DOM)\n" +
          "2. You might be breaking the Rules of Hooks\n" +
          "3. You might have more than one copy of React in the same app\n" +
          "See https://reactjs.org/link/invalid-hook-call for tips about how to debug and fix this problem."
      );
    }
  }
  // Will result in a null access error if accessed outside render phase. We
  // intentionally don't throw our own error because this is in a hot path.
  // Also helps ensure this is inlined.
  return ((dispatcher: any): Dispatcher);
}
```

<br />

[useState](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L80)

```javascript
export function useState<S>(
  initialState: (() => S) | S
): [S, Dispatch<BasicStateAction<S>>] {
  const dispatcher = resolveDispatcher();
  return dispatcher.useState(initialState);
}
```

[useReducer](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L86)

```javascript
export function useReducer<S, I, A>(
  reducer: (S, A) => S,
  initialArg: I,
  init?: (I) => S
): [S, Dispatch<A>] {
  const dispatcher = resolveDispatcher();
  return dispatcher.useReducer(reducer, initialArg, init);
}
```

[useRef](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L95)

```javascript
export function useRef<T>(initialValue: T): {| current: T |} {
  const dispatcher = resolveDispatcher();
  return dispatcher.useRef(initialValue);
}
```

[useEffect](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L100)

```javascript
export function useEffect(
  create: () => (() => void) | void,
  deps: Array<mixed> | void | null
): void {
  const dispatcher = resolveDispatcher();
  return dispatcher.useEffect(create, deps);
}
```

[useCallback](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L124)

```javascript
export function useCallback<T>(
  callback: T,
  deps: Array<mixed> | void | null
): T {
  const dispatcher = resolveDispatcher();
  return dispatcher.useCallback(callback, deps);
}
```

[useMemo](https://github.com/facebook/react/blob/832e2987e01aa357c3b2e551acae0682ca36fb14/packages/react/src/ReactHooks.js#L132)

```javascript
export function useMemo<T>(
  create: () => T,
  deps: Array<mixed> | void | null
): T {
  const dispatcher = resolveDispatcher();
  return dispatcher.useMemo(create, deps);
}
```
