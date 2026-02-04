# Lexiang MCP Server

<!-- Logo placeholder - add docs/images/lexiang-logo.png later -->
<!-- <p align="center">
  <img src="docs/images/lexiang-logo.png" alt="Lexiang MCP Server" width="200"/>
</p> -->

<p align="center">
  <a href="#中文">中文</a> | <a href="#english">English</a>
</p>

---

<a name="中文"></a>
## 中文

### 关于乐享

[腾讯乐享](https://lexiang.tencent.com/) 是**更懂企业的 AI 知识库**，通过 AI 技术激活团队私有知识价值，让知识触手可及。

**核心能力：**

- 🤖 **AI 智能问答**：锁定专属知识域，通过 AI 问答快速找到业务上下文
- 📚 **多格式全兼容**：支持文档、音视频、表格、图片等百余种格式
- 🔗 **多源知识入库**：聚合 Confluence、SharePoint、网盘及本地文件
- 👥 **轻松协作**：多人在线编辑，任务即时下发，知识与业务紧密关联
- 🔒 **安全可控**：四级权限管控、防泄露水印、操作可追溯

### 什么是 Lexiang MCP

Lexiang MCP 是乐享提供的 [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) 服务，让 AI 助手能够直接与您的乐享知识库进行交互。

通过 Lexiang MCP，您可以在 AI 对话中：

- 🔍 **搜索知识**：在知识库中搜索文档和内容
- 📖 **阅读内容**：获取文档、页面的详细内容
- ✏️ **创建编辑**：创建新页面、编辑文档内容
- 📁 **管理组织**：移动、重命名、组织知识结构
- 📎 **文件操作**：上传、下载文件
- 🎥 **会议导入**：将腾讯会议录制导入知识库

### 快速开始

#### 第一步：获取 MCP 服务地址

1. 访问 [https://lexiangla.com/mcp](https://lexiangla.com/mcp) 并登录您的乐享账号
2. 按照页面指引生成您的专属 MCP 服务地址
3. 您的地址格式类似：`https://mcp.lexiang-app.com/mcp?company_from=您的企业ID`

#### 第二步：配置 AI 客户端

##### CodeBuddy

在项目根目录创建 `.codebuddy/mcp.json`，或全局配置 `~/.codebuddy/mcp.json`：

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=您的企业ID"
    }
  }
}
```

##### Cursor

编辑 `.cursor/mcp.json`：

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=您的企业ID"
    }
  }
}
```

##### Claude Desktop

