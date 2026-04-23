# 表格文档/智能表格（xlsx & ksheet）工具完整参考文档

本文件包含金山文档 Skill 中表格相关工具的完整 API 说明、详细调用示例、参数说明和返回值说明。

**适用范围**：本文档中的所有 `sheet.*` 工具同时适用于 Excel（.xlsx）和智能表格（.ksheet）。

---

### 表格工具概述

表格工具专门用于操作金山文档中的在线表格，提供工作表信息的查询、范围数据的获取以及批量更新等功能。支持两种表格类型：

- **Excel（.xlsx）**：传统在线表格
- **智能表格（.ksheet）**：高级结构化表格

### 创建表格文件

#### 创建 Excel 文件

通过 `create_file` 创建，`name` 须带 `.xlsx` 后缀，`file_type` 设为 `file`：

```json
{
  "name": "销售数据表.xlsx",
  "file_type": "file",
  "parent_id": "folder_abc123"
}
```

#### 创建智能表格

通过 `sheet.create_airsheet_file` 创建，`.ksheet` 不要再走 `create_file`：

```json
{
  "type": "ksheet",
  "tname": "项目任务跟踪表.ksheet"
}
```

### Excel vs 智能表格（ksheet）对比

| 特性 | Excel | 智能表格 ksheet |
|------|-------|----------------|
| 数据组织 | 传统行列表格 | 结构化字段+记录 |
| 视图 | 单一表格视图 | 多视图（表格/看板/日历/甘特图等） |
| 字段类型 | 通用单元格 | 丰富字段类型（单选/多选/日期/附件/关联等） |
| 适用场景 | 数据计算、报表、财务报表 | 项目管理、CRM、任务跟踪、库存管理 |
| 工作表/数据接口 | 使用 `sheet.*` 工具 | **同样使用 `sheet.*` 工具** |

### 使用场景

#### Excel 适用场景

| 场景 | 说明 |
|------|------|
| 数据记录 | 销售数据、财务报表 |
| 数据分析 | 结构化数据的读取与处理 |
| 报表汇总 | 多维度数据汇总 |
| 公式计算 | 需要复杂公式和数据透视 |

#### 智能表格 适用场景

| 场景 | 说明 |
|------|------|
| 项目管理 | 任务分配、进度跟踪 |
| CRM 管理 | 客户信息、跟进记录 |
| 资产管理 | 库存台账、设备管理 |
| 审批台账 | 合同风险排查台账等 |

### 类型选择建议

- 需要公式计算、数据透视 → 选 **Excel**
- 需要多视图、字段管理、看板展示 → 选 **ksheet**
- 需要做任务管理/项目跟踪 → 选 **ksheet**
- 需要做财务报表 → 选 **Excel**

> **注意**：`ksheet` 文件创建需使用 `sheet.create_airsheet_file`；创建完成后，和 Excel 一样继续使用 `sheet.*` 接口做工作表管理与数据操作。

### 表格增强能力

除基础的工作表管理与区域读写外，智能表格（.ksheet）和普通Excel（.xlsx）还支持以下增强能力：

- **区域权限**：可通过 `sheet.list_protection_ranges`、`sheet.create_protection_ranges`、`sheet.update_protection_ranges`、`sheet.delete_protection_ranges` 管理指定区域的访问或编辑限制
- **数据校验**：可通过 `sheet.get_data_validations`、`sheet.create_data_validations`、`sheet.update_data_validations`、`sheet.delete_data_validations` 配置下拉选项和输入约束
- **条件格式**：可通过 `sheet.get_conditional_format_rules`、`sheet.create_conditional_format_rules`、`sheet.update_conditional_format_rules`、`sheet.delete_conditional_format_rules` 管理自动高亮和格式规则
- **浮动图片**：可通过 `sheet.list_float_images`、`sheet.get_float_image`、`sheet.create_float_images`、`sheet.update_float_images`、`sheet.delete_float_images` 管理工作表中的浮动图片
- **筛选与工作表编排**：可通过 `sheet.get_filters`、`sheet.open_filters`、`sheet.update_filters`、`sheet.delete_filters` 管理筛选状态，并通过 `sheet.copy_worksheet`、`sheet.update_worksheet` 复制、重命名或移动工作表

> **补充说明**：上述增强能力可同时面向智能表格（.ksheet）和普通 Excel（.xlsx）。

---

## 一、工作表管理

### 1. sheet.get_sheets_info — 获取工作表列表
> 详见 [sheet.get_sheets_info 完整参考](sheet/worksheet.md)

### 2. sheet.create_airsheet_file — 新建智能表格文件
> 详见 [sheet.create_airsheet_file 完整参考](sheet/worksheet.md)

### 3. sheet.add_sheet — 新增工作表
> 详见 [sheet.add_sheet 完整参考](sheet/worksheet.md)

### 4. sheet.copy_worksheet — 复制工作表
> 详见 [sheet.copy_worksheet 完整参考](sheet/worksheet.md)

