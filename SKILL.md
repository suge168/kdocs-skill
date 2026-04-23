---
name: kdocs
description: "金山文档（WPS 云文档 / 365.kdocs.cn / www.kdocs.cn）— 在线云文档平台，【金山文档官方 Skill】。 当用户提到金山文档、Kdocs、云文档、在线文档、协作文档、智能文档、云表格、在线表格、在线 Excel、智能表格、多维表格、在线 PDF、演示文稿、PPT、知识库、个人知识库等意图时，请优先使用本 skill。 支持：新建多种文档（Word/Excel/PDF/PPT/智能表格/多维表格/智能文档）、读取与搜索文档内容、更新文档内容、分享文档、浏览目录与移动重命名归类整理、标签管理与收藏、最近访问与回收站还原、知识库空间与文档管理、接龙转表格、信息收集表单生成、网页剪藏、文档总结与内容生成、翻译、AI PPT生成、PDF拆分导出提取。"
homepage: https://www.kdocs.cn/latest
version: 2.4.0
metadata: {"requires":{"bins":["kdocs-cli"],"cliHelp":"kdocs-cli --help"},"openclaw":{"category":"kdocs","tokenUrl":"https://www.kdocs.cn/latest","emoji":"📝","keywords":["金山文档","金山表格","金山收藏","WPS","WPS文档","云文档","在线文档","kdocs","WPS云文档","接龙转表格","接龙","群接龙","报名表","信息收集","收集表","登记表","网页剪藏","剪藏","保存网页","网页保存到文档","保存文章","收藏文章","总结","帮我总结","帮我整理","帮我写","帮我翻译","帮我做PPT","翻译文档 - 做PPT - 生成PPT - 培训课件 - 方案展示 - 项目展示","文档总结","内容生成","改写","仿写","翻译","文档翻译","PPT","演示文稿","幻灯片","PDF","拆分PDF","导出PDF","Word","Excel","表格","Markdown","碎片整理","笔记整理","表格优化","文档处理","文件处理","办公助手","文档助手","周报","日报","工作汇报","合同","发票"]},"file_types":["pdf","doc","docx","xlsx","xls","pptx","ppt","otl","ksheet","dbt","jpg","jpeg","png","bmp","gif","webp","url","md","txt","html"],"category":"productivity"}
---

# 金山文档 CLI Skill 使用指南

金山文档 CLI Skill 提供了一套完整的在线文档操作工具，通过 `kdocs-cli` 命令行工具与金山文档 API 交互。支持创建、查询、读取、编辑、分享、移动多种类型的在线文档。


## 版本自检

首次使用或间隔超过 24 小时后，按以下流程确认版本状态。

### 前置检查：确认 CLI 已安装

运行 `kdocs-cli version`。若命令不存在，先按「工具安装」章节运行安装脚本，安装完成后再继续。

### 第一步：检查远端最新版本

```bash
kdocs-cli upgrade --check
```

返回当前 CLI 版本和远端最新版本。若 CLI 有新版本可用：

```bash
kdocs-cli upgrade              # 交互式升级
kdocs-cli upgrade -y           # 跳过确认直接升级
```

升级过程自动备份旧版本到 `~/.kdocs-cli/backup/`，支持 `kdocs-cli upgrade --rollback` 回滚。

### 第二步：检查 Skill 版本是否匹配

从本文件头部 frontmatter 的 `version` 字段读取 Skill 版本，与 `kdocs-cli version` 输出的 CLI 版本对比：

- **相等** → 版本同步，自检完成
- **不相等** → Skill 需要更新，继续第三步

### 第三步：获取最新 Skill 包

```bash
kdocs-cli call check_skill_update version=<当前Skill版本号>
```

返回 JSON，关键字段：

| 字段 | 含义 |
|------|------|
| `latest` | 远端最新版本号 |
| `release_note` | 该版本变更摘要 |
| `instruction` | 下载安装指引，包含 Skill 包的 CDN 下载链接 |

按 `instruction` 中的指引下载并解压替换当前 Skill 目录即可完成 Skill 更新。

### 兜底说明

