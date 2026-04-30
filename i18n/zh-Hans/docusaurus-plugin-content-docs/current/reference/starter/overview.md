---
sidebar_position: 1
title: Starter 包概览
---

# Starter 包概览

`@vef-framework-react/starter` 是把 VEF 真正“拼成一个应用”的那层包。

它主要负责三件事:

1. 应用启动
2. 路由与布局
3. 应用壳层组件（根组件、布局、登录、路由状态页）

页面级容器、表单弹窗、表格与 CRUD 体系请参见 [组件 / 页面、表单容器与 CRUD](../components/page-and-crud.md)。

> **注意（v2.1.6）：** `Page`、`FlexCard`、`FormModal`、`FormDrawer`、`ProSearch`、`ProTable`、`Crud`、`CrudPage` 和 `createCrudKit` 已从 `starter` 迁移到 `@vef-framework-react/components`。

1. [应用启动与路由](./bootstrap-and-routing.md)
2. [应用壳层](./application-shell.md)
3. [Store、常量与类型](./stores-and-types.md)

## 常用导出

| 导出 | 用途 |
| --- | --- |
| `createApp` | 启动应用 |
| `createApiClient` | 创建应用级 API 客户端 |
| `createRouter` | 创建路由实例 |
| `createRootRouteOptions` | 根路由 |
| `createLayoutRouteOptions` | 布局和守卫 |
| `App` | 应用根组件 |
| `Layout` / `BaseLayout` | 应用壳层布局 |
| `Login` | 内置登录页 |
| `RouterProvider` | 路由 Provider |
| `ThemeConfigProvider` | 主题 Provider |
| `setupAppVersionNotification` | 应用版本检查与通知 |
