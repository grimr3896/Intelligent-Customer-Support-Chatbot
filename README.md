
# 🤖 Intelligent Customer Support Chatbot

A powerful, multi-channel customer support automation system built with n8n that uses AI to handle inquiries, automate ticketing, and escalate issues when needed.

## ✨ Features

- **Multi-Channel Support**: Handle web chat, WhatsApp, and email inquiries
- **AI-Powered Responses**: OpenAI GPT integration for intelligent replies
- **Automated Ticketing**: Create and track tickets in Airtable
- **Smart Escalation**: Auto-escalate high-priority issues to human agents
- **CRM Integration**: Update customer records automatically
- **Analytics Dashboard**: Track performance with Google Sheets/Data Studio
- **Follow-up Automation**: Send confirmation emails and updates

## 🚀 Quick Start

### Prerequisites
- [n8n account](https://n8n.cloud/) (cloud or self-hosted)
- [OpenAI API key](https://platform.openai.com/api-keys)
- [Airtable account](https://airtable.com/)
- [Google Account](https://accounts.google.com/)

### Installation

1. **Import the workflow**:
   - Download `chatbot-workflow.json`
   - In n8n: Workflows → New → Import from File
   - Select the JSON file

2. **Set up credentials**:
   - Click each node and add required API credentials
   - Configure:
     - OpenAI API (for GPT responses)
     - Airtable (for ticketing)
     - Google Sheets (for logging)
     - Email/SMTP (for notifications)

3. **Configure Airtable**:
   ```bash
   Create a base named "Support Tickets" with columns:
   - Ticket ID, Customer ID, Customer Message, Intent
   - Priority, Status, Assigned To, Created At
   - Channel, AI Response
   ```

4. **Set up webhook**:
   - Copy webhook URL from "Web Chat Webhook" node
   - Point your frontend to this URL

## 📁 Project Structure

```
chatbot-n8n/
├── chatbot-workflow.json    # Main n8n workflow
├── setup-guide.pdf          # Complete setup instructions
├── frontend-example/        # Sample web chat interface
│   ├── index.html
│   └── chatbot.js
├── screenshots/             # Workflow screenshots
└── README.md
```

## ⚙️ Configuration

### Intent Detection
Edit the "Detect Intent & Priority" node to customize keywords:

```javascript
// Example customization
if (message.includes('refund') || message.includes('return')) {
  intent = 'refund';
  priority = 'Medium';
}
```

### AI Response Settings
- **Temperature**: 0.7 (adjust for creativity vs consistency)
- **Max Tokens**: 500 (response length)
- **System Prompt**: Customize in OpenAI node

## 🌐 API Endpoints

- **Web Chat**: `POST /webhook/chat-webhook-id`
- **Test Endpoint**: `GET /healthz`
- **Webhook Payload**:
  ```json
  {
    "message": "Customer inquiry",
    "customerId": "123",
    "channel": "web",
    "email": "customer@example.com"
  }
  ```

## 📊 Monitoring

1. **n8n Executions**: Check success/failure rates
2. **Google Sheets**: Real-time conversation logs
3. **Airtable**: Ticket tracking and management
4. **Key Metrics**:
   - Response time (< 2s target)
   - AI accuracy (> 85% target)
   - Escalation rate (< 15% target)

## 🔧 Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| OpenAI timeout | Increase timeout to 30s |
| Airtable 404 | Verify Base ID and table name |
| Email not sending | Check SMTP credentials |
| Webhook not working | Verify CORS and firewall settings |

### Debug Mode
```bash
# Enable debug logging
export N8N_LOG_LEVEL=debug
n8n start
```

## 🛡️ Security Notes

- **Never commit API keys** to version control
- Use n8n credentials manager or environment variables
- Enable HTTPS for production
- Regularly rotate API keys
- Anonymize PII in logs

## 📈 Performance Tips

1. **Cache frequent responses** to reduce OpenAI calls
2. **Queue high-volume channels** to prevent rate limiting
3. **Monitor API usage** to control costs
4. **Regularly review** and update intent detection keywords

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Test changes thoroughly
4. Submit a pull request

## 📄 License

MIT License - see LICENSE file for details

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/chatbot-n8n/issues)
- **Documentation**: [Complete Setup Guide](setup-guide.pdf)
- **n8n Community**: [forum.n8n.io](https://forum.n8n.io)

## 🎯 Impact

This project demonstrates:
- ✅ End-to-end automation system design
- ✅ AI integration and prompt engineering
- ✅ Multi-API orchestration
- ✅ Real-world business problem solving
- ✅ Scalable architecture patterns

---

**Ready to deploy?** Follow the [complete setup guide](setup-guide.pdf) for detailed instructions!

*Built with ❤️ using n8n, OpenAI, and other awesome tools*