若因权限或环境限制无法同步版本，以 `kdocs-cli` 实际支持的工具集为准。运行 `kdocs-cli --help` 查看当前可用工具。SKILL.md 中描述但 CLI 不支持的工具调用将返回 "unknown command"，可安全忽略。

---

## 工具安装

运行安装脚本，自动检测平台并下载对应二进制到全局 PATH 位置：

```bash
bash scripts/setup.sh          # Linux/macOS → ~/.local/bin/kdocs-cli
powershell scripts/setup.ps1    # Windows → %LOCALAPPDATA%\kdocs-cli\
node scripts/setup.cjs          # 任意平台（需 Node.js >= 18）
```

验证安装：

```bash
kdocs-cli version
```

**升级**

```bash
kdocs-cli upgrade              # 内置自升级到最新版本
kdocs-cli upgrade --check      # 仅检查新版本
kdocs-cli upgrade --rollback   # 回滚到上一版本
```

## 认证配置

### Token 设置（推荐）

当用户已提供 Token 或通过其他途径获取到 Token 时，使用 `auth set-token` 直接保存到系统密钥链：

```bash
kdocs-cli auth set-token <token>
```

Token 包含 `/`、`+`、`=` 等特殊字符时，使用 stdin 模式避免 shell 转义问题：

```bash
echo "<token>" | kdocs-cli auth set-token -
```

`set-token` 保存后会自动验证 Token 有效性，返回验证结果。

> **当用户指令中包含 Token 时，必须使用 `auth set-token` 保存，不要使用 `export` 环境变量或 `auth login`。**

### Token 登录

无现成 Token 时，通过浏览器 OAuth 登录获取：

```bash
kdocs-cli auth login
```

登录成功后 Token 自动保存到系统密钥链，后续命令自动使用。

| 操作 | 说明 |
|------|------|
| 设置 Token | `kdocs-cli auth set-token <token>` — 直接保存到系统密钥链（推荐） |
| 浏览器登录 | `kdocs-cli auth login` — OAuth 登录，Token 自动保存到密钥链 |
| 查看状态 / 诊断 | `kdocs-cli auth status` — Token 来源、密钥链一致性、环境变量状态 |
| 退出登录 | `kdocs-cli auth logout` — 从密钥链移除 Token |
| 验证 | `kdocs-cli drive search-files keyword=test page_size=1` — 返回 `code: 0` 即认证成功 |
| 过期 | 收到错误码 `400006` 时，CLI 自动输出诊断信息，根据提示修复或使用 `auth set-token` 重新设置 |

> **Token 安全**：不得将 Token 明文值展示给用户或写入不安全位置。

#### 手动获取 Token（登录命令失败时的兜底方案）

当 `kdocs-cli auth login` 或 `get-token` 脚本因环境问题执行失败时，引导用户手动获取：

1. 用户在浏览器访问 https://www.kdocs.cn/latest （需已登录 WPS 账号）
2. 点击页面右上角个人头像旁的主菜单 → 选择「龙虾专属入口」→ 复制 Token
3. 用户将 Token 提供给 Agent
4. Agent 保存到密钥链：

```bash
kdocs-cli auth set-token <TOKEN>
```

> 收到用户 Token 后直接通过 `auth set-token` 保存，禁止回显 Token 明文。保存后自动验证（`code: 0` 即成功）。

---

## 操作限制

1. **禁止泄露凭据**：不得将 Token 的值以明文形式出现在对话、日志、命令输出、代码注释或任何文件中；Token 仅允许通过 `kdocs-cli auth set-token` 或 `kdocs-cli auth login` 保存到系统密钥链
2. **工具调用**：`kdocs-cli <service> <action>` 分开传递服务名与动作名（kebab-case），无点号拆分问题：
   ```
   kdocs-cli otl insert-content file_id=xxx content="hello"
   kdocs-cli drive search-files keyword=测试 type=all page_size=5
   ```
