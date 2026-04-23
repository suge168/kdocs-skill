# 筛选

## 1. sheet.get_filters

#### 功能说明

获取工作表当前的筛选配置。

适用于在更新筛选条件前先读取现有范围和筛选列规则。


> 若工作表尚未开启筛选，返回内容可能为空或不包含筛选列配置

#### 调用示例

查询当前筛选配置：

```json
{
  "file_id": "string",
  "worksheet_id": 7
}
```


#### 参数说明

- `file_id` (string, 必填): 文件 ID
- `worksheet_id` (integer, 必填): 工作表 ID

#### 返回值说明

```json
{
  "range": {
    "row_from": 0,
    "row_to": 100,
    "col_from": 0,
    "col_to": 5
  },
  "filters": [
    {
      "col": 2,
      "condition": {
        "values": ["进行中"]
      }
    }
  ]
}

```

| 字段 | 类型 | 说明 |
|------|------|------|
| `range` | object | 当前筛选区域 |
| `filters` | array | 按列配置的筛选条件 |


---

## 2. sheet.open_filters

#### 功能说明

为指定工作表开启筛选功能，并设置筛选范围。

适用于把某块数据区域转成可按列筛选的表格区域。


> 一般建议把首行作为表头，并确保筛选区域完整覆盖数据块

#### 调用示例

为表头区域开启筛选：

```json
{
  "file_id": "string",
  "worksheet_id": 7,
  "expand_filter_range": true,
  "range": {
    "row_from": 0,
    "row_to": 100,
    "col_from": 0,
    "col_to": 5
  }
}
```


#### 参数说明

- `file_id` (string, 必填): 文件 ID
- `worksheet_id` (integer, 必填): 工作表 ID
- `expand_filter_range` (boolean, 必填): 是否自动扩展筛选范围
- `range` (object, 必填): 筛选区域范围

#### 返回值说明

```json
{}

```


---

## 3. sheet.update_filters

#### 功能说明

更新工作表某一列的筛选条件。

适用于按枚举值、文本或其他条件动态收窄当前筛选结果。


> 调用前需已开启筛选；若未开启，请先用 `sheet.open_filters`

#### 调用示例

按状态列筛选：

```json
{
  "file_id": "string",
  "worksheet_id": 7,
  "col": 2,
  "condition": {
    "values": [
      "进行中"
    ]
  }
}
```


#### 参数说明

- `file_id` (string, 必填): 文件 ID
- `worksheet_id` (integer, 必填): 工作表 ID
- `col` (integer, 必填): 列索引，从 0 开始
- `condition` (object, 必填): 筛选条件对象

`condition` 为透传对象，推荐先通过 `sheet.get_filters` 获取现有筛选结构，再按相同格式更新目标列条件。


#### 返回值说明

```json
{}

```


---

## 4. sheet.delete_filters

#### 功能说明

删除工作表当前的筛选配置。

删除后将移除整个筛选状态和筛选范围。


> 删除前建议先用 `sheet.get_filters` 确认当前工作表确实已启用筛选

#### 调用示例

删除当前筛选：

```json
{
  "file_id": "string",
  "worksheet_id": 7
}
```


#### 参数说明

- `file_id` (string, 必填): 文件 ID
- `worksheet_id` (integer, 必填): 工作表 ID

#### 返回值说明

```json
{}

```


---

