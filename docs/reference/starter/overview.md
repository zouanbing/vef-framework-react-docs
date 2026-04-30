---
sidebar_position: 1
title: Starter Package Overview
---

# Starter Package Overview

`@vef-framework-react/starter` is the package that turns VEF into a complete application shell.

It mainly covers three areas:

1. application bootstrap
2. routing and layouts
3. application shell components (root app, layouts, login, status pages)

Page-level containers, form dialogs, tables, and the CRUD stack are documented under [Components / Pages, Form Containers, and CRUD](../components/page-and-crud.md).

## Suggested Reading Order

1. [Bootstrap and Routing](./bootstrap-and-routing.md)
2. [Application Shell](./application-shell.md)
3. [Stores, Constants, and Types](./stores-and-types.md)

## Common Exports

- `createApp`
- `createApiClient`
- `createRouter`
- `createRootRouteOptions`
- `createLayoutRouteOptions`
- `App`
- `Layout` / `BaseLayout`
- `Login`
- `RouterProvider`
- `ThemeConfigProvider`
- `setupAppVersionNotification`
