# PDF 文档（pdf）工具完整参考文档

金山文档 PDF 工具适合处理"最终交付版"文档，包括查询页数、抽取指定页和格式转换。

---

## 通用说明

### PDF 文档特点

- **推荐度**：⭐⭐ 适合作为最终输出格式，不适合作为过程编辑格式
- PDF 适合作为最终分发、归档和打印格式，不适合高频在线编辑
- 如果目标是"持续编辑内容"，优先使用 `otl`、`docx`、`sheet`、`pptx`
- 如果目标是"输出最终版"、"归档"、"打印"或"扫描件整理"，优先考虑 PDF
- 常规创建或覆盖上传 PDF 时，使用通用工具 `upload_file`
- 当需求是"处理 PDF 本身"时，再使用 `pdf.*` 专属工具

### 读取 PDF 内容

通过 `read_file_content` 读取，系统会自动提取文本并转为 Markdown：

```json
{
  "file_id": "file_pdf_001"
}
```

返回内容更适合"阅读理解、摘要、信息提取"，不适合依赖版式精确保真的任务。

### 创建或写入 PDF 内容

通过 `upload_file` 上传 PDF 文件；若传入已有 `file_id`，则执行覆盖更新：

```json
{
  "drive_id": "string",
  "parent_id": "string",
  "file_id": "string",
  "size": 1024,
  "hashes": [
    { "sum": "string", "type": "sha256" }
  ]
}
```

### 适用场景

| 场景 | 说明 |
|------|------|
| 合同签署 | 用于分发和归档最终版文件 |
| 财务报表 | 保持固定版式，便于打印 |
| 资料归档 | 长期保存、减少误编辑 |
| 最终交付 | 将 Word/Excel/PPT 或 Markdown 输出为 PDF |

### 注意事项

- 写入 PDF 为全量覆盖，不支持像文档类文件那样的局部编辑
- 若需要频繁编辑正文，建议先使用 `otl`、`docx`、`sheet` 或 `pptx`，完成后再导出为 PDF
- `pdf.extract_pdf_pages` 的页码为 1-based，即第一页是 `1`

### 工具选择建议

| 目标 | 推荐工具 |
|------|------|
| 只想读取 PDF 文本内容 | `read_file_content` |
| 想知道 PDF 一共有多少页 | `pdf.get_pdf_page_count` |
| 想从 PDF 中抽取部分页面生成新 PDF | `pdf.extract_pdf_pages` |
| 想把 PDF 转成可编辑文档（docx/xlsx/pptx） | `pdf.convert`（默认付费额度，VIP 不足时降级 `is_free_convert=true` 重试） + `pdf.convert_query` |

---

## 一、读取 PDF 内容

### 1. read_file_content

#### 功能说明

读取指定文件的内容，系统会自动提取文本并转为 Markdown 格式。

**适用于**：阅读理解、摘要、信息提取。

#### 调用示例

```json
{
  "file_id": "file_pdf_001"
}
```

#### 参数说明

- `file_id` (string, 必填): 文件 ID

#### 模型使用建议

- 当用户说"帮我读一下这个 PDF 讲了什么"时，优先使用这个工具
- 返回内容更适合"阅读理解、摘要、信息提取"，不适合依赖版式精确保真的任务

---

## PDF 文档（pdf）专属接口

### 1. pdf.get_pdf_page_count

#### 功能说明

查询指定 PDF 文件的总页数。

**适用于**：在拆页前确认范围是否合法，或当用户明确询问"这个 PDF 有多少页"时调用。

- 当用户给出"提取第 X 到 Y 页"这类要求时，若页数上限未知，先查页数再执行拆页
- 当用户已经明确给出可靠页数范围时，也可以直接调用后续工具
- 这个工具只解决"页数确认"，不负责读取正文内容



#### 调用示例

查询 PDF 页数：

```json
{
  "file_id": "file_pdf_001"
}
```


#### 参数说明

- `file_id` (string, 必填): PDF 文件 ID

#### 返回值说明

```json
{
  "code": 0,
  "msg": "ok",
  "data": {
    "page_count": 15
  }
}

```

| 字段 | 类型 | 说明 |
|------|------|------|
| `data.page_count` | integer | PDF 总页数 |

---

### 2. pdf.extract_pdf_pages

#### 功能说明

从原 PDF 中提取指定页码范围，生成新的 PDF 文件。

**适用于**：合同附件拆分、章节抽取、仅导出指定页面。

- `from` 和 `to` 都必须是正整数
- 多个范围会按传入顺序组合到新的 PDF 中
- 建议先调用 `pdf.get_pdf_page_count`，避免页码越界

**模型使用建议**：

- 当用户说"把第 3 到 5 页单独导出""保留封面和附录"时，优先使用这个工具
- 页码是 1-based，不要按 0-based 传参
- 如果用户描述的是"按章节拆分"，但没有给出章节对应页码，应先通过阅读内容或询问用户确认页码
- 如果目标是"提取正文文本"而不是"生成新 PDF"，不要用这个工具，改用 `read_file_content`



