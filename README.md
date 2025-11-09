# AI Cold Caller Backend v2

A modular FastAPI backend for the AI Cold Caller system with Gemini AI integration.

## 🚀 Features

- **Modular Architecture**: Clean separation of concerns with dedicated modules
- **Gemini AI Integration**: Advanced conversation handling with Google's Gemini API
- **RESTful API**: Complete CRUD operations for leads, calls, and conversations
- **Database Management**: SQLAlchemy ORM with SQLite/PostgreSQL support
- **Health Monitoring**: Comprehensive health checks for all services
- **CSV Import**: Bulk lead import functionality
- **Statistics & Analytics**: Detailed reporting and dashboard data
- **CORS Support**: Cross-origin resource sharing for frontend integration

## 📁 Project Structure

```
ai_caller_backend_v2/
├── app/
│   ├── api/                    # API endpoints
│   │   ├── leads.py           # Lead management endpoints
│   │   ├── ai.py              # AI conversation endpoints
│   │   ├── stats.py           # Statistics endpoints
│   │   └── health.py          # Health check endpoints
│   ├── core/                  # Core configuration
│   │   └── config.py          # Settings and environment variables
│   ├── database/              # Database management
│   │   └── database.py        # Database connection and session
│   ├── models/                # Database models
│   │   └── models.py          # SQLAlchemy models
│   ├── schemas/               # Pydantic schemas
│   │   └── schemas.py         # Request/response validation
│   ├── services/              # Business logic
│   │   ├── ai_service.py      # Gemini AI integration
│   │   └── lead_service.py    # Lead management logic
│   └── utils/                 # Utility functions
├── main.py                    # FastAPI application entry point
├── requirements.txt           # Python dependencies
├── env.example               # Environment variables template
└── README.md                 # This file
```

## 🛠️ Installation

### Prerequisites

- Python 3.8+
- pip package manager

### Setup

1. **Clone the repository**
   ```bash
   cd ai_caller_backend_v2
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment variables**
   ```bash
   cp env.example .env
   # Edit .env with your API keys and configuration
   ```

4. **Run the application**
   ```bash
   python main.py
   ```

## ⚙️ Configuration

### Environment Variables

Create a `.env` file with the following variables:

```env
# Database Configuration
DATABASE_URL=sqlite:///./ai_caller_backend.db

# Gemini AI Configuration
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL=gemini-1.5-flash

# Twilio Configuration (optional)
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_PHONE_NUMBER=your_twilio_phone_number

# Application Configuration
APP_NAME=AI Cold Caller Backend
APP_VERSION=1.0.0
DEBUG=True
HOST=0.0.0.0
PORT=8000

# CORS Configuration
ALLOWED_ORIGINS=["http://localhost:3000", "http://127.0.0.1:3000"]
```

## 📚 API Documentation

### Base URL
```
http://localhost:8000
```

### Available Endpoints

#### Health Checks
- `GET /health` - Basic health check
- `GET /api/health/` - API health status
- `GET /api/health/database` - Database connectivity check
- `GET /api/health/ai` - AI service health check
- `GET /api/health/full` - Comprehensive health check

#### Lead Management
- `GET /api/leads/` - Get all leads (with filtering)
- `POST /api/leads/` - Create new lead
- `GET /api/leads/{lead_id}` - Get specific lead
- `PUT /api/leads/{lead_id}` - Update lead
- `DELETE /api/leads/{lead_id}` - Delete lead
- `POST /api/leads/upload` - Upload leads from CSV
- `GET /api/leads/statistics` - Get lead statistics

#### AI Conversations
- `POST /api/ai/conversation` - Start/continue AI conversation
- `POST /api/ai/analyze-conversation` - Analyze conversation sentiment
- `POST /api/ai/generate-follow-up` - Generate follow-up message
- `GET /api/ai/health` - AI service health check

#### Statistics
- `GET /api/stats/dashboard` - Dashboard statistics
- `GET /api/stats/calls` - Call statistics
- `GET /api/stats/leads` - Lead statistics
- `GET /api/stats/queue` - Queue statistics

### Interactive Documentation

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

## 🤖 AI Integration

### Gemini AI Features

- **Conversation Management**: Natural language processing for cold calling
- **Lead Qualification**: Intelligent lead scoring and qualification
- **Meeting Scheduling**: Automated meeting scheduling capabilities
- **Sentiment Analysis**: Conversation sentiment and insight extraction
- **Follow-up Generation**: Automated follow-up message creation

### System Prompt

The AI is configured with a specialized system prompt for cold calling:

- Professional and conversational tone
- Lead qualification focus
- Meeting scheduling capabilities
- Feedback collection
- Domain-specific knowledge (AispireLabs)

## 🗄️ Database Models

### Lead Model
- Basic information (name, phone, email, company)
- Status tracking (pending, scheduled, calling, called, not_interested)
- Priority scoring (1-5 scale)
- Timestamps and audit trail

### Call Model
- Call tracking (SID, status, outcome, duration)
- Recording and meeting URLs
- Lead relationship
- Performance metrics

### Conversation Message Model
- AI conversation history
- Role-based messages (user/assistant)
- Timestamp tracking
- Call relationship

### System Status Model
- Scheduler status
- Active call tracking
- Queue health monitoring
- Performance metrics

## 🔧 Development

### Running in Development Mode

```bash
python main.py
```

The server will start with auto-reload enabled.

### Database Migrations

The application automatically creates tables on startup. For production, consider using Alembic for migrations.

### Logging

Logs are written to both console and `app.log` file with the following levels:
- INFO: General application events
- ERROR: Error conditions
- DEBUG: Detailed debugging information

## 🚀 Production Deployment

### Using Uvicorn

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

### Using Gunicorn

```bash
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000
```

### Docker Deployment

```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## 🔒 Security Considerations

- **API Keys**: Store sensitive API keys in environment variables
- **CORS**: Configure allowed origins for production
- **Rate Limiting**: Implement rate limiting for production use
- **Authentication**: Add JWT authentication for production
- **HTTPS**: Use HTTPS in production environments

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 🆘 Support

For support and questions:
- Check the API documentation at `/docs`
- Review the health endpoints for service status
- Check the application logs for detailed error information 