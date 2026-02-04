# Lexiang MCP Server

<p align="center">
  <a href="#中文">中文</a> | <a href="#english">English</a>
</p>

---

<a name="中文"></a>
## 中文

### 关于乐享

[腾讯乐享](https://lexiang.tencent.com/?event_type=link_exchange&event_channel=mcp&event_detail=github) 是**更懂企业的 AI 知识库**，通过 AI 技术激活团队私有知识价值，让知识触手可及。

**核心能力：**

- 🤖 **AI 智能问答**：锁定专属知识域，通过 AI 问答快速找下文
- 📚 **多格式全兼容**：支持文档、音视频、表格、图片等百余种格式
- 🔗 **多源知识入库**：聚合微信文件、微信公众号文章、腾讯会议、腾讯文档及本地文件入库
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

#### 第一步：获取 MCP 配置信息

1. 登录乐享后，访问 [https://lexiangla.com/mcp](https://lexiangla.com/mcp)
2. 页面会显示您的专属 MCP Server 配置信息：

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from={您的乐享code}"
    }
  }
}
```

> **说明**：`{您的乐享code}` 是您企业的唯一标识，从配置页面直接复制即可。

#### 第二步：配置 AI 客户端

##### CodeBuddy（推荐）

1. 打开 CodeBuddy，进入 MCP 配置
2. 添加乐享 MCP 配置信息（从第一步复制）
3. 点击「刷新」图标
4. 在弹窗中完成乐享 MCP Server **OAuth 授权**

配置文件位置：
- 项目级配置：`.codebuddy/mcp.json`
- 全局配置：`~/.codebuddy/mcp.json`

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from={您的乐享code}"
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
      "url": "https://mcp.lexiang-app.com/mcp?company_from={您的乐享code}"
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
      "url": "https://mcp.lexiang-app.com/mcp?company_from={您的乐享code}"
    }
  }
}
```

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

#### 更新版本日志

```
将本次更新，提交 github 仓库，同步更新到知识库版本更新日志中
```

> AI 会自动定位文档位置，在顶部插入新版本内容，历史记录原封不动。

#### 生成 API 文档

```
在同目录下，生成对应 API 文档，方便让其他系统调用
```

> AI 会分析代码中的接口结构，自动在乐享知识库中创建格式规范的 API 文档。

#### 导入会议录制

```
把会议号 123456789 的腾讯会议录制导入到知识库
```

### 为什么选择乐享知识库？

相比本地 Markdown 文件或其他在线文档工具，乐享知识库有几个独特优势：

1. **文档块（Block）级别的精准操作**
   - 本地文件只能全量覆盖，大部分在线文档只支持页面级操作
   - 乐享的 Block 设计让 AI 可以像"外科手术"一样精准更新文档任意位置
   - 对于版本日志、API 文档这种增量更新场景，这是刚需

2. **严肃场景下的文档审批**
   - 支持文档审批流，AI 生成的内容可先进入待审核状态
   - 经负责人确认后再正式发布，安全兜底

3. **一键分享，扩大影响力**
   - 便捷的文档共享，一个链接就能分享给客户、合作伙伴
   - 访问记录一目了然，支持点赞和评论

4. **AI 可二次消费的知识**
   - 文档不再是静态说明书，而是可被 AI 调用的"知识接口"
   - 在 CodeBuddy 中通过 MCP 直接读取 API 文档，自动完成接口集成

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