#### 调用示例

提取第 1-3 页和第 8-10 页：

```json
{
  "file_id": "file_pdf_001",
  "ranges": [
    {
      "from": 1,
      "to": 3
    },
    {
      "from": 8,
      "to": 10
    }
  ]
}
```


#### 参数说明

- `file_id` (string, 必填): 原始 PDF 文件 ID
- `ranges` (array, 必填): 要提取的页码范围列表，不能为空
  - `from` (integer, 必填): 起始页，1-based，且包含该页
  - `to` (integer, 必填): 结束页，1-based，且包含该页

#### 返回值说明

```json
{
  "code": 0,
  "msg": "",
  "data": {
    "download_uri": "https://weboffice-test.ks3-cn-beijing.wpscdn.cn/tmp/exportfiles/..."
  }
}

```

| 字段 | 类型 | 说明 |
|------|------|------|
| `data.download_uri` | string | 提取后 PDF 的临时下载链接（有时效性） |

---

### 3. pdf.convert

#### 功能说明

将 PDF 转换为 Office 可编辑格式，并返回转换任务信息。

**适用于**：需要把 PDF 转为 `docx`、`xlsx` 或 `pptx` 继续编辑的场景。

- 本工具用于“发起转换任务”
- 转换完成结果需通过 `pdf.convert_query` 查询
- 页码参数为 1-based（第一页为 1）


> 默认 `is_free_convert=false`（付费额度），若返回 `code=400100` 或错误含 `VipLevelNotEnough` 等会员不足提示，使用相同 `file_id`、`to_format`、页码范围等参数，仅将 `is_free_convert` 设为 `true` 重试一次（免费额度最多处理前 5 页）
> 转换完成后，结果文件存入金山文档云盘 `我的云文档/应用/PDF转换`，文件名为 `原文件名.docx/xlsx/pptx`
> 若 `pdf.convert_query` 不可用（返回 404），可通过 `drive.search_files` 搜索转换后的文件名找到结果
> 获取转换文件后，用 `drive.share_file` 创建公开分享链接，再用 `drive.download_file` 获取下载信息

#### 调用示例

转换 PDF 为 docx：

```json
{
  "file_id": "file_pdf_001",
  "to_format": "docx",
  "page_range_from": 1,
  "page_range_to": 3,
  "is_free_convert": false
}
```


#### 参数说明

- `file_id` (string, 必填): PDF 文件 ID
- `to_format` (string, 必填): 目标格式，仅支持 docx、xlsx、pptx
- `file_name` (string, 可选): 转换后文件的文件名（不含扩展名，如原文件为"报告.pdf"则默认输出"报告"）；默认值：`自动取原 PDF 文件名（去掉 .pdf 后缀）`
- `page_range_from` (integer, 可选): 起始页码（1-based）；默认值：`1`
- `page_range_to` (integer, 可选): 结束页码（1-based）；默认值：`1`
- `open_password` (string, 可选): PDF 打开密码（有密码文件时填写）
- `edit_password` (string, 可选): PDF 编辑密码（有密码文件时填写）
- `messy_repair` (boolean, 可选): 是否开启乱码修复；默认值：`false`
- `is_free_convert` (boolean, 可选): 是否使用免费转换额度（免费额度最多处理前 5 页）。默认 false，优先使用付费额度以获得完整转换。当返回会员/VIP 不足错误（code=400100 或含 VipLevelNotEnough 等提示）时，应使用相同参数、仅将此字段设为 true 重新发起转换；默认值：`false`

#### 返回值说明

```json
{
  "code": {
    "type": "number"
  },
  "msg": {
    "type": "string"
  },
  "data": {
    "type": "object",
    "fields": [
      {
        "name": "file_id",
        "type": "integer",
        "description": "源 PDF 数字文件 ID"
      },
      {
        "name": "encoded_file_id",
        "type": "string",
        "description": "转换服务内部文件标识"
      },
      {
        "name": "convert_job",
        "type": "object",
        "description": "转换任务信息（含 jobid）"
      },
      {
        "name": "query_params",
        "type": "object",
        "description": "查询参数（用于调用 pdf.convert_query）"
      },
      {
        "name": "file_info",
        "type": "object",
        "description": "源 PDF 文件信息（含页数、转换进度 progress=100 表示完成）"
      },
      {
        "name": "result_files",
        "type": "array",
        "description": "转换结果文件列表（包含 file_id、name、type、download_url 等字段）"
      }
    ]
  }
}
```

| 字段 | 类型 | 说明 |
|------|------|------|
| `data.file_id` | integer | 源 PDF 数字文件 ID |
| `data.encoded_file_id` | string | 转换服务内部文件标识 |
| `data.convert_job` | object | 转换任务信息（含 jobid） |
| `data.query_params` | object | 查询参数（用于调用 pdf.convert_query） |
| `data.file_info` | object | 源 PDF 文件信息（含页数、转换进度 progress=100 表示完成） |
| `data.result_files` | array | 转换结果文件列表（包含 file_id、name、type、download_url 等字段） |

