# AI Commit Notifier MCP Server

An MCP (Model Context Protocol) server that sends GitHub commit notifications to Slack through webhook integration. This server provides AI assistants with tools to notify about commits in a GitHub webhook format.

## 🚀 Features

- **MCP Protocol Support**: Full implementation of MCP JSON-RPC protocol
- **GitHub Webhook Integration**: Generates and sends GitHub-compatible webhook payloads
- **OAuth Authentication**: Secure token-based authentication system
- **Slack Notifications**: Sends commit notifications to Slack channels
- **AI Assistant Integration**: Designed to work with AI assistants like Claude Desktop
- **Cloud Ready**: Deployable on Railway, Heroku, and other cloud platforms

## 📁 Project Structure

```
active-mcp-server/
├── LICENSE                    
└── mcp_server/
    ├── server.py             # Main MCP server implementation
    ├── requirements.txt      # Python dependencies
    ├── Dockerfile            # Docker container configuration
    ├── start.sh              # Local development start script
    ├── Procfile              # Heroku deployment configuration
    ├── railway.json          # Railway deployment configuration
    └── railway.toml          # Railway build configuration
```

## 🛠️ Available Tools

### 1. `ai_commit_notifier_tool`
Sends AI-generated commit notifications in GitHub webhook format.

**Parameters:**
- `repo_name` (string): Repository name (e.g., "username/repo-name")
- `commit_message` (string): Commit message
- `commit_author` (string): Name of the commit author

### 2. `fetch_commit_info_tool`
Fetches commit information using access token validation.

**Parameters:** None (uses ACCESS_TOKEN from headers)

## 🔧 Installation & Setup

### Local Development

1. **Clone the repository:**
   ```bash
   git clone https://github.com/canertunc/active-mcp-server.git
   cd active-mcp-server/mcp_server
   ```

2. **Run the start script:**
   ```bash
   chmod +x start.sh
   ./start.sh
   ```

   The script will:
   - Create a virtual environment
   - Install dependencies
   - Load environment variables from `.env` if exists
   - Start the server on `http://localhost:3000`

### Manual Setup

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Start the server:**
   ```bash
   python server.py
   ```

## 🌐 Cloud Deployment

### Railway Deployment
The project includes Railway configuration files:
- `railway.json`: Deployment settings
- `railway.toml`: Build configuration

Deploy with one click or connect your GitHub repository to Railway.

### Docker Deployment
```bash
docker build -t ai-commit-notifier .
docker run -p 3000:3000 ai-commit-notifier
```

## 🔐 Authentication

The server uses OAuth-based authentication. To get an access token:

1. Visit the server's root URL (e.g., `https://your-server.railway.app/`)
2. Click "🔑 Yetki Ver & Token Al" button
3. Complete OAuth flow
4. Use the received token in your MCP client configuration

## 🧩 Claude Desktop Integration

Add this configuration to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "ai-commit-notifier": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://your-server.railway.app/mcp",
        "--header",
        "ACCESS_TOKEN:${ACCESS_TOKEN}"
      ],
      "env": {
        "ACCESS_TOKEN": "your_access_token_here"
      }
    }
  }
}
```

## 🔧 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port | `3000` |
| `HOST` | Server host | `0.0.0.0` |
| `WEBHOOK_URL` | Target webhook URL | `https://active-ai-commit-notifier-server-production.up.railway.app/github-webhook` |
| `GITHUB_WEBHOOK_SECRET` | GitHub webhook secret | Auto-generated |

## 📡 API Endpoints

- `POST /mcp` - Main MCP JSON-RPC endpoint
- `GET /` - Server info and OAuth setup page
- `GET /health` - Health check endpoint

## 🔄 MCP Protocol Methods

- `initialize` - Initialize MCP connection
- `tools/list` - List available tools
- `tools/call` - Execute tool functions

## 🧪 Testing

Test the server health:
```bash
curl http://localhost:3000/health
```

Test MCP initialization:
```bash
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{}}'
```

## 📦 Dependencies

- **FastAPI**: Modern web framework for APIs
- **Uvicorn**: ASGI server for FastAPI
- **httpx**: Async HTTP client
- **requests**: HTTP library for webhook calls
- **mcp**: Model Context Protocol implementation

## 📄 License

This project is licensed under the terms specified in the LICENSE file.

## 🔗 Related Services

This project works in conjunction with other services:

### OAuth2 Authentication Server
- **Repository**: [active-oauth2-server](https://github.com/canertunc/active-oauth2-server)
- **Live URL**: `https://caner-oauth-server.up.railway.app`
- **Purpose**: Handles OAuth2 authentication flow and token validation for MCP clients

### AI Commit Notifier Server
- **Repository**: [active-ai-commit-notifier-server](https://github.com/canertunc/active-ai-commit-notifier-server)
- **Live URL**: `https://active-ai-commit-notifier-server-production.up.railway.app`
- **Purpose**: Receives and processes GitHub webhook notifications for Slack integration

---
