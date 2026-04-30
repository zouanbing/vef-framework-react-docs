---
sidebar_position: 5
title: Store、常量与类型
---

# Store、常量与类型

## Store 导出

| 导出 | 用途 |
| --- | --- |
| `useAppStore` | 登录状态、菜单、权限点、用户信息等应用状态 |
| `useTabStore` | 标签页状态 |
| `useThemeStore` | 主题状态 |

对应类型:

| 类型 | 用途 |
| --- | --- |
| `AppState` | 应用 store 状态 |
| `Tab` / `TabState` | 标签页类型 |
| `ColorScheme` / `ThemeColors` / `ThemeState` | 主题状态类型 |

## 常量导出

| 常量 | 用途 |
| --- | --- |
| `RELOAD_PAGE_EVENT` | 刷新页面事件名 |
| `ACCESS_DENIED_EVENT` | 无权限事件名 |
| `UNAUTHENTICATED_EVENT` | 未认证事件名 |
| `STORAGE_KEY_PREFIX_STORE` / `STORAGE_KEY_SUFFIX_STORE` | store 存储 key 片段 |
| `SYMBOL_PAGINATION` | 分页参数内部 key |
| `SYMBOL_SORT` | 排序参数内部 key |

## API / 领域类型

实体身份:

| 类型 | 推荐场景 |
| --- | --- |
| `Entity<TId = string>` | 只携带 `id` 的基础实体接口 |

独立的审计字段接口（适合复合主键或非 `id` 主键的记录）:

| 类型 | 推荐场景 |
| --- | --- |
| `CreationTracked<TId, TDate>` | `createdAt` / `createdBy` / `createdByName` |
| `FullTracked<TId, TDate>` | 继承 `CreationTracked`，再加 `updatedAt` / `updatedBy` / `updatedByName` |

组合后的实体接口:

| 类型 | 推荐场景 |
| --- | --- |
| `CreationAuditedEntity<TId, TDate>` | `Entity` + `CreationTracked` |
| `FullAuditedEntity<TId, TDate>` | `Entity` + `FullTracked` |

批量参数辅助类型:

| 类型 | 推荐场景 |
| --- | --- |
| `Many<T>` | 包一层 `list: T[]`，用于批量新增/更新参数 |

## 用户和菜单类型

| 类型 | 推荐场景 |
| --- | --- |
| `Gender` | 用户性别枚举 |
| `UserMenuType` | 菜单节点类型 |
| `UserMenu` | 菜单树节点 |
| `UserInfo` | 当前登录用户，`details` 通过 `Register` 扩展点定型（见下） |
| `Register` | 空接口扩展点，项目通过 `declare module` 收紧 `UserInfo['details']` |
| `UserDetails` | 当 `Register` 未扩展时 `details` 的兜底类型（`Record<string, unknown>`） |
| `OrderSpec` | 排序字段描述 |

### 扩展 `UserInfo.details`

`UserInfo.details` 的具体形状通过 `Register` 接口解析，参考的是 `@tanstack/react-query` 给 `mutationMeta` 用的同款模式。在项目里声明一次，整个应用里 `UserInfo` 流经的地方就都能拿到强类型:

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

声明之后，`userInfo.details.department` 在整个应用里都会被推断成 `string`，无需 fork 框架。

## 路由类型

| 类型 | 推荐场景 |
| --- | --- |
| `RouterContext` | 根路由与 router 上下文类型 |

## 查询辅助

| 导出 | 用途 |
| --- | --- |
| `extractQueryParams` | 从查询对象里拆出业务参数、分页和排序 |
| `noopMutationFn` | 需要占位 mutation 时的空实现 |
