# MCP 服务器简介

MCP（模型上下文协议）是一种开源协议，旨在为大规模语言模型（LLM）提供安全、受控的工具和数据访问。MCP服务器是实现这一协议的关键组件，它们使LLM能够与外部工具和数据源进行交互，且具备灵活的扩展性和安全控制。

该项目收集了一些参考实现和社区贡献的MCP服务器，展示了如何利用MCP协议扩展LLM的功能。每个MCP服务器都基于Typescript或Python的MCP SDK进行实现，便于与各种工具和平台进行集成。

## 🌟 精选服务器

这些服务器实现了不同的功能，使LLM能够访问和操作各种工具和数据源。以下是一些重要的服务器：

- **[Filesystem](src/filesystem)**：提供安全的文件操作功能，支持配置访问控制。
- **[GitHub](src/github)**：支持GitHub仓库管理、文件操作及GitHub API集成。
- **[GitLab](src/gitlab)**：提供与GitLab API的集成，支持项目管理。
- **[Git](src/git)**：为Git仓库提供阅读、搜索和操作工具。
- **[Google Drive](src/gdrive)**：提供Google Drive文件的访问和搜索功能。
- **[PostgreSQL](src/postgres)**：只读数据库访问，支持模式检查。
- **[Sqlite](src/sqlite)**：数据库交互和商业智能功能。
- **[Slack](src/slack)**：支持Slack频道管理和消息发送。
- **[Sentry](src/sentry)**：获取并分析来自Sentry.io的错误信息。
- **[Memory](src/memory)**：基于知识图谱的持久化记忆系统。
- **[Puppeteer](src/puppeteer)**：浏览器自动化和网页抓取。
- **[Brave Search](src/brave-search)**：使用Brave搜索API进行网页和本地搜索。
- **[Google Maps](src/google-maps)**：提供位置服务、导航和地点详情。
- **[Fetch](src/fetch)**：高效地抓取和转换网页内容，以便LLM使用。

## 🚀 开始使用 MCP 服务器

### 如何使用本项目中的 MCP 服务器

本项目提供了基于Typescript和Python的MCP服务器，使用时非常简单。

对于Typescript实现的服务器，可以直接使用`npx`启动。例如，启动[Memory](src/memory)服务器的命令如下：
```sh
npx -y @modelcontextprotocol/server-memory
```

对于Python实现的服务器，可以使用[`uvx`](https://docs.astral.sh/uv/concepts/tools/)或[`pip`](https://pypi.org/project/pip/)进行启动。推荐使用`uvx`，因为它更简便易用。

例如，启动[Git](src/git)服务器的命令如下：
```sh
# 使用 uvx
uvx mcp-server-git

# 使用 pip
pip install mcp-server-git
python -m mcp_server_git
```

你可以通过[这些安装指南](https://docs.astral.sh/uv/getting-started/installation/)安装`uv`/`uvx`，通过[这些指南](https://pip.pypa.io/en/stable/installation/)安装`pip`。

### 配置 MCP 客户端

虽然单独运行服务器是有用的，但更常见的做法是将服务器配置为MCP客户端。例如，以下是将[Memory](src/memory)服务器配置为Claude Desktop客户端的示例：

```json
{
  "mcpServers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    }
  }
}
```

另外，也可以通过类似下面的配置将其他服务器集成到MCP客户端：

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
    },
    "git": {
      "command": "uvx",
      "args": ["mcp-server-git", "--repository", "path/to/git/repo"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://localhost/mydb"]
    }
  }
}
```

## 🛠️ 创建自己的 MCP 服务器

如果你有兴趣创建自己的MCP服务器，可以访问[官方文档](https://modelcontextprotocol.io/introduction)，了解有关MCP服务器实现的详细指南和最佳实践。

## 🤝 贡献

如果你有兴趣为该项目做出贡献，请查看[贡献指南](CONTRIBUTING.md)了解更多信息。

## 🔒 安全

有关安全漏洞报告的更多信息，请参见[安全文档](SECURITY.md)。

## 📜 许可

本项目使用MIT许可证，详细信息请查看[LICENSE](LICENSE)文件。

## 💬 社区

- [GitHub 讨论区](https://github.com/orgs/modelcontextprotocol/discussions)

## ⭐ 支持

如果你发现MCP服务器有用，请考虑给这个仓库加星并贡献新的服务器或改进！

---

该项目由Anthropic管理，并由社区共同开发。MCP是一个开源协议，我们鼓励大家贡献自己的服务器和改进！