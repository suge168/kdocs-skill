# 多维表格（dbt）工具完整参考文档

本文件包含金山文档 Skill 多维表格的操作说明。

---

## 一、数据表管理

### 1. dbsheet.get_schema — 获取文档结构（表/字段/视图）
> 详见 [dbsheet.get_schema 完整参考](dbsheet/data_table.md)

### 2. dbsheet.create_sheet — 创建数据表
> 详见 [dbsheet.create_sheet 完整参考](dbsheet/data_table.md)

### 3. dbsheet.update_sheet — 修改数据表名称
> 详见 [dbsheet.update_sheet 完整参考](dbsheet/data_table.md)

### 4. dbsheet.delete_sheet — 删除数据表
> 详见 [dbsheet.delete_sheet 完整参考](dbsheet/data_table.md)

## 二、视图管理

### 5. dbsheet.create_view — 创建视图
> 详见 [dbsheet.create_view 完整参考](dbsheet/view.md)

### 6. dbsheet.update_view — 更新视图配置
> 详见 [dbsheet.update_view 完整参考](dbsheet/view.md)

### 7. dbsheet.delete_view — 删除视图
> 详见 [dbsheet.delete_view 完整参考](dbsheet/view.md)

## 三、字段管理

### 8. dbsheet.create_fields — 批量创建字段
> 详见 [dbsheet.create_fields 完整参考](dbsheet/field.md)

### 9. dbsheet.update_fields — 批量更新字段
> 详见 [dbsheet.update_fields 完整参考](dbsheet/field.md)

### 10. dbsheet.delete_fields — 批量删除字段
> 详见 [dbsheet.delete_fields 完整参考](dbsheet/field.md)

## 四、记录操作

### 11. dbsheet.create_records — 批量创建记录
> 详见 [dbsheet.create_records 完整参考](dbsheet/record.md)

### 12. dbsheet.update_records — 批量更新记录
> 详见 [dbsheet.update_records 完整参考](dbsheet/record.md)

### 13. dbsheet.list_records — 分页遍历记录（支持筛选）
> 详见 [dbsheet.list_records 完整参考](dbsheet/record.md)

### 14. dbsheet.get_record — 获取单条记录
> 详见 [dbsheet.get_record 完整参考](dbsheet/record.md)

### 15. dbsheet.delete_records — 批量删除记录
> 详见 [dbsheet.delete_records 完整参考](dbsheet/record.md)

## 五、Webhook 与开放协作

### 16. dbsheet.list_webhooks — 查询全部 Hook 订阅
> 详见 [dbsheet.list_webhooks 完整参考](dbsheet/list_webhooks.md)

### 17. dbsheet.create_webhook — 创建 Hook 订阅
> 详见 [dbsheet.create_webhook 完整参考](dbsheet/list_webhooks.md)

### 18. dbsheet.delete_webhook — 取消 Hook 订阅
> 详见 [dbsheet.delete_webhook 完整参考](dbsheet/list_webhooks.md)

## 六、分享视图

### 19. dbsheet.share_open_view — 打开分享视图
> 详见 [dbsheet.share_open_view 完整参考](dbsheet/share_open_view.md)

### 20. dbsheet.share_view_status — 查询视图是否已开启分享
> 详见 [dbsheet.share_view_status 完整参考](dbsheet/share_open_view.md)

### 21. dbsheet.share_get_link_info — 查询分享链接信息
> 详见 [dbsheet.share_get_link_info 完整参考](dbsheet/share_open_view.md)

### 22. dbsheet.share_close_view — 关闭分享视图
> 详见 [dbsheet.share_close_view 完整参考](dbsheet/share_open_view.md)

### 23. dbsheet.share_get_repeatable — 查询表单是否可重复提交
> 详见 [dbsheet.share_get_repeatable 完整参考](dbsheet/share_open_view.md)

### 24. dbsheet.share_set_repeatable — 设置表单是否可重复提交
> 详见 [dbsheet.share_set_repeatable 完整参考](dbsheet/share_open_view.md)