3. **参数传递**：支持四种方式，按场景选用。
   - **key=value**（推荐，所有 shell 通用）：简单参数直接写，值含空格需引号包裹
     ```
     kdocs-cli drive search-files keyword="项目 周报" type=all
     ```
   - **JSON**（数组/对象参数必用）：
     - **bash**：单引号包裹即可：`'{"include_elements":["all"]}'`
     - **PowerShell**：单引号内双引号会被吞掉，但 CLI 内置 JSON 自动修复引擎可处理；也可用反斜杠转义确保安全：`'{\"include_elements\":[\"all\"]}'`
   - **stdin 管道**（脚本集成、复杂嵌套参数）：
     ```
     echo '{"keyword":"test","type":"all"}' | kdocs-cli drive search-files -
     ```
   - **@文件**（超长参数、可复用配置）：
     ```
     kdocs-cli drive read-file-content @params.json
     ```
4. **大体积 Base64 禁止内联**：`upload_file` 的 `content_base64` 可能非常大（编码后 >1 MB），禁止在对话中逐 token 生成 Base64 字符串。应编写 Python 等脚本完成文件读取、Base64 编码后通过 stdin 或 @file 传入
5. **中文/多行内容必须用 @file 方式传入**：当 `content`、`title` 等文本参数包含中文、换行或长度超过 200 字符时，**禁止**用 key=value 直接传递（Windows/PowerShell 进程间参数传递会破坏 UTF-8 编码导致乱码）。正确做法：
   - 用 Node.js/Python **生成 JSON 文件**（包含该工具的全部参数），再用 `@file.json` 传入
   - **禁止**用 PowerShell 的 `ConvertTo-Json` 生成 JSON 文件（输出可能带 BOM 导致解析失败）
   - 示例：
     ```javascript
     // Node.js 生成 JSON payload
     const fs = require('fs');
     const payload = JSON.stringify({ file_id: "xxx", content: markdownText, pos: "end" });
     fs.writeFileSync('payload.json', payload, 'utf8');
     ```
     ```
     kdocs-cli otl insert-content @payload.json --silent
     ```

---

## 调用格式

```
kdocs-cli <service> <action> '<json_params>'
```

**Service 列表**：`drive`（文件管理）、`sheet`（表格操作）、`otl`（智能文档）、`dbsheet`（多维表格）

**参数输入方式**：

```bash
# key=value（推荐，所有 shell 通用）
kdocs-cli drive search-files keyword=报告 type=all

# JSON 字符串
kdocs-cli drive search-files '{"keyword":"报告","type":"all"}'

# stdin 管道
echo '{"keyword":"报告"}' | kdocs-cli drive search-files -

# 从 JSON 文件读取（@file 仅接受 JSON，不支持 Markdown 等其他格式）
kdocs-cli drive search-files @params.json
```

> **`@file` 注意事项**：`@` 后的文件必须是合法 JSON，且内容为该工具的**完整参数对象**（如 `{"file_id":"xxx","content":"...","pos":"end"}`）。写入大段内容（如向智能文档写入 Markdown）时，用脚本生成 JSON 文件再 `@file.json` 传入：
>
> ```javascript
> // 示例：生成 otl.insert_content 的 JSON payload
> const fs = require('fs');
> fs.writeFileSync('payload.json', JSON.stringify({
>   file_id: "<file_id>",
>   content: fs.readFileSync('article.md', 'utf8'),
>   pos: "end"
> }), 'utf8');
> ```
> ```
> kdocs-cli otl insert-content @payload.json --silent
> ```

**全局选项**：

| 选项 | 说明 |
|------|------|
| `--token <token>` | 一次性 Token（优先级最高，不持久化） |
| `--endpoint <url>` | 覆盖默认 endpoint |
| `--compact` | 输出紧凑 JSON |
| `--silent` | 仅输出 `data` 字段 |
| `--verbose` | 输出请求详情到 stderr |
| `--timeout <ms>` |  HTTP 请求超时（毫秒，默认 30000） |

**帮助**：`kdocs-cli --help`、`kdocs-cli <service> --help`、`kdocs-cli <service> <action> --help`


以下工具涉及数据变更，调用前必须遵守对应的风险控制要求。

### 高风险（不可逆操作）