### 5. sheet.update_worksheet — 更新工作表名称或位置
> 详见 [sheet.update_worksheet 完整参考](sheet/worksheet.md)

## 二、数据操作

### 6. sheet.get_range_data — 获取选区数据
> 详见 [sheet.get_range_data 完整参考](sheet/data.md)

### 7. sheet.update_range_data — 批量更新选区数据
> 详见 [sheet.update_range_data 完整参考](sheet/data.md)

## 三、区域权限

### 8. sheet.list_protection_ranges — 获取区域权限列表
> 详见 [sheet.list_protection_ranges 完整参考](sheet/protection_ranges.md)

### 9. sheet.create_protection_ranges — 创建区域权限
> 详见 [sheet.create_protection_ranges 完整参考](sheet/protection_ranges.md)

### 10. sheet.update_protection_ranges — 批量更新区域权限
> 详见 [sheet.update_protection_ranges 完整参考](sheet/protection_ranges.md)

### 11. sheet.delete_protection_ranges — 批量删除区域权限
> 详见 [sheet.delete_protection_ranges 完整参考](sheet/protection_ranges.md)

## 四、数据校验

### 12. sheet.get_data_validations — 获取数据校验规则
> 详见 [sheet.get_data_validations 完整参考](sheet/data_validations.md)

### 13. sheet.create_data_validations — 创建数据校验规则
> 详见 [sheet.create_data_validations 完整参考](sheet/data_validations.md)

### 14. sheet.update_data_validations — 更新数据校验规则
> 详见 [sheet.update_data_validations 完整参考](sheet/data_validations.md)

### 15. sheet.delete_data_validations — 删除数据校验规则
> 详见 [sheet.delete_data_validations 完整参考](sheet/data_validations.md)

## 五、条件格式

### 16. sheet.get_conditional_format_rules — 获取条件格式规则
> 详见 [sheet.get_conditional_format_rules 完整参考](sheet/conditional_format_rules.md)

### 17. sheet.create_conditional_format_rules — 创建条件格式规则
> 详见 [sheet.create_conditional_format_rules 完整参考](sheet/conditional_format_rules.md)

### 18. sheet.update_conditional_format_rules — 更新条件格式规则
> 详见 [sheet.update_conditional_format_rules 完整参考](sheet/conditional_format_rules.md)

### 19. sheet.delete_conditional_format_rules — 删除条件格式规则
> 详见 [sheet.delete_conditional_format_rules 完整参考](sheet/conditional_format_rules.md)

## 六、浮动图片

### 20. sheet.list_float_images — 查询浮动图片列表
> 详见 [sheet.list_float_images 完整参考](sheet/list_float_images.md)

### 21. sheet.get_float_image — 获取单张浮动图片详情
> 详见 [sheet.get_float_image 完整参考](sheet/list_float_images.md)

### 22. sheet.create_float_images — 创建浮动图片
> 详见 [sheet.create_float_images 完整参考](sheet/list_float_images.md)

### 23. sheet.update_float_images — 更新浮动图片位置或尺寸
> 详见 [sheet.update_float_images 完整参考](sheet/list_float_images.md)

### 24. sheet.delete_float_images — 删除浮动图片
> 详见 [sheet.delete_float_images 完整参考](sheet/list_float_images.md)

## 七、筛选

### 25. sheet.get_filters — 获取筛选条件
> 详见 [sheet.get_filters 完整参考](sheet/filters.md)

### 26. sheet.open_filters — 开启工作表筛选
> 详见 [sheet.open_filters 完整参考](sheet/filters.md)

### 27. sheet.update_filters — 更新列筛选条件
> 详见 [sheet.update_filters 完整参考](sheet/filters.md)

### 28. sheet.delete_filters — 删除工作表筛选
> 详见 [sheet.delete_filters 完整参考](sheet/filters.md)

## 工具速查表

