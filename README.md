# Lexiang MCP Server

<!-- Logo placeholder - add docs/images/lexiang-logo.png later -->
<!-- <p align="center">
  <img src="docs/images/lexiang-logo.png" alt="Lexiang MCP Server" width="200"/>
</p> -->

<p align="center">
  <a href="#english">English</a> | <a href="#中文">中文</a>
</p>

---

<a name="english"></a>
## English

This project implements an [MCP server](https://spec.modelcontextprotocol.io/) for [Lexiang (乐享)](https://lexiangla.com) - Tencent's enterprise knowledge management platform.

The Lexiang MCP Server enables AI assistants to interact with your Lexiang knowledge bases, allowing you to search, read, create, and manage knowledge content directly through natural language conversations.

<!-- Demo image placeholder - add docs/images/mcp-demo.png later -->
<!-- ![MCP Demo](docs/images/mcp-demo.png) -->

### Features

- **Knowledge Management**: Create, read, update, and organize knowledge entries (pages, folders, files)
- **Team & Space Operations**: Access team information and manage knowledge spaces
- **Document Editing**: Edit online documents with block-level operations
- **Content Search**: Search across knowledge bases with keyword and semantic search
- **File Operations**: Upload, download, and manage files
- **Tencent Meeting Integration**: Import meeting recordings into knowledge bases
- **iWiki Import**: Import documents from iWiki to Lexiang

### Installation

#### Prerequisites

Before configuring the MCP client, you need to obtain your Lexiang MCP server URL with authentication.

#### Step 1: Get Your MCP Server URL

1. Visit [https://lexiangla.com/mcp](https://lexiangla.com/mcp) and log in with your Lexiang account
2. Follow the instructions to generate your personalized MCP server URL
3. Your URL will look like: `https://mcp.lexiang-app.com/mcp?company_from=YOUR_COMPANY_ID`

#### Step 2: Configure Your MCP Client

##### CodeBuddy / Cursor / Claude Desktop

Add the following to your MCP configuration file:

- **CodeBuddy**: `.codebuddy/mcp.json` in your project or `~/.codebuddy/mcp.json` for global config
- **Cursor**: `.cursor/mcp.json`
- **Claude Desktop**: 
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

> **Note**: Replace `YOUR_COMPANY_ID` with your actual company identifier from the Lexiang MCP configuration page.

##### VS Code with MCP Extension

Add to your VS Code settings or workspace `.vscode/settings.json`:

```json
{
  "mcp.servers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=YOUR_COMPANY_ID"
    }
  }
}
```

### Available Tools

The Lexiang MCP Server provides **38 tools** organized into the following categories:

#### Knowledge Entry Operations (11 tools)

| Tool | Description |
|------|-------------|
| `knowledge_create_entry` | Create knowledge entries (page/folder) |
| `knowledge_describe_entry` | Get knowledge entry details |
| `knowledge_describe_ai_parse_content` | Get AI-parseable content (HTML/Markdown/OCR) |
| `knowledge_diff_entry_content` | Compare content versions |
| `knowledge_import_content` | Import content in markdown/html format |
| `knowledge_list_children` | List child entries of a node |
| `knowledge_list_latest_entries` | Get recently updated entries |
| `knowledge_list_parents` | Get breadcrumb path to entry |
| `knowledge_move_entry` | Move entry to new location |
| `knowledge_rename_entry` | Rename an entry |
| `knowledge_search_udf_entries` | Search entries in a knowledge space |

#### Document Block Operations (8 tools)

| Tool | Description |
|------|-------------|
| `block_create_block_descendant` | Create child blocks under a parent block |
| `block_delete_block` | Delete a block and its children |
| `block_delete_block_children` | Delete specific child blocks |
| `block_describe_block` | Get block details |
| `block_list_block_children` | List child blocks |
| `block_move_blocks` | Move blocks to new position |
| `block_update_block` | Update block content or style |
| `block_update_blocks` | Batch update multiple blocks |

#### Knowledge Space Operations (3 tools)

| Tool | Description |
|------|-------------|
| `knowledge_create_space` | Create a new knowledge space |
| `knowledge_describe_space` | Get knowledge space details |
| `knowledge_list_spaces` | List knowledge spaces in a team |

#### File Operations (5 tools)

| Tool | Description |
|------|-------------|
| `knowledge_apply_upload` | Request file upload credentials (Step 1) |
| `knowledge_commit_upload` | Confirm file upload completion (Step 3) |
| `knowledge_create_hyperlink` | Import external links (e.g., WeChat articles) |
| `knowledge_describe_file` | Get file metadata |
| `knowledge_download_file` | Get file download URL |

#### Search Operations (2 tools)

| Tool | Description |
|------|-------------|
| `search_kb_search` | Keyword search across knowledge bases |
| `search_kb_embedding_search` | Semantic vector search for content retrieval |

#### Team Operations (3 tools)

| Tool | Description |
|------|-------------|
| `teamspace_describe_team` | Get team details |
| `teamspace_list_some_teams` | Get multiple teams' information |
| `teamspace_list_teams` | List accessible teams |

#### Connector Operations (6 tools)

| Tool | Description |
|------|-------------|
| `connector_import_iwiki_doc` | Import iWiki documents to Lexiang |
| `connector_describe_tx_meeting_record` | Get Tencent Meeting recording details |
| `connector_import_tx_meeting_record` | Import Tencent Meeting recording |
| `connector_list_tx_meeting_records` | List meeting recordings (deprecated) |
| `connector_reload_tx_meeting_record` | Re-import meeting recording |
| `connector_search_tx_meeting_records` | Search meeting recordings by meeting ID |

### Usage Examples

#### 1. Search and Read Knowledge

```text
Search for documents about "project planning" in my knowledge base
```

The AI will use `search_kb_search` to find relevant documents and `knowledge_describe_ai_parse_content` to read their content.

#### 2. Create New Knowledge Entry

```text
Create a new page titled "Meeting Notes - Q1 Review" in the "Team Documents" space
```

The AI will:
1. Use `teamspace_list_teams` to find your team
2. Use `knowledge_list_spaces` to find the "Team Documents" space
3. Use `knowledge_create_entry` to create the new page

#### 3. Import Content

```text
Create a page with the following markdown content:
# Project Overview
- Goal: Launch new feature
- Timeline: 2 weeks
- Team: 5 members
```

#### 4. Organize Knowledge

```text
Move the "Archive" folder under the "2024 Projects" folder
```

#### 5. Import Meeting Recording

```text
Import the Tencent Meeting recording with meeting ID 123456789 to my knowledge base
```

### URL Patterns

When working with Lexiang content, you can reference items using these URL patterns:

| Resource Type | URL Pattern |
|--------------|-------------|
| Knowledge Space | `https://{domain}/spaces/{space_id}` |
| Page/Entry | `https://{domain}/pages/{entry_id}` |
| Team Homepage | `https://{domain}/t/{team_id}/spaces` |

### File Upload Workflow

Uploading files requires a 3-step process:

1. **Step 1**: Call `knowledge_apply_upload` to get upload credentials and URL
2. **Step 2**: Upload file content to the returned `upload_url` using HTTP PUT (outside MCP)
3. **Step 3**: Call `knowledge_commit_upload` to confirm upload completion

```text
# Example: Upload a new file
1. apply_upload → returns session_id and upload_url
2. HTTP PUT file content to upload_url
3. commit_upload with session_id → returns entry details
```

### Security Considerations

- Your MCP server URL contains your authentication credentials
- Do not share your MCP configuration publicly
- The server respects your Lexiang permissions - you can only access content you have permission to view/edit

### Troubleshooting

#### Common Issues

**Q: I get "Authorization Required" errors**

A: Make sure you have:
1. Logged into Lexiang and obtained your MCP URL from [https://lexiangla.com/mcp](https://lexiangla.com/mcp)
2. Used the correct URL with your `company_from` parameter

**Q: I can't find my knowledge spaces**

A: The MCP server only shows spaces you have access to. Check your permissions in Lexiang.

**Q: File upload fails**

A: Ensure you complete all 3 steps of the upload workflow. Step 2 (HTTP PUT) must be done outside of MCP.

---

<a name="中文"></a>
## 中文

本项目为 [乐享](https://lexiangla.com)（腾讯企业知识管理平台）实现了 [MCP 服务器](https://spec.modelcontextprotocol.io/)。

乐享 MCP Server 使 AI 助手能够与您的乐享知识库进行交互，让您可以通过自然语言对话直接搜索、阅读、创建和管理知识内容。

<!-- Demo image placeholder - add docs/images/mcp-demo.png later -->
<!-- ![MCP 演示](docs/images/mcp-demo.png) -->

### 功能特性

- **知识管理**：创建、阅读、更新和组织知识条目（页面、文件夹、文件）
- **团队与空间操作**：访问团队信息和管理知识库
- **文档编辑**：通过块级操作编辑在线文档
- **内容搜索**：支持关键词搜索和语义向量搜索
- **文件操作**：上传、下载和管理文件
- **腾讯会议集成**：将会议录制导入知识库
- **iWiki 导入**：将 iWiki 文档导入乐享

### 安装配置

#### 前置条件

在配置 MCP 客户端之前，您需要获取带有身份验证的乐享 MCP 服务器 URL。

#### 第一步：获取 MCP 服务器 URL

1. 访问 [https://lexiangla.com/mcp](https://lexiangla.com/mcp) 并使用您的乐享账号登录
2. 按照说明生成您的个人 MCP 服务器 URL
3. 您的 URL 格式类似：`https://mcp.lexiang-app.com/mcp?company_from=您的企业ID`

#### 第二步：配置 MCP 客户端

##### CodeBuddy / Cursor / Claude Desktop

将以下内容添加到您的 MCP 配置文件中：

- **CodeBuddy**：项目中的 `.codebuddy/mcp.json` 或全局配置 `~/.codebuddy/mcp.json`
- **Cursor**：`.cursor/mcp.json`
- **Claude Desktop**：
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

> **注意**：请将 `您的企业ID` 替换为从乐享 MCP 配置页面获取的实际企业标识符。

##### VS Code MCP 扩展

添加到 VS Code 设置或工作区 `.vscode/settings.json`：

```json
{
  "mcp.servers": {
    "lexiang": {
      "url": "https://mcp.lexiang-app.com/mcp?company_from=您的企业ID"
    }
  }
}
```

### 可用工具

乐享 MCP Server 提供 **38 个工具**，分为以下类别：

#### 知识条目操作（11 个工具）

| 工具 | 描述 |
|------|------|
| `knowledge_create_entry` | 创建知识条目（页面/文件夹） |
| `knowledge_describe_entry` | 获取知识条目详情 |
| `knowledge_describe_ai_parse_content` | 获取 AI 可解析内容（HTML/Markdown/OCR） |
| `knowledge_diff_entry_content` | 对比内容版本差异 |
| `knowledge_import_content` | 导入 markdown/html 格式内容 |
| `knowledge_list_children` | 列出节点的子条目 |
| `knowledge_list_latest_entries` | 获取最近更新的条目 |
| `knowledge_list_parents` | 获取条目的面包屑路径 |
| `knowledge_move_entry` | 移动条目到新位置 |
| `knowledge_rename_entry` | 重命名条目 |
| `knowledge_search_udf_entries` | 在知识库中搜索条目 |

#### 文档块操作（8 个工具）

| 工具 | 描述 |
|------|------|
| `block_create_block_descendant` | 在父块下创建子块 |
| `block_delete_block` | 删除块及其子块 |
| `block_delete_block_children` | 删除指定的子块 |
| `block_describe_block` | 获取块详情 |
| `block_list_block_children` | 列出子块 |
| `block_move_blocks` | 移动块到新位置 |
| `block_update_block` | 更新块内容或样式 |
| `block_update_blocks` | 批量更新多个块 |

#### 知识库操作（3 个工具）

| 工具 | 描述 |
|------|------|
| `knowledge_create_space` | 创建新知识库 |
| `knowledge_describe_space` | 获取知识库详情 |
| `knowledge_list_spaces` | 列出团队下的知识库 |

#### 文件操作（5 个工具）

| 工具 | 描述 |
|------|------|
| `knowledge_apply_upload` | 申请文件上传凭证（第 1 步） |
| `knowledge_commit_upload` | 确认文件上传完成（第 3 步） |
| `knowledge_create_hyperlink` | 导入外部链接（如微信公众号文章） |
| `knowledge_describe_file` | 获取文件元信息 |
| `knowledge_download_file` | 获取文件下载地址 |

#### 搜索操作（2 个工具）

| 工具 | 描述 |
|------|------|
| `search_kb_search` | 关键词搜索知识库 |
| `search_kb_embedding_search` | 语义向量搜索，用于内容召回 |

#### 团队操作（3 个工具）

| 工具 | 描述 |
|------|------|
| `teamspace_describe_team` | 获取团队详情 |
| `teamspace_list_some_teams` | 批量获取团队信息 |
| `teamspace_list_teams` | 列出可访问的团队 |

#### 连接器操作（6 个工具）

| 工具 | 描述 |
|------|------|
| `connector_import_iwiki_doc` | 将 iWiki 文档导入乐享 |
| `connector_describe_tx_meeting_record` | 获取腾讯会议录制详情 |
| `connector_import_tx_meeting_record` | 导入腾讯会议录制 |
| `connector_list_tx_meeting_records` | 列出会议录制（已废弃） |
| `connector_reload_tx_meeting_record` | 重新导入会议录制 |
| `connector_search_tx_meeting_records` | 按会议号搜索会议录制 |

### 使用示例

#### 1. 搜索和阅读知识

```text
在知识库中搜索关于"项目规划"的文档
```

AI 将使用 `search_kb_search` 查找相关文档，并使用 `knowledge_describe_ai_parse_content` 读取内容。

#### 2. 创建新知识条目

```text
在"团队文档"空间中创建一个名为"会议纪要 - Q1 回顾"的新页面
```

AI 将：
1. 使用 `teamspace_list_teams` 查找您的团队
2. 使用 `knowledge_list_spaces` 查找"团队文档"空间
3. 使用 `knowledge_create_entry` 创建新页面

#### 3. 导入内容

```text
创建一个包含以下 markdown 内容的页面：
# 项目概述
- 目标：发布新功能
- 时间线：2 周
- 团队：5 人
```

#### 4. 组织知识

```text
将"归档"文件夹移动到"2024 项目"文件夹下
```

#### 5. 导入会议录制

```text
将会议号为 123456789 的腾讯会议录制导入到我的知识库
```

### URL 格式

使用乐享内容时，可以使用以下 URL 格式引用资源：

| 资源类型 | URL 格式 |
|---------|---------|
| 知识库 | `https://{domain}/spaces/{space_id}` |
| 页面/条目 | `https://{domain}/pages/{entry_id}` |
| 团队首页 | `https://{domain}/t/{team_id}/spaces` |

### 文件上传流程

上传文件需要 3 步操作：

1. **第 1 步**：调用 `knowledge_apply_upload` 获取上传凭证和 URL
2. **第 2 步**：使用 HTTP PUT 将文件内容上传到返回的 `upload_url`（在 MCP 外部完成）
3. **第 3 步**：调用 `knowledge_commit_upload` 确认上传完成

```text
# 示例：上传新文件
1. apply_upload → 返回 session_id 和 upload_url
2. HTTP PUT 文件内容到 upload_url
3. commit_upload 传入 session_id → 返回条目详情
```

### 安全注意事项

- 您的 MCP 服务器 URL 包含身份验证凭据
- 请勿公开分享您的 MCP 配置
- 服务器遵循您的乐享权限设置 - 您只能访问有权查看/编辑的内容

### 常见问题

**问：出现"需要授权"错误**

答：请确保：
1. 已登录乐享并从 [https://lexiangla.com/mcp](https://lexiangla.com/mcp) 获取 MCP URL
2. 使用了包含正确 `company_from` 参数的 URL

**问：找不到我的知识库**

答：MCP 服务器只显示您有权访问的空间。请在乐享中检查您的权限设置。

**问：文件上传失败**

答：请确保完成上传流程的所有 3 个步骤。第 2 步（HTTP PUT）必须在 MCP 外部完成。

---

## Related Resources / 相关资源

- [Lexiang Official Website / 乐享官网](https://lexiangla.com)
- [Lexiang MCP Configuration / 乐享 MCP 配置](https://lexiangla.com/mcp)
- [MCP Protocol Specification / MCP 协议规范](https://spec.modelcontextprotocol.io/)
- [Model Context Protocol](https://modelcontextprotocol.io/)

---

## Support / 支持

For issues related to / 如有问题请联系：
- **Lexiang platform / 乐享平台问题**：Contact Lexiang support through the platform / 通过平台联系乐享支持
- **MCP protocol / MCP 协议问题**：See [MCP documentation](https://modelcontextprotocol.io/) / 参见 MCP 文档

---

## License / 许可证

This MCP server is provided by Tencent Lexiang team. Usage is subject to Lexiang's terms of service.

本 MCP 服务器由腾讯乐享团队提供。使用须遵守乐享服务条款。