### 25. dbsheet.share_update_permission — 修改分享权限
> 详见 [dbsheet.share_update_permission 完整参考](dbsheet/share_open_view.md)

## 七、父子记录

### 26. dbsheet.parent_disable — 禁用父子关系（仅前端）
> 详见 [dbsheet.parent_disable 完整参考](dbsheet/parent_disable.md)

### 27. dbsheet.parent_enable — 启用父子关系（仅前端）
> 详见 [dbsheet.parent_enable 完整参考](dbsheet/parent_disable.md)

### 28. dbsheet.parent_status — 查询父子关系是否禁用
> 详见 [dbsheet.parent_status 完整参考](dbsheet/parent_disable.md)

### 29. dbsheet.parent_bind_children — 绑定父子记录
> 详见 [dbsheet.parent_bind_children 完整参考](dbsheet/parent_disable.md)

### 30. dbsheet.parent_list_children — 查询子记录列表
> 详见 [dbsheet.parent_list_children 完整参考](dbsheet/parent_disable.md)

### 31. dbsheet.parent_unbind_children — 解绑父子记录
> 详见 [dbsheet.parent_unbind_children 完整参考](dbsheet/parent_disable.md)

## 八、表单视图

### 32. dbsheet.form_list_fields — 列出表单问题
> 详见 [dbsheet.form_list_fields 完整参考](dbsheet/form_list_fields.md)

### 33. dbsheet.form_update_field — 更新表单问题
> 详见 [dbsheet.form_update_field 完整参考](dbsheet/form_list_fields.md)

### 34. dbsheet.form_get_meta — 获取表单元数据
> 详见 [dbsheet.form_get_meta 完整参考](dbsheet/form_list_fields.md)

### 35. dbsheet.form_update_meta — 更新表单元数据
> 详见 [dbsheet.form_update_meta 完整参考](dbsheet/form_list_fields.md)

## 九、仪表盘

### 36. dbsheet.dashboard_copy — 复制仪表盘
> 详见 [dbsheet.dashboard_copy 完整参考](dbsheet/dashboard_copy.md)

### 37. dbsheet.dashboard_list — 列出仪表盘
> 详见 [dbsheet.dashboard_list 完整参考](dbsheet/dashboard_copy.md)

## 十、数据表批量

### 38. dbsheet.sheet_batch_create — 批量创建工作表
> 详见 [dbsheet.sheet_batch_create 完整参考](dbsheet/sheet_batch_create.md)

### 39. dbsheet.sheet_batch_delete — 批量删除工作表
> 详见 [dbsheet.sheet_batch_delete 完整参考](dbsheet/sheet_batch_create.md)

## 11、视图查询

### 40. dbsheet.views_list — 列出视图
> 详见 [dbsheet.views_list 完整参考](dbsheet/views_list.md)

### 41. dbsheet.views_get — 获取单个视图
> 详见 [dbsheet.views_get 完整参考](dbsheet/views_list.md)

## 12、记录（Open 直链）

### 42. dbsheet.records_list — 列举记录（Open 直链）
> 详见 [dbsheet.records_list 完整参考](dbsheet/records_list.md)

### 43. dbsheet.records_search — 检索多条记录（Open）
> 详见 [dbsheet.records_search 完整参考](dbsheet/records_list.md)

## 13、高级权限

### 44. dbsheet.permission_list_roles — 列举自定义角色
> 详见 [dbsheet.permission_list_roles 完整参考](dbsheet/permission_list_roles.md)

### 45. dbsheet.permission_query_task — 获取异步任务结果
> 详见 [dbsheet.permission_query_task 完整参考](dbsheet/permission_list_roles.md)

### 46. dbsheet.permission_create_roles_async — 新增自定义角色（异步）
> 详见 [dbsheet.permission_create_roles_async 完整参考](dbsheet/permission_list_roles.md)

### 47. dbsheet.permission_update_roles_async — 更新自定义角色（异步）
> 详见 [dbsheet.permission_update_roles_async 完整参考](dbsheet/permission_list_roles.md)