答：
1. 确保已从 [https://lexiangla.com/mcp](https://lexiangla.com/mcp) 获取正确的配置信息
2. 在 CodeBuddy 中点击「刷新」图标，完成 OAuth 授权
3. 检查 URL 中的 `company_from` 参数是否正确

**问：找不到我的知识库？**

答：MCP 只能访问您有权限的知识库，请在乐享中检查您的权限设置。

**问：文件上传失败？**

答：文件上传需要 3 步：
1. 调用 `apply_upload` 获取上传地址
2. HTTP PUT 上传文件（在 MCP 外部完成）
3. 调用 `commit_upload` 确认

**问：AI 更新文档时创建了新文档而不是更新原文档？**

答：可以明确告诉 AI："在原文档上进行更新，而不是生成新文档"，AI 会使用块级操作精准更新原文档。

### 相关链接

- [乐享官网](https://lexiang.tencent.com/?event_type=link_exchange&event_channel=mcp&event_detail=github)
- [乐享 MCP 配置页面](https://lexiangla.com/mcp)
- [MCP 协议规范](https://spec.modelcontextprotocol.io/)

---

<a name="english"></a>
## English

### About Lexiang

[Tencent Lexiang](https://lexiang.tencent.com/?event_type=link_exchange&event_channel=mcp&event_detail=github) is an **AI-powered enterprise knowledge base** that activates the value of team knowledge through AI technology, making knowledge accessible at your fingertips.

**Core Capabilities:**

- 🤖 **AI Q&A**: Lock into your dedicated knowledge domain and quickly find business context through AI
- 📚 **Multi-format Support**: Supports 100+ formats including documents, audio/video, spreadsheets, and images
- 🔗 **Multi-source Integration**: Aggregate WeChat files, WeChat Official Account articles, Tencent Meeting, Tencent Docs, and local files
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

#### Step 1: Get MCP Configuration

1. Log in to Lexiang, then visit [https://lexiangla.com/mcp](https://lexiangla.com/mcp)
2. The page will display your personalized MCP Server configuration:

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from={your_lexiang_code}"
    }
  }
}
```

> **Note**: `{your_lexiang_code}` is your company's unique identifier. Copy it directly from the configuration page.

#### Step 2: Configure Your AI Client

##### CodeBuddy (Recommended)

1. Open CodeBuddy and go to MCP configuration
2. Add the Lexiang MCP configuration (copied from Step 1)
3. Click the "Refresh" icon
4. Complete the **OAuth authorization** in the popup

Configuration file locations:
- Project-level: `.codebuddy/mcp.json`
- Global: `~/.codebuddy/mcp.json`

```json
{
  "mcpServers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from={your_lexiang_code}"
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
      "url": "https://mcp.lexiang-app.com/mcp?company_from={your_lexiang_code}"
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
      "url": "https://mcp.lexiang-app.com/mcp?company_from={your_lexiang_code}"
    }
  }
}
```

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

#### Update Version Log

```
Commit this update to github and sync to the version changelog in the knowledge base
```

> AI will automatically locate the document position and insert new version content at the top, keeping historical records intact.

#### Generate API Documentation

```
Generate API documentation in the same directory for other systems to call
```

> AI will analyze the interface structure in the code and automatically create well-formatted API documentation in Lexiang.

#### Import Meeting Recording

```
Import the Tencent Meeting recording with meeting ID 123456789 to my knowledge base
```

### Why Choose Lexiang Knowledge Base?

Compared to local Markdown files or other online document tools, Lexiang offers unique advantages:

1. **Block-level Precision Operations**
   - Local files can only be fully overwritten; most online docs only support page-level operations
   - Lexiang's Block design allows AI to precisely update any position in a document like "surgery"
   - Essential for incremental update scenarios like version logs and API documentation

2. **Document Approval for Serious Scenarios**
   - Supports document approval workflows; AI-generated content can enter pending review status
   - Officially published only after responsible person confirmation

3. **One-click Sharing**
   - Easy document sharing with a single link to customers and partners
   - Clear access records with like and comment features

4. **AI-consumable Knowledge**
   - Documents are no longer static manuals but "knowledge interfaces" callable by AI
   - Read API docs via MCP in CodeBuddy to automatically complete interface integration

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

A:
1. Make sure you obtained the correct configuration from [https://lexiangla.com/mcp](https://lexiangla.com/mcp)
2. Click the "Refresh" icon in CodeBuddy to complete OAuth authorization
3. Verify the `company_from` parameter in the URL is correct

**Q: I can't find my knowledge spaces**

A: MCP can only access spaces you have permission to. Check your permissions in Lexiang.

**Q: File upload fails**

A: File upload requires 3 steps:
1. Call `apply_upload` to get upload URL
2. HTTP PUT the file (done outside MCP)
3. Call `commit_upload` to confirm

**Q: AI created a new document instead of updating the original?**

A: You can explicitly tell AI: "Update the original document instead of creating a new one", and AI will use block-level operations to precisely update the original document.

### Related Links

- [Lexiang Official Website](https://lexiang.tencent.com/?event_type=link_exchange&event_channel=mcp&event_detail=github)
- [Lexiang MCP Configuration Page](https://lexiangla.com/mcp)
- [MCP Protocol Specification](https://spec.modelcontextprotocol.io/)

---

## License / 许可证

This documentation is provided by Tencent Lexiang team. Usage is subject to Lexiang's terms of service.

本文档由腾讯乐享团队提供，使用须遵守乐享服务条款。