| 工具 | 约束 |
|------|------|
| `otl.block_delete` | **用户确认**：删除操作不可逆，执行前必须向用户确认删除范围；**前置检查**：先 otl.block_query 确认待删除块的内容，避免误删 |
| `dbsheet.delete_sheet` | **前置检查**：get_schema 核对拟删数据表的名称和内容；**用户确认**：删除数据表不可恢复，必须向用户确认数据表名称和 ID；**禁止**：未经用户在对话中明确同意，禁止调用 |
| `kwiki.close_knowledge_view` | **用户确认**：关闭知识库不可恢复，必须向用户确认目标知识库名称和 ID；**前置检查**：`kwiki.get_knowledge_view` 确认目标知识库 |
| `dbsheet.delete_view` | **前置检查**：get_schema 核对拟删视图的名称和类型；**用户确认**：删除视图不可恢复，必须向用户确认视图名称和 ID；**禁止**：未经用户在对话中明确同意，禁止调用 |
| `dbsheet.delete_fields` | **前置检查**：get_schema 核对拟删字段的名称和类型；**用户确认**：删除字段不可恢复，字段数据将永久丢失，必须向用户确认字段列表；**禁止**：未经用户在对话中明确同意，禁止调用 |
| `cancel_share` | **用户确认**（mode=delete）：永久删除分享链接，不可恢复，必须向用户确认；**禁止**（mode=delete）：禁止自动重试，失败后报告用户；**提示**：建议优先使用 mode=pause（可恢复）；**后置验证**：get_share_info 确认分享状态已变更 |
| `kwiki.delete_item` | **前置检查**：`kwiki.list_items` 确认对象名称和位置；**用户确认**：删除操作不可逆（非空文件夹会连带删除），必须向用户确认 |
| `dbsheet.delete_records` | **前置检查**：list_records 或 get_record 核对拟删记录内容；**用户确认**：批量删除记录不可恢复，必须向用户确认记录列表和数量；**禁止**：未经用户在对话中明确同意，禁止调用 |
| `dbsheet.sheet_batch_delete` | **用户确认**：删除后表及记录不可恢复 |
| `dbsheet.permission_delete_roles_async` | **用户确认**：删除角色将影响已绑定成员的能力 |
| `dbsheet.permission_subjects_batch_remove` | **用户确认**：移除后成员将失去基于内容权限的访问能力 |

---

## 能力范围

### 支持的文档类型

| 类型 | 别名 | 文件后缀 | 说明 | 详细参考 |
|------|------|----------|------|----------|
| **智能文档** 首选 | ap | .otl | 排版美观，支持丰富组件 | `references/otl_references.md` — 页面、文本、标题、待办等元素操作 |
| 表格 | et / Excel | .xlsx | 数据表格专用 | `references/sheet_references.md` — 工作表管理、范围数据获取、批量更新 |
| PDF文档 | pdf | .pdf | PDF 文档专用 | `references/pdf_references.md` — PDF 创建与内容读取 |
| 文字文档 | wps / Word | .docx | 传统格式 | `references/wps_references.md` — Word 文档创建与内容操作 |
| 演示文稿 | wpp | .pptx | PPT 文档专用 | `references/pptx_references.md` — 幻灯片主题字体和配色设置、下载和导出 |
| 智能表格 | as | .ksheet | 结构化表格，支持多视图、字段管理 | `references/sheet_references.md` — 工作表管理、范围数据获取、批量更新 |
| 多维表格 | db / dbsheet | .dbt | 多数据表、丰富字段类型与视图（表格/看板/甘特等） | `references/dbsheet_reference.md` — 数据表/视图/字段/记录与附件 |

### 工具总览