### 48. dbsheet.permission_delete_roles_async — 删除自定义角色（异步）
> 详见 [dbsheet.permission_delete_roles_async 完整参考](dbsheet/permission_list_roles.md)

### 49. dbsheet.permission_list_subjects — 列举成员（内容权限）
> 详见 [dbsheet.permission_list_subjects 完整参考](dbsheet/permission_list_roles.md)

### 50. dbsheet.permission_subjects_batch_add — 批量添加成员
> 详见 [dbsheet.permission_subjects_batch_add 完整参考](dbsheet/permission_list_roles.md)

### 51. dbsheet.permission_subjects_batch_change — 批量更改成员权限
> 详见 [dbsheet.permission_subjects_batch_change 完整参考](dbsheet/permission_list_roles.md)

### 52. dbsheet.permission_subjects_batch_remove — 批量删除成员
> 详见 [dbsheet.permission_subjects_batch_remove 完整参考](dbsheet/permission_list_roles.md)

## 工具速查表

| # | 工具名 | 分类 | 功能 | 必填参数 |
|---|--------|------|------|----------|
| 1 | `dbsheet.get_schema` | 数据表管理 | 获取文档结构（表/字段/视图） | `file_id` |
| 2 | `dbsheet.create_sheet` | 数据表管理 | 创建数据表 | `file_id`, `name` |
| 3 | `dbsheet.update_sheet` | 数据表管理 | 修改数据表名称 | `file_id`, `sheet_id` |
| 4 | `dbsheet.delete_sheet` | 数据表管理 | 删除数据表 | `file_id`, `sheet_id` |
| 5 | `dbsheet.create_view` | 视图管理 | 创建视图 | `file_id`, `sheet_id`, `name`, `type` |
| 6 | `dbsheet.update_view` | 视图管理 | 更新视图配置 | `file_id`, `sheet_id`, `view_id` |
| 7 | `dbsheet.delete_view` | 视图管理 | 删除视图 | `file_id`, `sheet_id`, `view_id` |
| 8 | `dbsheet.create_fields` | 字段管理 | 批量创建字段 | `file_id`, `sheet_id`, `fields` |
| 9 | `dbsheet.update_fields` | 字段管理 | 批量更新字段 | `file_id`, `sheet_id`, `fields` |
| 10 | `dbsheet.delete_fields` | 字段管理 | 批量删除字段 | `file_id`, `sheet_id`, `fields` |
| 11 | `dbsheet.create_records` | 记录操作 | 批量创建记录 | `file_id`, `sheet_id`, `records` |
| 12 | `dbsheet.update_records` | 记录操作 | 批量更新记录 | `file_id`, `sheet_id`, `records` |
| 13 | `dbsheet.list_records` | 记录操作 | 分页遍历记录（支持筛选） | `file_id`, `sheet_id` |
| 14 | `dbsheet.get_record` | 记录操作 | 获取单条记录 | `file_id`, `sheet_id`, `record_id` |
| 15 | `dbsheet.delete_records` | 记录操作 | 批量删除记录 | `file_id`, `sheet_id`, `records` |
| 16 | `dbsheet.list_webhooks` | Webhook 与开放协作 | 查询全部 Hook 订阅 | `file_id` |
| 17 | `dbsheet.create_webhook` | Webhook 与开放协作 | 创建 Hook 订阅 | `file_id`, `body` |
| 18 | `dbsheet.delete_webhook` | Webhook 与开放协作 | 取消 Hook 订阅 | `file_id`, `hook_id` |
| 19 | `dbsheet.share_open_view` | 分享视图 | 打开分享视图 | `file_id`, `sheet_id`, `view_id`, `body` |
| 20 | `dbsheet.share_view_status` | 分享视图 | 查询视图是否已开启分享 | `file_id`, `sheet_id`, `view_id` |
| 21 | `dbsheet.share_get_link_info` | 分享视图 | 查询分享链接信息 | `file_id`, `sheet_id`, `view_id`, `share_id` |
| 22 | `dbsheet.share_close_view` | 分享视图 | 关闭分享视图 | `file_id`, `sheet_id`, `view_id`, `share_id` |
| 23 | `dbsheet.share_get_repeatable` | 分享视图 | 查询表单是否可重复提交 | `file_id`, `sheet_id`, `view_id`, `share_id` |
| 24 | `dbsheet.share_set_repeatable` | 分享视图 | 设置表单是否可重复提交 | `file_id`, `sheet_id`, `view_id`, `share_id`, `body` |
| 25 | `dbsheet.share_update_permission` | 分享视图 | 修改分享权限 | `file_id`, `sheet_id`, `view_id`, `share_id`, `body` |
| 26 | `dbsheet.parent_disable` | 父子记录 | 禁用父子关系（仅前端） | `file_id`, `sheet_id` |
| 27 | `dbsheet.parent_enable` | 父子记录 | 启用父子关系（仅前端） | `file_id`, `sheet_id` |
| 28 | `dbsheet.parent_status` | 父子记录 | 查询父子关系是否禁用 | `file_id`, `sheet_id` |
| 29 | `dbsheet.parent_bind_children` | 父子记录 | 绑定父子记录 | `file_id`, `sheet_id`, `parent_id`, `body` |
| 30 | `dbsheet.parent_list_children` | 父子记录 | 查询子记录列表 | `file_id`, `sheet_id`, `parent_id` |
| 31 | `dbsheet.parent_unbind_children` | 父子记录 | 解绑父子记录 | `file_id`, `sheet_id`, `parent_id`, `body` |
| 32 | `dbsheet.form_list_fields` | 表单视图 | 列出表单问题 | `file_id`, `sheet_id`, `view_id` |
| 33 | `dbsheet.form_update_field` | 表单视图 | 更新表单问题 | `file_id`, `sheet_id`, `view_id`, `field_id`, `body` |
| 34 | `dbsheet.form_get_meta` | 表单视图 | 获取表单元数据 | `file_id`, `sheet_id`, `view_id` |
| 35 | `dbsheet.form_update_meta` | 表单视图 | 更新表单元数据 | `file_id`, `sheet_id`, `view_id`, `body` |
| 36 | `dbsheet.dashboard_copy` | 仪表盘 | 复制仪表盘 | `file_id`, `dashboard_id`, `body` |
| 37 | `dbsheet.dashboard_list` | 仪表盘 | 列出仪表盘 | `file_id` |
| 38 | `dbsheet.sheet_batch_create` | 数据表批量 | 批量创建工作表 | `file_id`, `body` |
| 39 | `dbsheet.sheet_batch_delete` | 数据表批量 | 批量删除工作表 | `file_id`, `body` |
| 40 | `dbsheet.views_list` | 视图查询 | 列出视图 | `file_id`, `sheet_id` |
| 41 | `dbsheet.views_get` | 视图查询 | 获取单个视图 | `file_id`, `sheet_id`, `view_id` |
| 42 | `dbsheet.records_list` | 记录（Open 直链） | 列举记录（Open 直链） | `file_id`, `sheet_id` |
| 43 | `dbsheet.records_search` | 记录（Open 直链） | 检索多条记录（Open） | `file_id`, `sheet_id`, `body` |
| 44 | `dbsheet.permission_list_roles` | 高级权限 | 列举自定义角色 | `file_id` |
| 45 | `dbsheet.permission_query_task` | 高级权限 | 获取异步任务结果 | `file_id`, `task_id`, `task_type` |
| 46 | `dbsheet.permission_create_roles_async` | 高级权限 | 新增自定义角色（异步） | `file_id`, `body` |
| 47 | `dbsheet.permission_update_roles_async` | 高级权限 | 更新自定义角色（异步） | `file_id`, `body` |
| 48 | `dbsheet.permission_delete_roles_async` | 高级权限 | 删除自定义角色（异步） | `file_id`, `body` |
| 49 | `dbsheet.permission_list_subjects` | 高级权限 | 列举成员（内容权限） | `file_id`, `cloud_permission_id`, `permission_type` |
| 50 | `dbsheet.permission_subjects_batch_add` | 高级权限 | 批量添加成员 | `file_id`, `body` |
| 51 | `dbsheet.permission_subjects_batch_change` | 高级权限 | 批量更改成员权限 | `file_id`, `body` |
| 52 | `dbsheet.permission_subjects_batch_remove` | 高级权限 | 批量删除成员 | `file_id`, `body` |

