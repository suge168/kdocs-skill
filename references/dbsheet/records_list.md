# 记录（Open 直链）

## 1. dbsheet.records_list

#### 功能说明

对应开放平台「列举记录 list-record」能力：请求为 JSON 体（application/json）。网关路径不含 /list-record 段，与 SkillHub 直链一致。

**请求体（均在 JSON 内，无 URL query）**：下列名为 Skill 侧 snake_case；SkillHub 发往网关时会转为开放平台 JSON 所用 camelCase（如 `prefer_id`→`preferId`、`page_size`→`pageSize`）。

| 名称 | 类型 | 必填 | 说明 |
|------|------|------|------|
| fields | array[string] | 是* | 指定返回记录中的字段；*文档写必填，若不填则默认返回全部字段。`prefer_id=true` 时填字段 id，否则填字段名 |
| filter | object | 否 | 筛选条件 |
| filter.criteria | array[object] | 条件内必填 | 条件数组，结构见多维表格参数说明 |
| max_records | integer | 否 | 最多取前 max_records 条；不填则不限 |
| page_size | integer | 否 | 每页大小，默认 100，范围 1–1000 |
| page_token | string | 否 | 分页游标；有下一页时用上次的 page_token |
| prefer_id | boolean | 否 | 为 true 时 fields 等按字段 id 解析 |
| show_fields_info | boolean | 否 | 是否额外返回字段元信息（类似 Schema fields） |
| show_record_extra_info | boolean | 否 | 是否返回创建者、创建时间、最后修改者、最后修改时间等 |
| text_value | string | 否 | 不填默认 original；可选 original、text、compound |
| view_id | string | 否 | 指定视图则从该视图取用户可见记录；不填从工作表取 |

SkillHub：未传 `body` 或仅 `{}` 时合并默认 `prefer_id=false`、`show_fields_info=false`、`text_value=original`；可与顶层同名字段或整包 `body` 混用，**同键以 MCP 顶层为准**。

**与 `dbsheet.list_records` 区别**：本接口走 Open 网关直链；`list_records` 走 core/execute。日常读数优先 `list_records`。


> filter.criteria 的结构需符合多维表格开放接口对筛选条件的约定。
> 若在网关侧直接使用 JSON，请使用 camelCase 顶层字段名；经 SkillHub 调用时可用本 Skill 的 snake_case 参数。

#### 调用示例

最简（依赖 SkillHub 默认体）：

```json
{
  "file_id": "string",
  "sheet_id": 1,
  "body": {}
}
```

分页与视图：

```json
{
  "file_id": "string",
  "sheet_id": 1,
  "view_id": "B",
  "page_size": 50,
  "page_token": ""
}
```


#### 参数说明

- `file_id` (string, 必填): 多维表格文件 ID
- `sheet_id` (integer, 必填): 数据表 ID
- `body` (object, 可选): 可选整包请求体；与顶层字段混用时同键以顶层为准
- `fields` (array, 可选): 请求体 fields，不填则服务端返回全部列；prefer_id 决定用字段名或 id
- `filter` (object, 可选): 请求体 filter，内含 criteria 数组
- `max_records` (integer, 可选): 请求体 max_records
- `page_size` (integer, 可选): 请求体 page_size，默认 100，1–1000
- `page_token` (string, 可选): 请求体 page_token 分页游标
- `prefer_id` (boolean, 可选): 请求体 prefer_id
- `show_fields_info` (boolean, 可选): 请求体 show_fields_info
- `show_record_extra_info` (boolean, 可选): 请求体 show_record_extra_info
- `text_value` (string, 可选): 请求体 text_value：original / text / compound
- `view_id` (string, 可选): 请求体 view_id，按视图取数

所有列举参数均在 **POST JSON 请求体** 中，不拼 URL query。

**SkillHub 默认体**：`prefer_id=false`、`show_fields_info=false`、`text_value=original`。

若同时传 `body` 与顶层字段，同键以 **顶层** 为准。


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
| `detail` | object | 记录分页数据，结构以网关 data 为准 |


---

## 2. dbsheet.records_search

#### 功能说明


**前置条件**：对数据表有检索权限；`filter` 结构与操作符以接口约定为准。



#### 调用示例

最小检索：

```json
{
  "file_id": "string",
  "sheet_id": 1,
  "body": {
    "filter": {}
  }
}
```


#### 参数说明

- `file_id` (string, 必填): 多维表格文件 ID
- `sheet_id` (integer, 必填): 数据表 ID
- `body` (object, 必填): JSON 请求体，根级须含 filter

**body 根级必填（与 SkillHub 校验一致）**

| 字段 | 类型 | 说明 |
|------|------|------|
| `filter` | object | 筛选条件；内部字段（如 mode、criteria、字段 op 等）须抄录服务端「检索记录」文档 |

其它可与检索一并提交的字段（排序、分页等）以官方 POST body 为准。


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
| `detail` | object | 匹配记录集合 |


---