编辑配置文件：
- macOS：`~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows：`%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=您的企业ID"
    }
  }
}
```

> **注意**：请将 `您的企业ID` 替换为从乐享 MCP 配置页面获取的实际值。

### 使用示例

配置完成后，您可以直接在 AI 对话中操作乐享知识库：

#### 搜索知识

```
帮我搜索知识库中关于"产品规划"的文档
```

#### 创建页面

```
在"团队文档"空间中创建一个名为"Q1 会议纪要"的新页面
```

#### 导入内容

```
创建一个页面，内容如下：
# 项目概述
- 目标：发布新功能
- 时间线：2 周
- 团队：5 人
```

#### 整理知识

```
把"归档"文件夹移动到"2024 项目"下面
```

#### 导入会议录制

```
把会议号 123456789 的腾讯会议录制导入到知识库
```

### 可用工具列表

Lexiang MCP 提供 **38 个工具**，覆盖以下场景：

| 分类 | 工具数 | 说明 |
|-----|-------|------|
| 知识条目操作 | 11 | 创建、查看、编辑、移动、搜索知识条目 |
| 文档块操作 | 8 | 在线文档的块级编辑操作 |
| 知识库操作 | 3 | 创建和管理知识库 |
| 文件操作 | 5 | 文件上传、下载、外链导入 |
| 搜索操作 | 2 | 关键词搜索和语义搜索 |
| 团队操作 | 3 | 获取团队信息 |
| 连接器 | 6 | 腾讯会议、iWiki 等外部内容导入 |

<details>
<summary>📋 点击查看完整工具列表</summary>

#### 知识条目操作

| 工具 | 描述 |
|------|------|
| `knowledge_create_entry` | 创建知识条目（页面/文件夹） |
| `knowledge_describe_entry` | 获取知识条目详情 |
| `knowledge_describe_ai_parse_content` | 获取 AI 可解析内容 |
| `knowledge_diff_entry_content` | 对比内容版本差异 |
| `knowledge_import_content` | 导入 markdown/html 内容 |
| `knowledge_list_children` | 列出子条目 |
| `knowledge_list_latest_entries` | 获取最近更新的条目 |
| `knowledge_list_parents` | 获取面包屑路径 |
| `knowledge_move_entry` | 移动条目 |
| `knowledge_rename_entry` | 重命名条目 |
| `knowledge_search_udf_entries` | 搜索条目 |

#### 文档块操作

| 工具 | 描述 |
|------|------|
| `block_create_block_descendant` | 创建子块 |
| `block_delete_block` | 删除块 |
| `block_delete_block_children` | 删除子块 |
| `block_describe_block` | 获取块详情 |
| `block_list_block_children` | 列出子块 |
| `block_move_blocks` | 移动块 |
| `block_update_block` | 更新块内容 |
| `block_update_blocks` | 批量更新块 |

#### 知识库操作

| 工具 | 描述 |
|------|------|
| `knowledge_create_space` | 创建知识库 |
| `knowledge_describe_space` | 获取知识库详情 |
| `knowledge_list_spaces` | 列出知识库 |

#### 文件操作

| 工具 | 描述 |
|------|------|
| `knowledge_apply_upload` | 申请上传凭证 |
| `knowledge_commit_upload` | 确认上传完成 |
| `knowledge_create_hyperlink` | 导入外部链接 |
| `knowledge_describe_file` | 获取文件信息 |
| `knowledge_download_file` | 获取下载地址 |

#### 搜索操作

| 工具 | 描述 |
|------|------|
| `search_kb_search` | 关键词搜索 |
| `search_kb_embedding_search` | 语义向量搜索 |

#### 团队操作

| 工具 | 描述 |
|------|------|
| `teamspace_describe_team` | 获取团队详情 |
| `teamspace_list_some_teams` | 批量获取团队 |
| `teamspace_list_teams` | 列出可访问团队 |

#### 连接器

| 工具 | 描述 |
|------|------|
| `connector_import_iwiki_doc` | 导入 iWiki 文档 |
| `connector_describe_tx_meeting_record` | 获取会议录制详情 |
| `connector_import_tx_meeting_record` | 导入会议录制 |
| `connector_list_tx_meeting_records` | 列出会议录制 |
| `connector_reload_tx_meeting_record` | 重新导入录制 |
| `connector_search_tx_meeting_records` | 搜索会议录制 |

</details>

### 常见问题

**问：出现"需要授权"错误怎么办？**

答：请确保已从 [https://lexiangla.com/mcp](https://lexiangla.com/mcp) 获取正确的 MCP 服务地址，并检查 URL 中的 `company_from` 参数是否正确。

**问：找不到我的知识库？**

答：MCP 只能访问您有权限的知识库，请在乐享中检查您的权限设置。

**问：文件上传失败？**

答：文件上传需要 3 步：① 调用 `apply_upload` 获取上传地址 → ② HTTP PUT 上传文件 → ③ 调用 `commit_upload` 确认。第 2 步需要在 MCP 外部完成。

### 相关链接

- [乐享官网](https://lexiang.tencent.com/)
- [乐享 MCP 配置](https://lexiangla.com/mcp)
- [MCP 协议规范](https://spec.modelcontextprotocol.io/)

---

<a name="english"></a>
## English

### About Lexiang

[Tencent Lexiang](https://lexiang.tencent.com/) is an **AI-powered enterprise knowledge base** that activates the value of team knowledge through AI technology, making knowledge accessible at your fingertips.

**Core Capabilities:**

- 🤖 **AI Q&A**: Lock into your dedicated knowledge domain and quickly find business context through AI
- 📚 **Multi-format Support**: Supports 100+ formats including documents, audio/video, spreadsheets, and images
- 🔗 **Multi-source Integration**: Aggregate knowledge from Confluence, SharePoint, cloud drives, and local files
- 👥 **Easy Collaboration**: Real-time co-editing, instant task assignment, seamlessly integrated with business workflows
- 🔒 **Secure & Controllable**: Four-level access control, anti-leak watermarks, auditable operations

### What is Lexiang MCP

Lexiang MCP is a [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) service provided by Lexiang, enabling AI assistants to interact directly with your Lexiang knowledge bases.

With Lexiang MCP, you can perform the following in AI conversations:

- 🔍 **Search Knowledge**: Search documents and content in your knowledge bases
- 📖 **Read Content**: Get detailed content of documents and pages
- ✏️ **Create & Edit**: Create new pages and edit document content
- 📁 **Organize**: Move, rename, and organize knowledge structure
- 📎 **File Operations**: Upload and download files
- 🎥 **Import Meetings**: Import Tencent Meeting recordings to knowledge bases

### Quick Start

#### Step 1: Get Your MCP Server URL

1. Visit [https://lexiangla.com/mcp](https://lexiangla.com/mcp) and log in with your Lexiang account
2. Follow the instructions to generate your personalized MCP server URL
3. Your URL will look like: `https://mcp.lexiang-app.com/mcp?company_from=YOUR_COMPANY_ID`

#### Step 2: Configure Your AI Client

##### CodeBuddy

Create `.codebuddy/mcp.json` in your project root, or `~/.codebuddy/mcp.json` for global config:

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=YOUR_COMPANY_ID"
    }
  }
}
```

##### Cursor

Edit `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=YOUR_COMPANY_ID"
    }
  }
}
```

##### Claude Desktop

Edit the configuration file:
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=YOUR_COMPANY_ID"
    }
  }
}
```

