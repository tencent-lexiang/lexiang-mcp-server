# Lexiang MCP Server

<p align="center">
  <img src="docs/images/lexiang-logo.png" alt="Lexiang MCP Server" width="200"/>
</p>

This project implements an [MCP server](https://spec.modelcontextprotocol.io/) for [Lexiang (乐享)](https://lexiangla.com) - Tencent's enterprise knowledge management platform.

The Lexiang MCP Server enables AI assistants to interact with your Lexiang knowledge bases, allowing you to search, read, create, and manage knowledge content directly through natural language conversations.

![MCP Demo](docs/images/mcp-demo.png)

---

## Features

- **Knowledge Management**: Create, read, update, and organize knowledge entries (pages, folders, files)
- **Team & Space Operations**: Access team information and manage knowledge spaces
- **Document Editing**: Edit online documents with block-level operations
- **Content Search**: Search across knowledge bases with keyword and semantic search
- **File Operations**: Upload, download, and manage files
- **Tencent Meeting Integration**: Import meeting recordings into knowledge bases
- **iWiki Import**: Import documents from iWiki to Lexiang

---

## Installation

### Prerequisites

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

---

## Available Tools

The Lexiang MCP Server provides **38 tools** organized into the following categories:

### Knowledge Entry Operations (11 tools)

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

### Document Block Operations (8 tools)

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

### Knowledge Space Operations (3 tools)

| Tool | Description |
|------|-------------|
| `knowledge_create_space` | Create a new knowledge space |
| `knowledge_describe_space` | Get knowledge space details |
| `knowledge_list_spaces` | List knowledge spaces in a team |

### File Operations (5 tools)

| Tool | Description |
|------|-------------|
| `knowledge_apply_upload` | Request file upload credentials (Step 1) |
| `knowledge_commit_upload` | Confirm file upload completion (Step 3) |
| `knowledge_create_hyperlink` | Import external links (e.g., WeChat articles) |
| `knowledge_describe_file` | Get file metadata |
| `knowledge_download_file` | Get file download URL |

### Search Operations (2 tools)

| Tool | Description |
|------|-------------|
| `search_kb_search` | Keyword search across knowledge bases |
| `search_kb_embedding_search` | Semantic vector search for content retrieval |

### Team Operations (3 tools)

| Tool | Description |
|------|-------------|
| `teamspace_describe_team` | Get team details |
| `teamspace_list_some_teams` | Get multiple teams' information |
| `teamspace_list_teams` | List accessible teams |

### Connector Operations (6 tools)

| Tool | Description |
|------|-------------|
| `connector_import_iwiki_doc` | Import iWiki documents to Lexiang |
| `connector_describe_tx_meeting_record` | Get Tencent Meeting recording details |
| `connector_import_tx_meeting_record` | Import Tencent Meeting recording |
| `connector_list_tx_meeting_records` | List meeting recordings (deprecated) |
| `connector_reload_tx_meeting_record` | Re-import meeting recording |
| `connector_search_tx_meeting_records` | Search meeting recordings by meeting ID |

---

## Usage Examples

### 1. Search and Read Knowledge

```text
Search for documents about "project planning" in my knowledge base
```

The AI will use `search_kb_search` to find relevant documents and `knowledge_describe_ai_parse_content` to read their content.

### 2. Create New Knowledge Entry

```text
Create a new page titled "Meeting Notes - Q1 Review" in the "Team Documents" space
```

The AI will:
1. Use `teamspace_list_teams` to find your team
2. Use `knowledge_list_spaces` to find the "Team Documents" space
3. Use `knowledge_create_entry` to create the new page

### 3. Import Content

```text
Create a page with the following markdown content:
# Project Overview
- Goal: Launch new feature
- Timeline: 2 weeks
- Team: 5 members
```

### 4. Organize Knowledge

```text
Move the "Archive" folder under the "2024 Projects" folder
```

### 5. Import Meeting Recording

```text
Import the Tencent Meeting recording with meeting ID 123456789 to my knowledge base
```

---

## URL Patterns

When working with Lexiang content, you can reference items using these URL patterns:

| Resource Type | URL Pattern |
|--------------|-------------|
| Knowledge Space | `https://{domain}/spaces/{space_id}` |
| Page/Entry | `https://{domain}/pages/{entry_id}` |
| Team Homepage | `https://{domain}/t/{team_id}/spaces` |

---

## File Upload Workflow

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

---

## Security Considerations

- Your MCP server URL contains your authentication credentials
- Do not share your MCP configuration publicly
- The server respects your Lexiang permissions - you can only access content you have permission to view/edit

---

## Troubleshooting

### Common Issues

**Q: I get "Authorization Required" errors**

A: Make sure you have:
1. Logged into Lexiang and obtained your MCP URL from [https://lexiangla.com/mcp](https://lexiangla.com/mcp)
2. Used the correct URL with your `company_from` parameter

**Q: I can't find my knowledge spaces**

A: The MCP server only shows spaces you have access to. Check your permissions in Lexiang.

**Q: File upload fails**

A: Ensure you complete all 3 steps of the upload workflow. Step 2 (HTTP PUT) must be done outside of MCP.

---

## Related Resources

- [Lexiang Official Website](https://lexiangla.com)
- [Lexiang MCP Configuration](https://lexiangla.com/mcp)
- [MCP Protocol Specification](https://spec.modelcontextprotocol.io/)
- [Model Context Protocol](https://modelcontextprotocol.io/)

---

## Support

For issues related to:
- **Lexiang platform**: Contact Lexiang support through the platform
- **MCP protocol**: See [MCP documentation](https://modelcontextprotocol.io/)

---

## License

This MCP server is provided by Tencent Lexiang team. Usage is subject to Lexiang's terms of service.
