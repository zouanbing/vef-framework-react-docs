---
sidebar_position: 5
title: Pages, Form Containers, and CRUD
---

# Pages, Form Containers, and CRUD

Page containers, form-driven dialogs, table abstractions, and the CRUD stack all live in `@vef-framework-react/components`. They used to be exported from `starter`; in current versions they have been consolidated here.

## `Page`

Primary container for regular business pages.

Recommended for:

- monitoring pages
- settings pages
- dashboards
- left / right split panels

Key props:

| Prop | Type | Purpose |
| --- | --- | --- |
| `margin` | `boolean` | enable page-level margin |
| `gap` | `Length` | spacing between main areas |
| `leftAside` / `rightAside` | `ReactNode` | left and right side panels |
| `leftAsideWidth` / `rightAsideWidth` | `AsideWidth` | side width or resizable config |
| `header` / `footer` | `ReactNode` | header and footer slots |
| `headerPosition` / `footerPosition` | `"inside" \| "outside"` | header/footer placement |
| `scrollable` | `boolean` | whether the content area scrolls |
| `scrollMargin` | `boolean` | auto pad the scroll area |

Related export: `useViewportHeight`.

## `FlexCard`

A semantic card-style container, useful for split layouts such as list + detail or tree + form.

## `FormModal`

Combines `Modal`, form state, mutation behavior, and submit actions.

Recommended for:

- standard create / edit dialogs
- form dialogs that benefit from a unified default footer

Key props:

| Prop | Type | Purpose |
| --- | --- | --- |
| `open` | `boolean` | controls visibility |
| `title` | `ReactNode` | modal title |
| `width` | `ModalProps["width"]` | modal width |
| `draggable` | `boolean` | enable dragging |
| `defaultValues` | `TValues` | initial form values |
| `mutationFn` | `MutationFunction` | submit mutation |
| `renderActions` | `(formApi) => ReactNode` | custom footer area |
| `beforeSubmit` / `afterSubmit` | callbacks | submit lifecycle hooks |

## `FormDrawer`

Same form pattern as `FormModal`, but inside a drawer.

Key props mirror `FormModal` plus:

| Prop | Type | Purpose |
| --- | --- | --- |
| `placement` | `DrawerProps["placement"]` | drawer placement |
| `resizable` | `boolean` | allow drawer resizing |
| `width` | `Length` | drawer width |

## `ProSearch`

Search-form container for:

- basic search area
- advanced search area
- search and reset actions

Key props:

| Prop | Type | Purpose |
| --- | --- | --- |
| `defaultValues` | `TValues` | initial search values |
| `basicSearch` | `ReactNode` | basic search area |
| `advancedSearch` | `ReactNode` | advanced search area |
| `extra` | `ReactNode` | left-side extra content |
| `onSearch` | `(values) => void` | search callback |
| `onReset` | `(defaultValues) => void` | reset callback |
| `defaultAdvancedSearchVisible` | `boolean` | initial advanced visibility |
| `advancedSearchVisible` | `boolean` | controlled advanced visibility |

## `ProTable`

Page-level table abstraction with support for:

- query functions
- pagination
- row selection
- column settings
- operation columns
- header and footer slots

Related exports:

- `ProTableSubscriber`
- `OperationButtonGroup`
- `ParamsWithPagination`
- `ParamsWithSort`
- `RowSelectionConfig`
- `ProTableRef`
- `ProTableState`

## `Crud`

Combines `ProSearch`, `ProTable`, scene forms, and delete-related mutations into one CRUD state model.

## `CrudPage`

The standard page-level CRUD abstraction, built from `Page + Crud`.

Behavior notes:

- after `delete` or `deleteMany` succeed, `CrudPage` clears the internal selection state automatically — toolbar buttons that depend on `selectedRows` will re-disable on their own
- the `renderForm(scene, defaults)` and per-scene action renderers receive a `defaults` argument exposing the framework's default `submitButton` / `resetButton` so that custom action layouts can keep the standard buttons when needed

Key props:

| Prop | Type | Purpose |
| --- | --- | --- |
| `tableColumns` | `Array<TableColumn<TRow>>` | table columns |
| `queryFn` | `QueryFunction` | list query |
| `basicSearch` / `advancedSearch` | `ReactNode` | search areas |
| `renderForm` | `(scene) => ReactNode` | scene-driven form rendering |
| `formMutationFns` | `CrudFormMutationFns` | submit functions per scene |
| `renderFormActions` | `CrudFormActionsRenderers` | optional per-scene action renderers, receive `(formApi, defaults)` |
| `deleteMutationFn` | `MutationFunction` | single-row delete |
| `deleteManyMutationFn` | `MutationFunction` | batch delete |
| `toolbarActions` | `ReactNode` | toolbar slot |
| `operationColumn` | `OperationColumnConfig` | row action column |
| `sceneDefaultFormValues` | `PartialDeep<TSceneFormValues>` | defaults per scene |
| `formMode` | `"modal" \| "drawer"` | form container mode |
| `formDrawerConfig` | `CrudFormDrawerConfig` | drawer-specific overrides |

## `createCrudKit`

Fixes a page's `TRow`, `TSearchValues`, and `TSceneFormValues` generics into a reusable local toolkit.

Returned helpers:

| Helper | Purpose |
| --- | --- |
| `useCrudStore` | read CRUD-internal state |
| `useSearchValues` | read current search values |
| `useSelectedRows` | read currently selected rows |
| `ActionButtonGroup` | toolbar-level button group |
| `OperationButtonGroup` | row-level operation button group |

## CRUD Types

| Type | Purpose |
| --- | --- |
| `CrudBasicFormScene` | basic scene literal (`"create" \| "update"`) |
| `CrudFormScene` | scene key type |
| `CrudBasicSceneFormValues` | basic scene values map |
| `CrudFormMutationFns` | submit-fn map per scene |
| `CrudFormActionsRenderers` | action renderer map per scene |
| `CrudFormMode` / `CrudFormDrawerConfig` | form container mode / drawer config |
| `CrudProps` / `CrudPageProps` | CRUD component props |
| `CrudKit` | return type of `createCrudKit()` |