> **Note**: Replace `YOUR_COMPANY_ID` with the actual value from the Lexiang MCP configuration page.

### Usage Examples

After configuration, you can interact with your Lexiang knowledge base directly in AI conversations:

#### Search Knowledge

```
Search for documents about "product planning" in my knowledge base
```

#### Create Page

```
Create a new page titled "Q1 Meeting Notes" in the "Team Documents" space
```

#### Import Content

```
Create a page with the following content:
# Project Overview
- Goal: Launch new feature
- Timeline: 2 weeks
- Team: 5 members
```

#### Organize Knowledge

```
Move the "Archive" folder under "2024 Projects"
```

#### Import Meeting Recording

```
Import the Tencent Meeting recording with meeting ID 123456789 to my knowledge base
```

### Available Tools

Lexiang MCP provides **38 tools** covering the following scenarios:

| Category | Count | Description |
|----------|-------|-------------|
| Knowledge Entry Operations | 11 | Create, view, edit, move, search knowledge entries |
| Document Block Operations | 8 | Block-level editing for online documents |
| Knowledge Space Operations | 3 | Create and manage knowledge spaces |
| File Operations | 5 | File upload, download, external link import |
| Search Operations | 2 | Keyword search and semantic search |
| Team Operations | 3 | Get team information |
| Connectors | 6 | Import from Tencent Meeting, iWiki, etc. |

<details>
<summary>📋 Click to view full tool list</summary>

#### Knowledge Entry Operations

| Tool | Description |
|------|-------------|
| `knowledge_create_entry` | Create knowledge entries (page/folder) |
| `knowledge_describe_entry` | Get knowledge entry details |
| `knowledge_describe_ai_parse_content` | Get AI-parseable content |
| `knowledge_diff_entry_content` | Compare content versions |
| `knowledge_import_content` | Import markdown/html content |
| `knowledge_list_children` | List child entries |
| `knowledge_list_latest_entries` | Get recently updated entries |
| `knowledge_list_parents` | Get breadcrumb path |
| `knowledge_move_entry` | Move entry |
| `knowledge_rename_entry` | Rename entry |
| `knowledge_search_udf_entries` | Search entries |

#### Document Block Operations

| Tool | Description |
|------|-------------|
| `block_create_block_descendant` | Create child blocks |
| `block_delete_block` | Delete block |
| `block_delete_block_children` | Delete child blocks |
| `block_describe_block` | Get block details |
| `block_list_block_children` | List child blocks |
| `block_move_blocks` | Move blocks |
| `block_update_block` | Update block content |
| `block_update_blocks` | Batch update blocks |

#### Knowledge Space Operations

| Tool | Description |
|------|-------------|
| `knowledge_create_space` | Create knowledge space |
| `knowledge_describe_space` | Get space details |
| `knowledge_list_spaces` | List spaces |

#### File Operations

| Tool | Description |
|------|-------------|
| `knowledge_apply_upload` | Request upload credentials |
| `knowledge_commit_upload` | Confirm upload completion |
| `knowledge_create_hyperlink` | Import external links |
| `knowledge_describe_file` | Get file metadata |
| `knowledge_download_file` | Get download URL |

#### Search Operations

| Tool | Description |
|------|-------------|
| `search_kb_search` | Keyword search |
| `search_kb_embedding_search` | Semantic vector search |

#### Team Operations

| Tool | Description |
|------|-------------|
| `teamspace_describe_team` | Get team details |
| `teamspace_list_some_teams` | Get multiple teams |
| `teamspace_list_teams` | List accessible teams |

#### Connectors

| Tool | Description |
|------|-------------|
| `connector_import_iwiki_doc` | Import iWiki documents |
| `connector_describe_tx_meeting_record` | Get meeting recording details |
| `connector_import_tx_meeting_record` | Import meeting recording |
| `connector_list_tx_meeting_records` | List meeting recordings |
| `connector_reload_tx_meeting_record` | Re-import recording |
| `connector_search_tx_meeting_records` | Search meeting recordings |

</details>

### FAQ

**Q: I get "Authorization Required" errors**

A: Make sure you have obtained the correct MCP server URL from [https://lexiangla.com/mcp](https://lexiangla.com/mcp) and verify the `company_from` parameter is correct.

**Q: I can't find my knowledge spaces**

A: MCP can only access spaces you have permission to. Check your permissions in Lexiang.

**Q: File upload fails**

A: File upload requires 3 steps: ① Call `apply_upload` to get upload URL → ② HTTP PUT the file → ③ Call `commit_upload` to confirm. Step 2 must be done outside of MCP.

### Related Links

- [Lexiang Official Website](https://lexiang.tencent.com/)
- [Lexiang MCP Configuration](https://lexiangla.com/mcp)
- [MCP Protocol Specification](https://spec.modelcontextprotocol.io/)

---

## License / 许可证

This documentation is provided by Tencent Lexiang team. Usage is subject to Lexiang's terms of service.

本文档由腾讯乐享团队提供，使用须遵守乐享服务条款。