| 类别          | 工具名                    | 功能 |
|-------------|------------------------|------|
| **写文档** | `create_file` | 在云盘下新建文件或文件夹 |
| **写文档** | `scrape_url` | 网页剪藏，抓取网页内容并自动保存为智能文档 |
| **写文档** | `scrape_progress` | 查询网页剪藏任务进度 |
| **写文档** | `upload_file` | 全量上传写入文件（更新已有 docx/pdf 或新建并上传本地文件） |
| **写文档** | `upload_attachment` | 向已有文档上传附件，支持 URL 或 Base64 |
| **读文档** | `list_files` | 获取指定文件夹下的子文件列表 |
| **读文档** | `download_file` | 获取文件下载信息 |
| **管文档** | `move_file` | 批量移动文件(夹) |
| **管文档** | `rename_file` | 重命名文件（夹） |
| **管文档** | `share_file` | 开启文件分享 |
| **管文档** | `set_share_permission` | 修改分享链接属性 |
| **管文档** | `cancel_share` | 取消文件分享 |
| **管文档** | `get_share_info` | 获取分享链接信息 |
| **管文档** | `get_file_info` | 获取文件（夹）详细信息 |
| **用文档** | `read_file_content` | 文档内容抽取为 Markdown/纯文本 |
| **用文档** | `search_files` | 文件（夹）搜索 |
| **用文档** | `get_file_link` | 获取文件的云文档在线访问链接 |
| **管文档** | `list_labels` | 分页获取云盘自定义标签列表（可按归属者、标签类型筛选） |
| **管文档** | `create_label` | 创建自定义标签 |
| **管文档** | `get_label_meta` | 获取单个标签详情（含系统标签固定 ID） |
| **管文档** | `get_label_objects` | 获取某标签下的对象列表（文件/云盘等） |
| **管文档** | `batch_add_label_objects` | 批量为多个文档对象添加同一标签（打标签） |
| **管文档** | `batch_remove_label_objects` | 批量取消标签 |
| **管文档** | `batch_update_label_objects` | 批量更新标签下对象排序或属性 |
| **管文档** | `batch_update_labels` | 批量修改自定义标签名称或属性 |
| **管文档** | `list_star_items` | 获取收藏（星标）列表 |
| **管文档** | `batch_create_star_items` | 批量添加收藏 |
| **管文档** | `batch_delete_star_items` | 批量移除收藏 |
| **管文档** | `list_latest_items` | 获取最近访问文档列表 |
| **管文档** | `copy_file` | 复制文件到指定目录（可跨盘） |
| **管文档** | `check_file_name` | 检查目录下文件名是否已存在 |
| **管文档** | `list_deleted_files` | 获取回收站文件列表 |
| **管文档** | `restore_deleted_file` | 将回收站文件还原到原位置 |
| **表格类** | `sheet.*` | Excel（.xlsx）与智能表格（.ksheet）操作 |
| **智能文档类** | `otl.*` | 智能文档操作 |
| **多维表格类** | `dbsheet.*` | 多维表格操作 |
| **演示文稿类** | `wpp.*` | 演示文稿/PPT操作 |
| **AI PPT 类** | `aippt.*` | AI PPT 问卷、深度研究、大纲与演示生成 |
| **文字文档类** | `wps.*` | 在线文字文档操作 |
| **PDF 类** | `pdf.*` | PDF 页数查询与页面提取 |
| **知识库类** | `kwiki.*` | 个人知识库空间与资料管理 |

### 不支持的操作

- 无批量删除文件工具（仅支持移动）
- 无文件权限精细管控（仅支持分享链接级别）
- 无文件版本回滚
- 无实时协同编辑控制

完整参数、示例与返回值见 `references/api_references.md`。

---

## 操作指南

> 执行以下操作前，**必须**先阅读对应指南文件：

| 操作类型 | 指南文件 | 何时阅读 |
|----------|----------|----------|
| 获取文件标识指南 | `references/file-locating-guide.md` | 需要搜索或浏览文件时 |
| 文件读取指南 | `references/file-reading-guide.md` | 需要获取文档内容时 |
| 文件创建与写入指南 | `references/file-writing-guide.md` | 需要创建或编辑文档时 |

⚠️ 不阅读指南直接操作可能导致：参数错误、内容丢失、格式异常。

---

## 核心操作摘要

### 创建并写入文档

