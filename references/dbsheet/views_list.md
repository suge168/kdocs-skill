# 视图查询

## 1. dbsheet.views_list

#### 功能说明


**必填 query**：无。



#### 调用示例

列出视图：

```json
{
  "file_id": "string",
  "sheet_id": 1
}
```


#### 参数说明

- `file_id` (string, 必填): 多维表格文件 ID
- `sheet_id` (integer, 必填): 数据表 ID

#### 返回值说明

```json
{
  "result": "ok",
  "detail": {}
}

```

| 字段 | 类型 | 说明 |
|------|------|------|
| `result` | string | ok 表示成功 |
| `detail` | object | views 列表 |


---

## 2. dbsheet.views_get

#### 功能说明


**必填 query**：无。



#### 调用示例

获取视图：

```json
{
  "file_id": "string",
  "sheet_id": 1,
  "view_id": "B"
}
```


#### 参数说明

- `file_id` (string, 必填): 多维表格文件 ID
- `sheet_id` (integer, 必填): 数据表 ID
- `view_id` (string, 必填): 视图 ID

#### 返回值说明

```json
{
  "result": "ok",
  "detail": {}
}

```

| 字段 | 类型 | 说明 |
|------|------|------|
| `result` | string | ok 表示成功 |
| `detail` | object | view 对象 |


---

