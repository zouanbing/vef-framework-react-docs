---
sidebar_position: 3
title: Application Shell
---

# Application Shell

These exports build the application shell — the part that wraps every route. Page-level containers (`Page`, `FlexCard`), form dialogs (`FormModal`, `FormDrawer`), table abstractions (`ProTable`), and the CRUD stack (`CrudPage`, `createCrudKit`, etc.) now live in `@vef-framework-react/components`. See [Components / Pages, Form Containers, and CRUD](../components/page-and-crud.md).

## `App`

The application root component that connects:

- `AppContextProvider`
- `ApiClientProvider`
- `MotionProvider`
- `ThemeConfigProvider`
- `RouterProvider`

In normal application code it is used through `createApp().render()` rather than instantiated directly.

## `BaseLayout` / `Layout`

Application-shell layout components, usually driven by the layout route (`createLayoutRouteOptions()`) instead of being rebuilt manually in page code.

`BaseLayout` is the lower-level shell. `Layout` adds the menu, user area, and tab system on top of it.

## `RouterProvider`

Injects the router and extended router context into the React tree. When the app is bootstrapped through `createApp()`, mounting it manually is not required.

## `ThemeConfigProvider`

Starter-level theme wrapper, normally used together with `App`.

## `Login`

Built-in login page component.

Recommended for:

- standard admin login pages
- avoiding rebuilding form, RSA encryption, and post-login redirect logic by hand

Key props:

| Prop | Type | Purpose |
| --- | --- | --- |
| `logo` | `ReactNode` | brand mark in the corner |
| `title` | `string` | page title |
| `description` | `string` | subtitle |
| `publicKey` | `string` | enables RSA password encryption when present |
| `onLogin` | `(params: LoginParams) => Promise<LoginResult>` | login callback |

## Routing Status Pages

| Export | Purpose |
| --- | --- |
| `AccessDenied` | rendered when the current user lacks permission |
| `Error` | route-level error page |
| `NotFound` | 404 page |

## Route Loading Indicator

| Export | Purpose |
| --- | --- |
| `NProgress` | top-edge progress bar component |
| `nProgressEventEmitter` | event hooks for custom progress integrations |
