# LangGraph AI Booking Agent

An intelligent, autonomous booking assistant that intelligently parses natural language requests, prevents scheduling conflicts, and manages the complete booking lifecycle—all with human-in-the-loop approval for safety.

## ✨ Key Features

- **Natural Language Processing** – Convert informal user messages into structured booking data using Gemini 2.5-flash
- **Smart Conflict Detection** – Real-time Google Calendar integration prevents double-booking and overlaps
- **Human-in-the-Loop Workflow** – Requires user approval before finalizing any calendar events
- **Automated Communications** – Generates Google Meet links and sends professional email confirmations via Gmail API
- **Autonomous Decision Making** – LangGraph state machines handle complex multi-step booking workflows
- **Production-Ready** – Built with enterprise-grade APIs and error handling

## 🏗️ Architecture

```
User Request
    ↓
[LangGraph Agent] → Parse Intent (Gemini)
    ↓
[Calendar Service] → Check Conflicts
    ↓
[Human Approval] → Confirm Booking
    ↓
[Create Event] → Generate Meet Link
    ↓
[Gmail Service] → Send Confirmation
```

## 📋 Prerequisites

- **Python** 3.12 or higher
- **Google Cloud Account** with enabled APIs:
  - Google Calendar API v3
  - Gmail API v1
  - Google Meet (automatic)
- **Google Gemini API Key** (via Google AI Studio)

## 🚀 Quick Start

### 1. Clone & Setup

```bash
git clone <repository-url>
cd LangGraph-Booking-Agent
python -m venv .venv

# On Windows
.venv\Scripts\activate

# On macOS/Linux
source .venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Google APIs

**Using OAuth 2.0 (Recommended):**
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable these APIs:
   - Google Calendar API
   - Gmail API
4. Create an OAuth 2.0 Desktop Client
5. Download credentials as `credentials.json` and place in project root

**Running Authentication:**
```bash
python auth_setup.py
```
This generates `token.json` for future requests.

### 4. Set Gemini API Key

```bash
# Windows
$env:GOOGLE_API_KEY="your-gemini-api-key"

# macOS/Linux
export GOOGLE_API_KEY="your-gemini-api-key"
```

Get your API key from [Google AI Studio](https://aistudio.google.com/)

### 5. Run the Agent

```bash
# Jupyter Notebook (Interactive Development)
jupyter notebook LangGraph-Booking-Agent.ipynb

# Or use Python directly
python main.py
```

## 📁 Project Structure

```
.
├── main.py                           # Entry point
├── real_time_agent.py               # LangGraph agent implementation
├── auth_setup.py                    # Google OAuth setup
├── LangGraph-Booking-Agent.ipynb    # Interactive notebook
├── credentials.json                 # Google API credentials (auto-generated)
├── token.json                       # OAuth token (auto-generated)
├── requirements.txt                 # Python dependencies
├── pyproject.toml                   # Project metadata
└── README.md                        # This file
```

## 🔧 Configuration

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GOOGLE_API_KEY` | Gemini API key from Google AI Studio | ✅ Yes |
| `CALENDAR_ID` | Target Google Calendar ID (default: primary) | ❌ No |
| `GMAIL_SENDER` | Email to send confirmations from | ❌ No |

### Customization

Edit `real_time_agent.py` to customize:
- Booking duration defaults
- Meet link generation settings
- Email template for confirmations
- Conflict buffer time
- Agent behavior & state transitions

## 💻 Usage Example

```python
from real_time_agent import BookingAgent

agent = BookingAgent()

# User request (natural language)
request = "Can you book a 1-hour meeting with John for tomorrow at 2 PM?"

# Process booking
result = agent.process_booking(request)

# Result includes:
# - Parsed meeting details
# - Conflict check results
# - Approval status
# - Google Meet link
# - Confirmation email sent
```

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| `credentials.json not found` | Run `python auth_setup.py` to generate authentication files |
| `API quotas exceeded` | Check your Google Cloud Console usage limits |
| `Meeting conflicts detected` | Agent will suggest alternative times automatically |
| `Gmail not sending emails` | Ensure "Less secure app access" is enabled (or use app-specific passwords) |
| `Token expired` | Delete `token.json` and run `python auth_setup.py` again |

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `langgraph` | ≥1.1.6 | Agent orchestration framework |
| `langchain` | ≥1.2.15 | LLM integration & utilities |
| `langchain-google-genai` | ≥4.2.1 | Gemini model integration |
| `google-api-python-client` | Latest | Google Calendar & Gmail APIs |
| `google-auth-oauthlib` | Latest | OAuth 2.0 authentication |
| `pandas` | Latest | Data processing |

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## ⚠️ Important Notes

- **Security:** Never commit `credentials.json` or `token.json` to version control. Add to `.gitignore`
- **Rate Limiting:** Respect Google API quotas to avoid unexpected billing
- **Testing:** Test thoroughly with a non-production calendar before using with real events
- **Human Approval:** Always requires explicit user confirmation before making calendar changes

## 📝 License

This project is licensed under the MIT License. See LICENSE file for details.

## 🆘 Support

For issues or questions:
- Check the troubleshooting section above
- Review [LangGraph documentation](https://langchain-ai.github.io/langgraph/)
- Check [Google Calendar API docs](https://developers.google.com/calendar)
- Open an issue on GitHub

---

**Built with ❤️ using LangGraph, LangChain, and Google Gemini**
