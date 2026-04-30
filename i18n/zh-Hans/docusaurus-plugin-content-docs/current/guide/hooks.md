---
sidebar_position: 6
title: Hooks
---

# Hooks

`@vef-framework-react/hooks` 不是“杂项工具箱”，它主要补的是页面层会高频遇到、但又不适合塞进组件或 store 的能力。

## 最值得优先掌握的 hooks

| Hook | 解决什么问题 |
| --- | --- |
| `useDictionaryQuery` | 从应用上下文的数据字典函数拉选项 |
| `useDataOptionsQuery` | 把任意列表数据转换为统一选项结构 |
| `useCheckPermission` | 拿到一个可复用的权限判断函数 |
| `useIsAuthorized` | 直接判断当前权限是否满足 |
| `useAuthorizedItems` | 过滤带权限要求的配置项 |
| `useHasFetching` | 判断某类 query 是否还在加载 |
| `useHasMutating` | 判断某类 mutation 是否还在执行 |

## `useDictionaryQuery`

只要你在 `createApp().render()` 里提供了 `appContext.dictionaryQueryFn`，就可以用别名映射的方式拉字典，每个别名对应解析后的一段数据:

```tsx
const { data, isFetching } = useDictionaryQuery({
  gender: "common.gender",
  status: "user.status"
});

// 在请求成功之前，data 是 undefined。
const genderOptions = data?.gender ?? [];
```

注意:

- `useDictionaryQuery(keys, options?)` 返回原生的 `UseQueryResult<TData>`，请求成功之前 `data` 是 `undefined`。
- `options.enabled` 用来推迟请求，比如上游参数还没准备好的时候。
- `options.select` 可以把字典别名映射再加工一次。它的引用会被透传给 React Query，所以请用模块作用域、`as const`、`useMemo` 或 `useCallback` 把 `keys` 和 `select` 稳住，避免每次渲染都重置 memoization。
- 普通下拉场景优先用 `useDictionaryOptionsSelect`——它在 `useDictionaryQuery` 之上再封了一层，按别名直接吐 `SelectProps`，可以直接展开到 `Select` 上。

## `useDataOptionsQuery`

当后端返回的不是 `label/value` 标准结构时，用这个 hook 统一转换最省事。

```tsx
const roleOptions = useDataOptionsQuery({
  queryOptions: {
    queryKey: [findRoleOptions.key],
    queryFn: findRoleOptions
  },
  labelKey: "name",
  valueKey: "id"
});
```

它会返回:

- `options`
- 查询状态字段
- 原始 query 的其它结果能力

## 权限相关 hooks

### `useCheckPermission`

```tsx
const checkPermission = useCheckPermission();

if (checkPermission("sys:user:create")) {
  // ...
}
```

### `useIsAuthorized`

```tsx
const canEdit = useIsAuthorized(["sys:user:update", "sys:user:write"], "any");
```

### `useAuthorizedItems`

特别适合菜单、按钮配置、操作列表这类“先声明数组，再按权限过滤”的场景。

```tsx
const visibleActions = useAuthorizedItems([
  { key: "create", permTokens: "sys:user:create" },
  { key: "delete", permTokens: "sys:user:delete" }
]);
```

## 加载状态 hooks

### `useHasFetching`

```tsx
const isUserPageFetching = useHasFetching(findUserPage.key, searchParams);
```

### `useHasMutating`

```tsx
const isCreatingUser = useHasMutating(createUser.key);
```

这两个 hook 很适合:

- 页面级 loading 联动
- 按钮禁用态
- 避免重复提交

## 其它常用导出

`@vef-framework-react/hooks` 还整理并复导出了不少来自 Mantine、AI SDK、热键库的能力，常见的包括:

- `useDebouncedValue`
- `useElementSize`
- `useDocumentTitle`
- `useInterval`
- `useMediaQuery`
- `useHotkeys`
- `useChat`

它们的价值主要在于: 你可以统一从框架层拿，而不必在业务项目里自己散装组织依赖入口。
