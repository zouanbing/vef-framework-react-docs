---
sidebar_position: 5
title: Stores, Constants, and Types
---

# Stores, Constants, and Types

## Store Exports

- `useAppStore`
- `useTabStore`
- `useThemeStore`

Related types:

- `AppState`
- `Tab`
- `TabState`
- `ColorScheme`
- `ThemeColors`
- `ThemeState`

## Constants

- `RELOAD_PAGE_EVENT`
- `ACCESS_DENIED_EVENT`
- `UNAUTHENTICATED_EVENT`
- `STORAGE_KEY_PREFIX_STORE`
- `STORAGE_KEY_SUFFIX_STORE`
- `SYMBOL_PAGINATION`
- `SYMBOL_SORT`

## API and Domain Types

Entity identity:

- `Entity<TId = string>` — base interface that only carries `id`

Standalone audit field interfaces (use these for composite primary keys or non-`id` keyed records):

- `CreationTracked<TId, TDate>` — `createdAt` / `createdBy` / `createdByName`
- `FullTracked<TId, TDate>` — extends `CreationTracked` with `updatedAt` / `updatedBy` / `updatedByName`

Composed entity interfaces:

- `CreationAuditedEntity<TId, TDate>` — `Entity` + `CreationTracked`
- `FullAuditedEntity<TId, TDate>` — `Entity` + `FullTracked`

Batch parameter helper:

- `Many<T>` — wraps a `list: T[]` for batch create / update payloads

## User and Menu Types

- `Gender`
- `UserMenuType`
- `UserMenu`
- `UserInfo` — `details` is typed via the `Register` augmentation point (see below)
- `Register` — empty interface that projects augment via `declare module` to refine `UserInfo['details']`
- `UserDetails` — fallback shape (`Record<string, unknown>`) when `Register` is not augmented
- `OrderSpec`

### Extending `UserInfo.details`

`UserInfo.details` resolves through the `Register` interface, mirroring the pattern used by `@tanstack/react-query` for `mutationMeta`. Augment it once in your project to get strongly typed user attributes everywhere `UserInfo` flows through the app:

```ts
// src/types/vef-augment.d.ts
declare module "@vef-framework-react/starter" {
  interface Register {
    userDetails: {
      department: string;
      organization: string;
    };
  }
}
```

After this declaration, `userInfo.details.department` is typed as `string` across the application without forking the framework.

## Router Types

- `RouterContext`

## Query Helpers

- `extractQueryParams`
- `noopMutationFn`