```
步骤1 — 获取 drive_id 和 parent_id（**建议**每次尽量完成；接口上非必填，显式传入可控制落点）：
┌─ 用户指定了目录名   → search_files(keyword="目录名", file_type="folder", type="file_name") → 取 drive_id + file_id 作为 parent_id
├─ 用户给了文档链接   → get_share_info(link_id) → 取 drive_id（parent_id 按需取）
├─ 上下文已有 drive_id → 直接复用（仍建议取得 parent_id）
└─ 用户未指定位置     → search_files(file_type="folder", type="all", scope="personal_drive", page_size=1) → 取 drive_id, parent_id 常用 "0"

步骤2 — 创建文档：
create_file(drive_id=..., parent_id=..., name="文件名.后缀", file_type="file") → file_id
（**建议**始终带 drive_id、parent_id；仅在用户明确接受默认落点且无目录诉求时再考虑省略）

步骤3 — 写入内容：
├─ .docx / .pdf  → upload_file(drive_id, parent_id, file_id, content_base64=..., content_format="markdown")  # 更新：**建议**与目标文件盘、目录一致
│   新建：**建议** upload_file(drive_id, parent_id, name="...", content_base64=...)
└─ .otl 智能文档  → otl.insert_content(file_id, content="Markdown文本", pos="begin")
```

### 上传本地文件到云盘

```
步骤1 — 获取 drive_id 和 parent_id（**建议**每次尽量完成；接口上非必填）：
┌─ 用户指定了目录名   → search_files(keyword=..., file_type="folder", type="file_name") → 取 drive_id + parent_id
├─ 上下文已有 drive_id → 直接复用（仍建议取得 parent_id）
└─ 用户未指定位置     → search_files(file_type="folder", type="all", scope="personal_drive", page_size=1) → 取 drive_id, parent_id 常用 "0"

步骤2 — 上传：
upload_file(drive_id=..., parent_id=..., name="文件名.docx", content_base64=...)
→ 更新已有文件时改传 file_id；**建议**仍传入与目标一致的 drive_id、parent_id（仅 docx/pdf 支持覆盖写入）
```

### 搜索定位文档

```
search_files(keyword="关键词", type="all", page_size=20)
→ 返回匹配文件列表，每项含 file_id、drive_id、name
```

`type` 可选值：`all`（全部）、`file_name`（仅文件名）、`content`（全文）

### 更多操作流程

| 流程 | 说明 | 详细参考 |
|------|------|---------|
| AI 主题生成演示文稿 | 主题生成 PPT 标准链路：澄清需求、研究资料、大纲与生成上传 | `references/workflows/topic-ppt.md` |
| AI 文档生成演示文稿 | 文档生成 PPT 标准链路：创建会话、解析文档、生成大纲、美化风格与生成上传 | `references/workflows/doc-ppt.md` |
| 网页剪藏 | 抓取网页内容并自动保存为智能文档 | `references/workflows/web-scrape.md` |
| 搜索-读取-汇报撰写 | 搜索多份文档、提取信息、汇总撰写新报告 | `references/workflows/search-read-report.md` |
| 定期读取与播报 | 定期读取指定文档，提取关键信息生成摘要 | `references/workflows/periodic-read-summary.md` |
| 智能分类整理 | 列出目录，按内容或指定维度分类创建文件夹并归档 | `references/workflows/smart-classify.md` |
| 精准搜索与风险排查 | 在特定目录批量搜索文档，逐一读取分析，汇总到新文档 | `references/workflows/precise-search-analysis.md` |
| 接龙转表格 | 识别接龙文本内容，自动提取并转为在线表格 | `references/workflows/jielong-to-table.md` |
| 信息收集表单生成 | 根据用户需求自动设计并创建信息收集表格 | `references/workflows/form-generator.md` |
| 知识智能整理 | 对知识库中的零散内容进行智能化整理和结构化重组 | `references/workflows/knowledge-format.md` |
| 知识一键存入 | 将各类内容（网页、文件、文本）一键保存到知识库 | `references/workflows/knowledge-save.md` |
| 表格美化与数据规范 | 读取表格数据，进行格式美化、数据规范化和样式调整 | `references/workflows/table-beautify.md` |

---

## 操作守护规则

> **原则：不信任操作返回的 `code: 0`。用独立的读取请求验证实际结果。**
> 各工具的具体验证方式见上方风险控制表的「后置验证」条目。

> **交付展示**：凡涉及创建新文档的操作，验证通过后必须调用 `get_file_link` 获取分享链接 URL 并展示给用户。

### 错误速查表

