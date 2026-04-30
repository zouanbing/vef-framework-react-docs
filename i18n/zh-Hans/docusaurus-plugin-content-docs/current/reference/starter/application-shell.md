---
sidebar_position: 3
title: 应用壳层
---

# 应用壳层

这里集中介绍 starter 包里围绕“应用壳层”的导出——这些组件会包住每一个路由。页面级容器（`Page`、`FlexCard`）、表单弹窗（`FormModal`、`FormDrawer`）、表格抽象（`ProTable`）以及 CRUD 体系（`CrudPage`、`createCrudKit` 等）现在都属于 `@vef-framework-react/components`，见 [组件 / 页面、表单容器与 CRUD](../components/page-and-crud.md)。

## `App`

应用根组件。负责串起:

- `AppContextProvider`
- `ApiClientProvider`
- `MotionProvider`
- `ThemeConfigProvider`
- `RouterProvider`

你通常不直接手写它，而是通过 `createApp().render()` 使用。

## `BaseLayout` / `Layout`

应用壳层布局组件，通常由布局路由（`createLayoutRouteOptions()`）驱动，不建议在普通业务页手工直接重组。

`BaseLayout` 是较低一层的壳层，`Layout` 在它之上叠加了菜单、用户区与多 Tab 体系。

## `RouterProvider`

把 router 和扩展上下文注入 React 树。  
如果使用 `createApp()`，通常也不需要单独手动挂它。

## `ThemeConfigProvider`

starter 对应用主题层的进一步封装，通常和 `App` 一起工作。

## `Login`

框架内置登录页组件。

推荐场景:

- 标准后台登录页
- 不想自行重复搭登录表单、RSA 加密和登录后跳转逻辑

关键 Props:

| Prop | 类型 | 说明 |
| --- | --- | --- |
| `logo` | `ReactNode` | 左上角品牌图形 |
| `title` | `string` | 登录页标题 |
| `description` | `string` | 副标题 |
| `publicKey` | `string` | 开启 RSA 加密时使用 |
| `onLogin` | `(params: LoginParams) => Promise<LoginResult>` | 登录回调 |

## 路由状态页

| 导出 | 用途 |
| --- | --- |
| `AccessDenied` | 无权限页 |
| `Error` | 路由错误页 |
| `NotFound` | 404 页 |

## 路由进度条

| 导出 | 用途 |
| --- | --- |
| `NProgress` | 顶部进度条组件 |
| `nProgressEventEmitter` | 提供给自定义进度条集成的事件 |
