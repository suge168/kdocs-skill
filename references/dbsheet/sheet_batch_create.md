# 数据表批量

## 1. dbsheet.sheet_batch_create

#### 功能说明


**前置条件**：有创建数据表权限；单次批量条数与字段结构以文档上限为准。



#### 操作约束

- **后置验证**：建议 dbsheet.get_schema 核对

#### 调用示例

批量建表：

```json
{
  "file_id": "string",
  "body": {
    "sheets": []
  }
}
```


#### 参数说明

- `file_id` (string, 必填): 多维表格文件 ID
- `body` (object, 必填): 须含 sheets 数组

**body 根级必填**

| 字段 | 类型 | 说明 |
|------|------|------|
| `sheets` | array | 每个元素描述一个待建数据表（名称、字段、视图等），子字段以接口约定为准（batch-create-sheet） |


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
| `detail` | object | 创建结果 |


---

## 2. dbsheet.sheet_batch_delete

#### 功能说明


**前置条件**：确认目标 `sheet_ids` 内数据均可删除；不可逆。



#### 操作约束

- **用户确认**：删除后表及记录不可恢复
- **幂等**：否

#### 调用示例

批量删除：

```json
{
  "file_id": "string",
  "body": {
    "sheet_ids": [
      2,
      3
    ]
  }
}
```


#### 参数说明

- `file_id` (string, 必填): 多维表格文件 ID
- `body` (object, 必填): 须含 sheet_ids

**body 根级必填**

| 字段 | 类型 | 说明 |
|------|------|------|
| `sheet_ids` | array[integer] | 待删除数据表 ID 列表 |


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
| `detail` | object | 接口返回详情 |


---

