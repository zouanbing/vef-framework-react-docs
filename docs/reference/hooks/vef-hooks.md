---
sidebar_position: 2
title: VEF Hooks
---

# VEF Hooks

## `useAuthorizedItems`

Filters config arrays by permission metadata.

## `useBreakpoints`

Returns breakpoint state from a custom breakpoint configuration.

## `useCheckPermission`

Returns a reusable function for imperative permission checks.

## `useDictionaryQuery`

Fetches data-dictionary options through `appContext.dictionaryQueryFn` using an alias map.

Signature: `useDictionaryQuery(keys, options?) => UseQueryResult<TData>`.

Key behaviors:

- `keys` is an alias map such as `{ gender: "common.gender" }`; each alias becomes a key in the resolved `data`.
- `data` follows React Query semantics — it is `undefined` until the query resolves.
- `options.enabled` defers fetching.
- `options.select` reshapes the resolved alias map. Stabilize `keys` and `select` references to avoid invalidating React Query's `select` memoization on each render.

For typical select usage prefer `useDictionaryOptionsSelect`, which wraps this hook and produces ready-to-spread `SelectProps`.

## `useDataOptionsQuery`

Transforms query or dictionary data into normalized option structures, including pinyin-enhanced variants when needed.

## Deep / Shallow Comparison Hooks

These hooks help when dependency arrays contain objects or arrays and default shallow reference checks are not enough:

- `useDeepCallback`
- `useDeepCompare`
- `useDeepEffect`
- `useDeepIsomorphicEffect`
- `useDeepLayoutEffect`
- `useDeepMemo`
- `useShallowCallback`
- `useShallowCompare`
- `useShallowEffect`
- `useShallowIsomorphicEffect`
- `useShallowLayoutEffect`
- `useShallowMemo`

## Event and Environment Hooks

Representative hooks in this group:

- `useDocumentEvent`
- `useEmitterEvent`
- `useLatest`
- `useRafState`
- `useSingleton`
- `useViewportSize`

## Query and Mutation State Hooks

- `useHasFetching`
- `useHasMutating`

These are especially useful for page-level loading coordination and disabling repeated actions while requests are running.
