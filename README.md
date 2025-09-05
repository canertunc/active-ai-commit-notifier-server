# AI Commit Notifier Server

GitHub webhook processor that analyzes commits with OpenAI GPT-4 and sends notifications to Slack.

## 📁 Project Structure

```
active-ai-commit-notifier-server/
├── LICENSE                                                           
└── ai-commit-notifier/
    ├── src/
    │   ├── app.py                         # Main Flask application
    │   └── config.py                      # Configuration management
    ├── requirements.txt                   # Python dependencies
    ├── env.template                       # Environment variables template
    ├── Procfile                           # Heroku deployment configuration
    └── railway.toml                       # Railway deployment configuration
```

## 🚀 Quick Deploy

### Railway Deployment
1. Connect GitHub repository to Railway
2. Set environment variables (see below)
3. Deploy automatically

### Environment Variables
```env
SLACK_BOT_TOKEN=xoxb-your-bot-token-here
SLACK_CHANNELS=channel1,channel2
OPENAI_API_KEY=sk-proj-your-openai-key-here
REGEXP="\\b[Mm]erg(e|ed|ing)?\\b"
GITHUB_WEBHOOK_SECRET=your-webhook-secret-key
```

## 🔗 Related Projects

- **[Active MCP Server](https://github.com/canertunc/active-mcp-server)** - MCP server that triggers this notifier
- **[Active OAuth2 Server](https://github.com/canertunc/active-oauth2-server)** - OAuth2 authentication server

---
