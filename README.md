# mcp-meituan-ip MCP server

A dynamic MCP server management service that creates, runs, and manages Model Context Protocol (MCP) servers dynamically. This service itself functions as an MCP server and launches/manages other MCP servers as child processes, enabling a flexible MCP ecosystem.

<a href="https://glama.ai/mcp/servers/@aixi134/mcp-meituan-ip">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@aixi134/mcp-meituan-ip/badge" alt="mcp-meituan-ip MCP server" />
</a>

## Components

### Resources

The server implements a simple note storage system with:
- Custom note:// URI scheme for accessing individual notes
- Each note resource has a name, description and text/plain mimetype

### Prompts

The server provides a single prompt:
- summarize-notes: Creates summaries of all stored notes
  - Optional "style" argument to control detail level (brief/detailed)
  - Generates prompt combining all current notes with style preference

### Tools

The server implements one tool:
- add-note: Adds a new note to the server
  - Takes "name" and "content" as required string arguments
  - Updates server state and notifies clients of resource changes

## Configuration

[TODO: Add configuration details specific to your implementation]

## Quickstart

### Install

#### Claude Desktop

On MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

<details>
  <summary>Development/Unpublished Servers Configuration</summary>
  ```
  "mcpServers": {
    "mcp-meituan-ip": {
      "command": "uv",
      "args": [
        "--directory",
        "D:\idea-work\mcp-meituan-ip",
        "run",
        "mcp-meituan-ip"
      ]
    }
  }
  ```
</details>

<details>
  <summary>Published Servers Configuration</summary>
  ```
  "mcpServers": {
    "mcp-meituan-ip": {
      "command": "uvx",
      "args": [
        "mcp-meituan-ip"
      ]
    }
  }
  ```
</details>

## Development

### Building and Publishing

To prepare the package for distribution:

1. Sync dependencies and update lockfile:
```bash
uv sync
```

2. Build package distributions:
```bash
uv build
```

This will create source and wheel distributions in the `dist/` directory.

3. Publish to PyPI:
```bash
uv publish
```

Note: You'll need to set PyPI credentials via environment variables or command flags:
- Token: `--token` or `UV_PUBLISH_TOKEN`
- Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).

You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory D:\idea-work\mcp-meituan-ip run mcp-meituan-ip
```

Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.