## 工具组合速查

| 用户需求 | 推荐工具组合 |
|----------|-------------|
| 多维表格读结构/数据 | `dbsheet.get_schema` → `dbsheet.list_records` / `dbsheet.get_record` |
| 多维表格增删改 | `dbsheet.get_schema` → `dbsheet.create_records` / `dbsheet.update_records` / `dbsheet.delete_records`|

---

## 错误速查表

| 错误特征 | 原因 | 处理方式 |
|----------|------|----------|
| 多维表格读不到结构化数据 | 误用 `read_file_content` 作主读 | 改用 `dbsheet.get_schema`、`dbsheet.list_records` 等，见 `references/dbsheet_reference.md` |

---

## 附录

### 字段类型

| 类型 | 说明 |
|------|------|
| `SingleLineText` | 单行文本 |
| `MultiLineText` | 多行文本 |
| `Number` | 数值 |
| `Currency` | 货币 |
| `Percentage` | 百分比 |
| `Date` | 日期 |
| `Time` | 时间 |
| `Checkbox` | 复选框 |
| `SingleSelect` | 单选项 |
| `MultipleSelect` | 多选项 |
| `Rating` | 等级 |
| `Complete` | 进度条 |
| `Phone` | 电话 |
| `Email` | 电子邮箱 |
| `Url` | 超链接 |
| `Contact` | 联系人 |
| `Attachment` | 附件 |
| `Link` | 关联 |
| `Note` | 富文本 |
| `Address` | 地址 |
| `AutoNumber` | 编号（自动填充） |
| `CreatedBy` | 创建者（自动填充） |
| `CreatedTime` | 创建时间（自动填充） |
| `LastModifiedBy` | 最后修改者（自动填充） |
| `LastModifiedTime` | 最后修改时间（自动填充） |
| `Formula` | 公式（自动计算） |
| `Lookup` | 引用（自动计算） |

