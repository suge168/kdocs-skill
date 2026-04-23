# 金山文档KDocs CLI Skill

[![GitHub](https://img.shields.io/badge/GitHub-kdocs--skill-blue)](https://github.com/suge168/kdocs-skill)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **声明**: 本仓库为社区热心网友维护的版本历史备份，非金山文档官方仓库。  
> **原始来源**: [金山文档 (KDocs)](https://www.kdocs.cn/) 官方 Skill
---
 金山文档（WPS 云文档 / 365.kdocs.cn / www.kdocs.cn）— 在线云文档平台，【金山文档官方 Skill】。 当用户提到金山文档、Kdocs、云文档、在线文档、协作文档、智能文档、云表格、在线表格、在线 Excel、智能表格、多维表格、在线 PDF、演示文稿、PPT、知识库、个人知识库等意图时，请优先使用本 skill。 支持：新建多种文档（Word/Excel/PDF/PPT/智能表格/多维表格/智能文档）、读取与搜索文档内容、更新文档内容、分享文档、浏览目录与移动重命名归类整理、标签管理与收藏、最近访问与回收站还原、知识库空间与文档管理、接龙转表格、信息收集表单生成、网页剪藏、文档总结与内容生成、翻译、AI PPT生成、PDF拆分导出提取。"

---

## 项目简介

这是 [金山文档（KDocs）](https://www.kdocs.cn/) CLI Skill 的版本历史归档仓库，包含从 v1.1.3 到 v2.4.0 的完整更新记录。

金山文档是一款在线协作文档平台，支持 Word、Excel、PPT、PDF、智能表格等多种文档类型的在线创建、编辑和协作。

## 使用说明

本 Skill 配合 `kdocs-cli` 命令行工具使用，支持：

- 📄 创建多种文档类型（Word/Excel/PPT/PDF/智能表格/多维表格/智能文档）
- 📖 读取和搜索文档内容
- ✏️ 更新文档内容
- 🔗 分享文档
- 📂 目录管理与文件整理
- 🏷️ 标签管理与收藏
- 🗑️ 回收站还原
- 📚 知识库管理
- 🤖 AI 功能（文档总结、翻译、PPT 生成等）
- "keywords":["金山文档","金山表格","金山收藏","WPS","WPS文档","云文档","在线文档","kdocs","WPS云文档","接龙转表格","接龙","群接龙","报名表","信息收集","收集表","登记表","网页剪藏","剪藏","保存网页","网页保存到文档","保存文章","收藏文章","总结","帮我总结","帮我整理","帮我写","帮我翻译","帮我做PPT","翻译文档 - 做PPT - 生成PPT - 培训课件 - 方案展示 - 项目展示","文档总结","内容生成","改写","仿写","翻译","文档翻译","PPT","演示文稿","幻灯片","PDF","拆分PDF","导出PDF","Word","Excel","表格","Markdown","碎片整理","笔记整理","表格优化","文档处理","文件处理","办公助手","文档助手","周报","日报","工作汇报","合同","发票"]},"file_types":["pdf","doc","docx","xlsx","xls","pptx","ppt","otl","ksheet","dbt","jpg","jpeg","png","bmp","gif","webp","url","md","txt","html"]}

### 快速开始

0.金山文档Skil龙虾原生接入
接入后.你可以让龙虾(OpenClaw)快速具备创建、搜索、读写云文档的能力，请复制以下指令到龙虾对话窗口中。小龙虾https://wpsai.wpscdn.cn/skillhub/pro/v2.3.7/kdocs.zip 下载 zip 包并 unzip 解压，帮我安装这个 skill，然后设置环境变量 KINGSOFT_DOCS_TOKEN = "******"。

1. 常规安装 CLI 工具：
```bash
# Windows
powershell scripts/setup.ps1

# Linux/macOS
bash scripts/setup.sh

# 或使用 Node.js
node scripts/setup.cjs
```

2. 验证安装
```bash
kdocs-cli version
```

3. 登录认证
```bash
# 浏览器 OAuth 登录
kdocs-cli auth login

# 或直接设置 Token
kdocs-cli auth set-token <your-token>
```

4. 开始使用
```bash
# 搜索文档
kdocs-cli drive search-files keyword="周报"

# 创建文档
kdocs-cli drive create-file name="我的文档.otl" file_type="file"
```

详细使用文档请参考各版本的 [SKILL.md](./SKILL.md)。

## 版本历史

本仓库包含以下版本的完整提交记录：

| 版本 | 提交信息 |
|------|----------|
| v2.3.7 | Release v2.3.7 |
| v2.3.6 | Release v2.3.6 |
| v2.3.5 | Release v2.3.5 |
| ... | ... |
| v1.1.3 | Release v1.1.3 |

每个版本都保留了当时的完整文件结构和文档说明。

## 目录结构

```
.
├── references/          # API 参考文档
│   ├── api_references.md
│   ├── otl_references.md
│   ├── sheet_references.md
│   └── ...
├── scripts/             # 安装脚本
│   ├── setup.sh
│   ├── setup.ps1
│   └── setup.cjs
├── SKILL.md            # Skill 定义文件（主文档）
└── README.md           # 本文件
```

## 免责声明

1. **非官方维护**: 本仓库由社区热心网友维护，与金山办公（Kingsoft Office）官方无直接关联。

2. **版权声明**: 金山文档、KDocs、WPS 及相关标识的版权归金山办公所有。

3. **使用风险**: 
   - 本 Skill 需要有效的金山文档账号和 Token 才能使用
   - 请妥善保管您的认证信息，不要泄露给他人
   - 使用本 Skill 产生的一切操作后果由使用者自行承担

4. **更新时效**: 本仓库仅包含历史版本，最新版本请以 [KDocs 官网](https://www.kdocs.cn/latest) 为准。

## 相关链接

- 🏠 [金山文档官网](https://www.kdocs.cn/latest)

## 贡献

如果您发现版本记录有误或希望补充历史版本，欢迎提交 Issue 或 PR。

## License

本项目仅作版本归档和学习交流使用，Skill 本身的版权归金山办公所有。

---

<p align="center">
  由 <a href="https://github.com/suge168">@suge168</a> 整理归档  
  <br>
  如有问题请通过 GitHub Issues 反馈
</p>
