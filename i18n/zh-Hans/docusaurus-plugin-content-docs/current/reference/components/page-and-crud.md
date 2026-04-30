---
sidebar_position: 5
title: 页面、表单容器与 CRUD
---

# 页面、表单容器与 CRUD

页面容器、表单弹窗、表格抽象与 CRUD 体系如今都属于 `@vef-framework-react/components`。它们历史上来自 `starter`，目前已统一收敛到 `components`。

## `Page`

普通业务页首选容器。

推荐场景:

- 监控页
- 配置页
- 图表看板
- 左右侧栏布局页

关键 Props:

| Prop | 类型 | 说明 |
| --- | --- | --- |
| `margin` | `boolean` | 是否启用页面外边距 |
| `gap` | `Length` | 主区域间距 |
| `leftAside` / `rightAside` | `ReactNode` | 左右侧栏 |
| `leftAsideWidth` / `rightAsideWidth` | `AsideWidth` | 侧栏宽度或可拖拽配置 |
| `header` / `footer` | `ReactNode` | 页头页脚 |
| `headerPosition` / `footerPosition` | `"inside" \| "outside"` | 内外布局位置 |
| `scrollable` | `boolean` | 内容区是否滚动 |
| `scrollMargin` | `boolean` | 是否自动给滚动区补边距 |

相关导出: `useViewportHeight`。

## `FlexCard`

语义化的卡片容器，适合分栏卡片页和树表页。

## `FormModal`

把 Modal 与表单、mutation、提交按钮统一封装在一起。

推荐场景:

- 小中型新增/编辑弹窗
- 需要默认 footer 行为的表单弹窗

关键 Props:

| Prop | 类型 | 说明 |
| --- | --- | --- |
| `open` | `boolean` | 是否打开 |
| `title` | `ReactNode` | 标题 |
| `width` | `ModalProps["width"]` | 宽度 |
| `draggable` | `boolean` | 是否支持拖拽 |
| `defaultValues` | `TValues` | 默认值 |
| `mutationFn` | `MutationFunction` | 提交时执行的 mutation |
| `renderActions` | `(formApi) => ReactNode` | 自定义底部操作区 |
| `beforeSubmit` / `afterSubmit` | 回调 | 提交前后钩子 |

## `FormDrawer`

与 `FormModal` 语义相同，但承载容器是 Drawer。

在 `FormModal` 之外的关键 Props:

| Prop | 类型 | 说明 |
| --- | --- | --- |
| `placement` | `DrawerProps["placement"]` | 打开方向 |
| `resizable` | `boolean` | 是否可调整尺寸 |
| `width` | `Length` | 宽度 |

## `ProSearch`

搜索表单容器，负责基础搜索区、高级搜索区、搜索按钮和重置逻辑。

关键 Props:

| Prop | 类型 | 说明 |
| --- | --- | --- |
| `defaultValues` | `TValues` | 初始搜索值 |
| `basicSearch` | `ReactNode` | 基础搜索区域 |
| `advancedSearch` | `ReactNode` | 高级搜索区域 |
| `extra` | `ReactNode` | 左侧扩展内容 |
| `onSearch` | `(values) => void` | 搜索回调 |
| `onReset` | `(defaultValues) => void` | 重置回调 |
| `defaultAdvancedSearchVisible` | `boolean` | 默认展开高级搜索 |
| `advancedSearchVisible` | `boolean` | 受控展开状态 |

## `ProTable`

页面级表格容器，支持:

- 查询函数
- 分页或非分页模式
- 选中行状态
- 列显示设置
- 操作列
- header / footer 插槽

相关导出:

| 导出 | 用途 |
| --- | --- |
| `ProTableSubscriber` | 订阅表格内部状态 |
| `OperationButtonGroup` | 行级操作按钮组 |
| `ParamsWithPagination` | 分页参数类型 |
| `ParamsWithSort` | 排序参数类型 |
| `RowSelectionConfig` | 选中配置 |
| `ProTableRef` | 表格 ref 类型 |
| `ProTableState` | 表格内部状态类型 |

## `Crud`

在 `ProSearch`、`ProTable`、场景表单和删除 mutation 之上再包一层，提供一整套 CRUD 页面内部状态。

## `CrudPage`

`Page + Crud` 的组合页，是标准后台列表页首选。

行为说明:

- `delete` / `deleteMany` 成功后，`CrudPage` 会自动清空内部的选中行状态——依赖 `selectedRows` 的工具栏按钮会自行重新禁用
- `renderForm(scene, defaults)` 以及各场景的 action 渲染器会收到 `defaults` 参数，里面带着框架默认的 `submitButton` / `resetButton`；自定义 action 布局想保留默认按钮时直接用即可

关键 Props:

| Prop | 类型 | 说明 |
| --- | --- | --- |
| `tableColumns` | `Array<TableColumn<TRow>>` | 表格列 |
| `queryFn` | `QueryFunction` | 列表查询 |
| `basicSearch` / `advancedSearch` | `ReactNode` | 搜索区域 |
| `renderForm` | `(scene) => ReactNode` | 表单场景渲染 |
| `formMutationFns` | `CrudFormMutationFns` | 各场景提交函数 |
| `renderFormActions` | `CrudFormActionsRenderers` | 各场景的可选 action 渲染器，签名为 `(formApi, defaults)` |
| `deleteMutationFn` | `MutationFunction` | 单条删除 |
| `deleteManyMutationFn` | `MutationFunction` | 批量删除 |
| `toolbarActions` | `ReactNode` | 工具栏 |
| `operationColumn` | `OperationColumnConfig` | 行操作列 |
| `sceneDefaultFormValues` | `PartialDeep<TSceneFormValues>` | 各场景默认值 |
| `formMode` | `"modal" \| "drawer"` | 表单容器模式 |
| `formDrawerConfig` | `CrudFormDrawerConfig` | drawer 模式下的额外配置 |

## `createCrudKit`

把页面的 `TRow`、`TSearchValues`、`TSceneFormValues` 泛型固化成一组本地可复用工具。

返回值:

| 返回值 | 用途 |
| --- | --- |
| `useCrudStore` | 读取当前 CRUD 内部状态 |
| `useSearchValues` | 读取当前搜索值 |
| `useSelectedRows` | 读取当前选中行 |
| `ActionButtonGroup` | 工具栏级按钮组 |
| `OperationButtonGroup` | 行操作按钮组 |

## CRUD 类型导出

| 类型 | 用途 |
| --- | --- |
| `CrudBasicFormScene` | 基础场景字面量（`"create" \| "update"`） |
| `CrudFormScene` | 场景键类型 |
| `CrudBasicSceneFormValues` | 基础场景值映射 |
| `CrudFormMutationFns` | 各场景提交函数映射 |
| `CrudFormActionsRenderers` | 各场景 action 渲染器映射 |
| `CrudFormMode` / `CrudFormDrawerConfig` | 表单容器模式 / drawer 配置 |
| `CrudProps` / `CrudPageProps` | CRUD 组件 Props |
| `CrudKit` | `createCrudKit()` 返回类型 |
