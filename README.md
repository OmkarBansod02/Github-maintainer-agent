# GitHub Maintainer Bot

An intelligent AI-powered GitHub repository maintenance bot that automates contributor support, detects duplicate issues, learns from interactions, and provides comprehensive repository health monitoring through email notifications.

## 🚀 Features

- **📧 Email Notification Processing**: Automatically processes GitHub PR and issue notifications
- **🔍 Duplicate Issue Detection**: Intelligently groups similar bug reports using advanced similarity scoring
- **🧠 FAQ Learning System**: Builds knowledge base from past interactions for better future responses
- **⏰ Neglected PR Monitoring**: Tracks PRs and alerts maintainers for items needing attention (>7 days)
- **📊 Weekly Health Reports**: Generates comprehensive repository status reports with actionable insights
- **🌐 Web Search Integration**: Uses real-time web search for current repository intelligence
- **🤖 Professional Email Responses**: Sends properly formatted HTML emails with context-aware content

## 📋 Prerequisites

Before setting up the project, ensure you have:

- **Python 3.8+** installed on your system
- **Git** for version control
- **An AgentMail Account** - [Contact AgentMail](mailto:contact@agentmail.to) for API access
- **OpenAI API Key** - [Get yours here](https://platform.openai.com/api-keys)
- **ngrok Account** - [Sign up at ngrok.com](https://ngrok.com/) for webhook tunneling

## 🛠️ Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/YourUsername/AgentMail-PR_Bot.git
cd Github-maintainer-agent
```

### Step 2: Create Virtual Environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Environment Configuration

1. **Copy the example environment file:**
   ```bash
   cp .env.example .env
   ```

2. **Edit `.env` with your configuration:**
   ```env
   # AgentMail Configuration
   AGENTMAIL_API_KEY=your_agentmail_api_key_here
   OPENAI_API_KEY=your_openai_api_key_here

   # Inbox Configuration
   INBOX_USERNAME=maintainer
   WEBHOOK_DOMAIN=your-custom-domain.ngrok-free.app

   # Ngrok Configuration
   NGROK_AUTHTOKEN=your_ngrok_authtoken_here

   # Repository Monitoring
   TARGET_GITHUB_REPO=YourUsername/YourRepository
   REPORT_TARGET_EMAIL=your-email@example.com

   # Monitoring Schedule (in seconds)
   MONITORING_INTERVAL=604800
   ```

### Step 5: Get Required API Keys

#### AgentMail API Key
1. Contact AgentMail support at contact@agentmail.to
2. Request API access for your project
3. Add the provided API key to your `.env` file

#### OpenAI API Key
1. Visit [OpenAI Platform](https://platform.openai.com/api-keys)
2. Create a new API key
3. Add it to your `.env` file as `OPENAI_API_KEY`

#### ngrok Setup
1. Sign up at [ngrok.com](https://ngrok.com/)
2. Get your authtoken from the dashboard
3. Set up a custom domain (optional but recommended)
4. Add authtoken to `.env` as `NGROK_AUTHTOKEN`

## 🔧 Configuration Details

### Environment Variables Explained

| Variable | Description | Example |
|----------|-------------|---------|
| `AGENTMAIL_API_KEY` | Your AgentMail API key for email processing | `abc123...` |
| `OPENAI_API_KEY` | OpenAI API key for AI responses | `sk-proj-...` |
| `INBOX_USERNAME` | Username for your AgentMail inbox | `maintainer` |
| `WEBHOOK_DOMAIN` | Your ngrok domain for webhooks | `yourapp.ngrok-free.app` |
| `NGROK_AUTHTOKEN` | ngrok authentication token | `2a1b3c4d...` |
| `TARGET_GITHUB_REPO` | Repository to monitor (owner/repo format) | `microsoft/vscode` |
| `REPORT_TARGET_EMAIL` | Email address for health reports | `admin@company.com` |
| `MONITORING_INTERVAL` | Report frequency in seconds (604800 = 1 week) | `604800` |

### Repository Configuration Format

**❌ Incorrect:**
```
TARGET_GITHUB_REPO=https://github.com/owner/repo.git
```

**✅ Correct:**
```
TARGET_GITHUB_REPO=owner/repo
```

## 🚀 Running the Bot

### Start the Bot

```bash
python main.py
```

### Expected Output

```
Starting Advanced GitHub Maintainer Bot...
Target Repository: owner/repository
Report Email: your-email@example.com
Setting up AgentMail infrastructure...
Inbox maintainer@agentmail.to ready
ngrok tunnel: https://your-domain.ngrok-free.app
Webhook configured: https://your-domain.ngrok-free.app/webhooks
Bot ready! Inbox: maintainer@agentmail.to
Features: GitHub notifications, repository monitoring, automated reports
Starting repository monitoring thread...
Repository monitoring active - reports every 10080 minutes
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:8080
```

## 🧪 Testing the Bot

### Test 1: Email Response (Immediate)

1. Send a test email to your AgentMail inbox: `maintainer@agentmail.to`
2. Include GitHub-like content in the subject/body
3. Check terminal logs for webhook processing
4. Verify bot response in your email

### Test 2: Quick Health Report

For testing without waiting a week:

1. **Temporarily change monitoring interval:**
   ```bash
   # In .env file
   MONITORING_INTERVAL=120  # 2 minutes for testing
   ```

2. **Restart the bot**
3. **Wait 2 minutes** for the first report
4. **Check your configured email** for the health report
5. **Revert back to weekly:**
   ```bash
   MONITORING_INTERVAL=604800  # Back to 1 week
   ```

### Test 3: Duplicate Detection

1. Send an email with a bug report (e.g., "ImportError in main.py")
2. Send a similar issue with different wording
3. Second issue should be detected as duplicate
4. Verify consolidated response

### Test 4: GitHub Integration

1. **Configure GitHub Repository:**
   - Go to your repo → Settings → Notifications
   - Add `maintainer@agentmail.to` to notification emails
   
2. **Create test issue/PR** in your repository
3. **Monitor bot logs** for webhook processing
4. **Check for automated response** to contributor

## 📁 Project Structure

```
AgentMail-PR_Bot/
├── main.py                 # Main bot application
├── utils.py                # Utility functions for GitHub processing
├── System_prompt.txt       # Agent system prompt and behavior
├── requirements.txt        # Python dependencies
├── .env                    # Environment configuration (not in repo)
├── .env.example           # Example environment file
├── .gitignore             # Git ignore rules
├── README.md              # This file
└── maintiner-agent.md     # Detailed agent documentation
```

## 🔍 Features Deep Dive

### Duplicate Detection Algorithm

The bot uses sophisticated scoring based on:
- **Error Keywords** (TypeError, ImportError, etc.)
- **File Patterns** (matching file names/extensions)
- **Function Patterns** (similar function calls)
- **Semantic Similarity** (word overlap analysis)

### Learning System

- **FAQ Storage**: Builds knowledge base from email interactions
- **Pattern Recognition**: Identifies common contributor questions
- **Response Improvement**: Applies learned knowledge to future similar issues

### Health Reports Include

- 📊 Repository metrics and status
- 🚀 Recent commits and releases
- 🐛 Open issues and PR analysis
- 🔒 Security alerts and vulnerabilities
- 📈 Community engagement metrics
- ⚡ Actionable recommendations

## 🚨 Troubleshooting

### Common Issues

#### 1. Webhook Not Receiving Events
```bash
# Check ngrok tunnel status
curl https://your-domain.ngrok-free.app/webhooks

# Verify webhook configuration in AgentMail dashboard
# Ensure GitHub notifications are sent to correct email
```

#### 2. API Authentication Errors
```bash
# Verify API keys are correctly set
python -c "import os; from dotenv import load_dotenv; load_dotenv(); print('AgentMail:', bool(os.getenv('AGENTMAIL_API_KEY'))); print('OpenAI:', bool(os.getenv('OPENAI_API_KEY')))"
```

#### 3. No Health Reports Generated
- Check `TARGET_GITHUB_REPO` format (should be `owner/repo`, not full URL)
- Verify `REPORT_TARGET_EMAIL` is set correctly
- Monitor terminal logs for monitoring thread activity

#### 4. Duplicate Detection Not Working
- Ensure bot has processed some initial emails to build knowledge base
- Check FAQ knowledge storage in terminal logs
- Verify similar keywords/patterns in test issues

### Debug Mode

Add debug logging to main.py:
```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

### Log Analysis

Monitor these log messages:
- `[WEBHOOK]` - Incoming email processing
- `[MONITOR]` - Repository health monitoring
- `[DUPLICATE]` - Duplicate issue detection
- `[FAQ]` - Knowledge base updates

## 🔐 Security Considerations

- **Never commit `.env` file** - Contains sensitive API keys
- **Use environment variables** for all credentials
- **Regularly rotate API keys** - Update them periodically
- **Monitor bot responses** - Ensure no sensitive data exposure
- **Use ngrok authentication** - Secure your webhook endpoint

## 📈 Performance Optimization

### Production Recommendations

1. **Use a stable hosting service** instead of local development
2. **Configure proper logging** with log rotation
3. **Set up monitoring alerts** for bot health
4. **Implement rate limiting** for API calls
5. **Use database storage** for larger FAQ knowledge bases

### Scaling Considerations

- Consider Redis for FAQ knowledge storage at scale
- Implement database for PR tracking persistence
- Use message queues for high-volume repositories
- Add caching for repository information

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and test thoroughly
4. Commit changes: `git commit -m 'Add feature description'`
5. Push to branch: `git push origin feature-name`
6. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 Support

- **Issues**: Open a GitHub issue for bugs or feature requests
- **Questions**: Contact the development team
- **AgentMail Support**: contact@agentmail.to

---

**Ready to automate your GitHub repository management? Start with the installation steps above! 🚀**