---

### 4. pdf.convert_query

#### 功能说明

查询 `pdf.convert` 发起的转换任务状态；完成后返回转换结果文件信息。

**适用于**：异步转换任务轮询，直到拿到可下载结果文件。

- 常见轮询间隔建议 1-2 秒
- 当 `progress=100` 时可读取结果文件信息


> `progress < 100` 时继续轮询
> `progress = 100` 时从 `result_files` 读取目标文件 URL 与类型

#### 调用示例

查询转换结果：

```json
{
  "jobid": "69d47281d3e451001f1be3a8wl",
  "file_id": "file_pdf_001",
  "fname": "contract.pdf"
}
```


#### 参数说明

- `jobid` (string, 必填): `pdf.convert` 返回的转换任务 ID
- `file_id` (string, 必填): 源 PDF 文件 ID
- `fname` (string, 可选): 源 PDF 文件名（含 .pdf 后缀）；默认值：`document.pdf`

#### 返回值说明

```json
{
  "code": {
    "type": "number"
  },
  "msg": {
    "type": "string"
  },
  "data": {
    "type": "object",
    "fields": [
      {
        "name": "progress",
        "type": "integer",
        "description": "转换进度，100 表示完成"
      },
      {
        "name": "result_files",
        "type": "array",
        "description": "转换结果文件列表（完成后返回）"
      }
    ]
  }
}
```

| 字段 | 类型 | 说明 |
|------|------|------|
| `data.progress` | integer | 转换进度，100 表示完成 |
| `data.result_files` | array | 转换结果文件列表（完成后返回） |

---


## 工具速查表

| # | 工具名 | 功能 | 必填参数 |
|---|--------|------|----------|
| 1 | `pdf.get_pdf_page_count` | 查询 PDF 总页数 | `file_id` |
| 2 | `pdf.extract_pdf_pages` | 提取指定页并生成新 PDF | `file_id`, `ranges` |
| 3 | `pdf.convert` | 发起 PDF 转 Office 转换任务 | `file_id`, `to_format` |
| 4 | `pdf.convert_query` | 查询 PDF 转换任务进度与结果 | `jobid`, `file_id` |

## 常用工作流

### PDF 文档操作

按用户需求选择对应操作：

**读取 PDF 内容**：
1. `search_files` 或 `get_share_info` 定位文档 → 获取 `file_id`、`drive_id`
2. `read_file_content(file_id=..., format="markdown")` → 返回 Markdown 文本
> 适合摘要、信息提取等场景；复杂排版可能有精度损失

**查询 PDF 页数**：
1. `search_files` 定位 PDF → 获取 `file_id`
2. `pdf.get_pdf_page_count(file_id=...)` → 返回总页数

**提取指定页面**：
1. `search_files` 定位 PDF → 获取 `file_id`
2. `pdf.get_pdf_page_count` 确认总页数，校验用户请求的页码是否越界
3. `pdf.extract_pdf_pages(file_id=..., ranges=[{from:1,to:1},{from:5,to:8}])` → 生成新 PDF
> 页码 1-based；`ranges` 为 `{from, to}` 对象数组，多段按顺序合并；提取结果为临时下载链接

**转换为可编辑文档（Word/Excel/PPT）**：
1. `search_files` 定位 PDF → 获取 `file_id`
2. `pdf.convert(file_id=..., to_format="docx|xlsx|pptx", ...)` 发起转换任务（默认 `is_free_convert=false`）
3. 若步骤 2 返回 `code=400100` 或含 `VipLevelNotEnough` 等会员不足提示，使用相同参数、仅将 `is_free_convert=true` 重新调用 `pdf.convert`（免费额度最多处理前 5 页）
4. `pdf.convert_query(jobid=..., file_id=..., fname=...)` 轮询进度，直到 `progress=100`
5. 从 `result_files` 读取转换结果（类型、大小、下载 URL）

**创建/上传 PDF**：
- `upload_file(drive_id=..., parent_id=..., name="xxx.pdf", content_base64=...)` 直接上传
- 更新已有 PDF：`upload_file(file_id=..., content_base64=...)` 全量覆盖

## 常见决策示例

- 用户说"帮我读一下这个 PDF 讲了什么"：用 `read_file_content`
- 用户说"这个 PDF 有多少页"：用 `pdf.get_pdf_page_count`
- 用户说"把第 2 到 6 页单独导出来"：用 `pdf.extract_pdf_pages`
- 用户说"把这个 PDF 转成 Word/Excel/PPT"：先用 `pdf.convert`（默认 `is_free_convert=false`），若返回会员不足错误（`code=400100` / `VipLevelNotEnough`）则将 `is_free_convert` 改为 `true` 重试，再用 `pdf.convert_query` 轮询结果