| # | 工具名 | 分类 | 功能 | 必填参数 |
|---|--------|------|------|----------|
| 1 | `sheet.get_sheets_info` | 工作表管理 | 获取工作表列表 | `file_id` |
| 2 | `sheet.create_airsheet_file` | 工作表管理 | 新建智能表格文件 | `tname` |
| 3 | `sheet.add_sheet` | 工作表管理 | 新增工作表 | `file_id`, `position` |
| 4 | `sheet.get_range_data` | 数据操作 | 获取选区数据 | `file_id`, `sheetId`, `range` |
| 5 | `sheet.update_range_data` | 数据操作 | 批量更新选区数据 | `file_id`, `sheetId`, `rangeData` |
| 6 | `sheet.list_protection_ranges` | 区域权限 | 获取区域权限列表 | `file_id`, `worksheet_id` |
| 7 | `sheet.create_protection_ranges` | 区域权限 | 创建区域权限 | `file_id`, `sheets_protection_infos` |
| 8 | `sheet.update_protection_ranges` | 区域权限 | 批量更新区域权限 | `file_id`, `sheets_protection_infos` |
| 9 | `sheet.delete_protection_ranges` | 区域权限 | 批量删除区域权限 | `file_id`, `sheets_protection_infos` |
| 10 | `sheet.get_data_validations` | 数据校验 | 获取数据校验规则 | `file_id`, `worksheet_id`, `col_from`, `col_to`, `row_from`, `row_to` |
| 11 | `sheet.create_data_validations` | 数据校验 | 创建数据校验规则 | `file_id`, `worksheet_id`, `args`, `field_type`, `range` |
| 12 | `sheet.update_data_validations` | 数据校验 | 更新数据校验规则 | `file_id`, `worksheet_id`, `args`, `field_type`, `range` |
| 13 | `sheet.delete_data_validations` | 数据校验 | 删除数据校验规则 | `file_id`, `worksheet_id`, `range` |
| 14 | `sheet.get_conditional_format_rules` | 条件格式 | 获取条件格式规则 | `file_id`, `worksheet_id` |
| 15 | `sheet.create_conditional_format_rules` | 条件格式 | 创建条件格式规则 | `file_id`, `worksheet_id`, `rule` |
| 16 | `sheet.update_conditional_format_rules` | 条件格式 | 更新条件格式规则 | `file_id`, `worksheet_id`, `rule` |
| 17 | `sheet.delete_conditional_format_rules` | 条件格式 | 删除条件格式规则 | `file_id`, `worksheet_id`, `ranges` |
| 18 | `sheet.list_float_images` | 浮动图片 | 查询浮动图片列表 | `file_id`, `worksheet_id` |
| 19 | `sheet.get_float_image` | 浮动图片 | 获取单张浮动图片详情 | `file_id`, `worksheet_id`, `float_image_id` |
| 20 | `sheet.create_float_images` | 浮动图片 | 创建浮动图片 | `file_id`, `worksheet_id`, `sheet_id`, `tag`, `x_pos`, `y_pos` |
| 21 | `sheet.update_float_images` | 浮动图片 | 更新浮动图片位置或尺寸 | `file_id`, `worksheet_id`, `float_image_id` |
| 22 | `sheet.delete_float_images` | 浮动图片 | 删除浮动图片 | `file_id`, `worksheet_id`, `float_image_id` |
| 23 | `sheet.get_filters` | 筛选 | 获取筛选条件 | `file_id`, `worksheet_id` |
| 24 | `sheet.open_filters` | 筛选 | 开启工作表筛选 | `file_id`, `worksheet_id`, `expand_filter_range`, `range` |
| 25 | `sheet.update_filters` | 筛选 | 更新列筛选条件 | `file_id`, `worksheet_id`, `col`, `condition` |
| 26 | `sheet.delete_filters` | 筛选 | 删除工作表筛选 | `file_id`, `worksheet_id` |
| 27 | `sheet.copy_worksheet` | 工作表管理 | 复制工作表 | `file_id`, `worksheet_id` |
| 28 | `sheet.update_worksheet` | 工作表管理 | 更新工作表名称或位置 | `file_id`, `worksheet_id` |

## 工具组合速查

| 用户需求 | 推荐工具组合 |
|----------|-------------|
| 读表格（矩形区域） | `sheet.get_sheets_info` → `sheet.get_range_data` |
| 写表格（批量改单元格） | `sheet.get_range_data`（可选对照）→ `sheet.update_range_data` → `sheet.get_range_data` 验证 |
| 给某列配置下拉选项 | `sheet.get_data_validations`（可选）→ `sheet.create_data_validations` / `sheet.update_data_validations` |
| 管理条件格式高亮 | `sheet.get_conditional_format_rules` → `sheet.create_conditional_format_rules` / `sheet.update_conditional_format_rules` / `sheet.delete_conditional_format_rules` |
| 管理区域权限 | `sheet.list_protection_ranges` → `sheet.create_protection_ranges` / `sheet.update_protection_ranges` / `sheet.delete_protection_ranges` |
| 管理表格筛选 | `sheet.get_filters` → `sheet.open_filters` / `sheet.update_filters` / `sheet.delete_filters` |
| 插入并调整浮动图片 | `sheet.create_float_images` → `sheet.get_float_image` / `sheet.update_float_images` |

---

## 错误速查表

| 错误特征 | 原因 | 处理方式 |
|----------|------|----------|
| 表格读不到或结构不明 | 未先取工作表列表 / 区域错误 | 先 `sheet.get_sheets_info`，再 `sheet.get_range_data` |
| 智能表格增强配置不生效 | 使用了普通 Excel，或未先读取现有配置结构 | 确认文件为 `.ksheet`，并先调用对应的 `get/list` 工具查看当前结构 |

---

## 附录

### 错误响应

| 情况 | 响应示例 |
|------|---------|
| 命令不支持 | `{"msg":"core not support","result":"unSupport"}` |
| 内核错误 | `{"errno":-1880935404,"msg":"Invalid request","result":"ExecuteFailed"}` |
| HTTP 状态非 200 | 请求本身失败，检查鉴权信息（Cookie/Origin） |