### 视图类型

| 类型 | 说明 |
|------|------|
| `Grid` | 表格视图 |
| `Kanban` | 看板视图 |
| `Gallery` | 画册视图 |
| `Form` | 表单视图 |
| `Gantt` | 甘特视图 |
| `Calendar` | 日历视图 |

### 筛选规则（filter op）

| 操作符 | 适用字段类型 | 说明 |
|--------|-------------|------|
| `Equals` | 通用 | 等于 |
| `NotEqu` | 通用 | 不等于 |
| `Greater` | 数值、日期 | 大于 |
| `GreaterEqu` | 数值、日期 | 大于等于 |
| `Less` | 数值、日期 | 小于 |
| `LessEqu` | 数值、日期 | 小于等于 |
| `BeginWith` | 文本 | 开头是 |
| `EndWith` | 文本 | 结尾是 |
| `Contains` | 文本 | 包含 |
| `NotContains` | 文本 | 不包含 |
| `Intersected` | 单选、多选 | 选项包含指定值 |
| `Empty` | 通用 | 为空（`values` 可省略） |
| `NotEmpty` | 通用 | 不为空（`values` 可省略） |

### 错误响应

| 情况 | 响应示例 |
|------|---------|
| 命令不支持 | `{"msg":"core not support","result":"unSupport"}` |
| 内核错误 | `{"errno":-1880935404,"msg":"Invalid request","result":"ExecuteFailed"}` |
| HTTP 状态非 200 | 请求本身失败，检查 `file_id` 是否正确及鉴权信息 |