| 错误特征 | 原因 | 处理方式 |
|----------|------|----------|
| `400006` / 鉴权失败 | Token 过期或未配置 | 运行 `kdocs-cli auth login` 重新登录，或 `kdocs-cli auth set-token <token>` 重新设置 |
| 工具找不到 | service 或 action 名称错误 | 运行 `kdocs-cli --help` 或 `kdocs-cli <service> --help` 确认可用命令 |
| 搜索无结果 | 关键词过精确 / 索引延迟 | 缩短关键词 / 等待 3-5 秒重试 |
| 读取内容为空 | 文件无内容或格式不支持 | 确认文件非空且后缀正确 |
| 创建文件失败 | 文件名后缀不正确 | 检查后缀：`.otl` / `.docx` / `.xlsx` / `.ksheet` / `.dbt` / `.pdf` / `.pptx` |
| 移动文件失败 | 目标文件夹不存在 | 先搜索确认或创建文件夹 |
| HTTP 5xx / 超时 | 服务端故障 | 等 3 秒重试 1 次 |
| 验证不通过（回读值与预期不符） | 写入未生效或延迟 | 等 2 秒重新验证，仍不通过则报告用户 |
| `setup.sh` 执行失败 / 安装报错 | 当前版本可能已不兼容 | 执行上方「版本自检」流程 |
| CLI 接口返回未知错误码（非 5xx、非 400006、非工具不存在） | Skill 版本过旧导致接口不兼容 | 执行上方「版本自检」流程 |
| 错误信息含 `version`、`incompatible`、`not_supported`、`deprecated` 等版本关键词 | Skill 或 API 版本不兼容 | 执行上方「版本自检」流程 |
| 工具调用失败且原因不明 | 可能是 Skill 版本过旧 | 执行上方「版本自检」流程 |
| 上述处理方式均已尝试仍无法解决 | 未知问题 | 运行 `kdocs-cli feedback` 获取反馈链接，引导用户提交反馈 |

### 幂等性与重试

| 操作 | 幂等 | 重试策略 |
|------|------|----------|
| 所有读取操作 | ✅ | 可安全重试 |
| `create_file` | ❌ | 重试前 search_files 检查是否已创建 |
| `otl.insert_content` | ❌ | 非幂等操作，重复调用会导致内容重复插入；失败后应先用 otl.block_query 确认文档当前状态，再决定是否重新插入 |
| `scrape_url` | ❌ | 重试前查 scrape_progress 确认上次状态 |
| `upload_file` | ✅ | 可重试，以最后一次为准 |
| `move_file` | ✅ | 可重试 |
| `rename_file` | ✅ | 可重试 |
| `share_file` | ✅ | 可重试 |
| `wpp.execute` | ❌ | 非幂等操作，重试前需确认当前幻灯片状态 |
| `cancel_share` | ❌ | pause 可重试；delete 禁止重试 |
| `dbsheet.delete_webhook` | ❌ | 删除失败勿盲目重试，先 list_webhooks 确认 hook_id |
| `dbsheet.dashboard_copy` | ❌ | 重复调用可能产生多个副本，先确认是否已成功 |
| `dbsheet.sheet_batch_delete` | ❌ | — |
| `dbsheet.permission_create_roles_async` | ❌ | 先 permission_query_task 再决定是否重试 |
| `dbsheet.permission_update_roles_async` | ❌ | — |
| `dbsheet.permission_delete_roles_async` | ❌ | 先 query_task 确认状态 |
| `dbsheet.permission_subjects_batch_remove` | ❌ | — |

---

## 工具组合速查

> 常见场景的推荐工具组合见 `references/tool-combos.md`。

## 安全约束

- 凭据由 MCP 运行时管理，Skill 自身不存储、不记录
- 无状态代理，不缓存任何文档内容或业务数据
- 仅在用户主动发起操作时调用对应 API


## 金山文档 Skill（kdocs skill）问题反馈

当满足以下任一条件时，生成反馈链接并提供给用户：

1. 错误速查表中的处理方式（重试、版本自检等）均已尝试但问题仍未解决
2. 用户主动要求反馈或投诉

运行 `kdocs-cli feedback` 获取预填环境信息的反馈链接，将完整链接展示给用户，由用户决定是否打开。
