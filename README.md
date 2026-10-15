# HeartShield - Heart Disease Prediction System

A full-stack web application for heart disease risk assessment and management.

## Quick Start (Plug & Play)

### Prerequisites
- **Python 3.8+** (Backend)
- **Node.js 16+** (Frontend)
- **MySQL** database (or use the provided cloud DB)

### Backend Setup

1. **Navigate to backend directory:**
```bash
cd Back-end
```

2. **Create virtual environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables:**
```bash
# Copy the example env file
cp .env.example .env

# Edit .env with your actual values
# - DATABASE_URL: Your MySQL database connection
# - JWT_SECRET_KEY: Generate a random secret key
# - GEMINI_API_KEY: Get from Google AI Studio
# - SMTP credentials: For email notifications
```

5. **Start the backend server:**
```bash
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Backend will run on: **http://localhost:8000**

### Frontend Setup

1. **Navigate to frontend directory (in a new terminal):**
```bash
cd Front-end
```

2. **Install dependencies:**
```bash
npm install
```

3. **Set up environment variables:**
```bash
# Copy the example env file
cp .env.local.example .env.local

# Keep the default API URL unless you're deploying
```

4. **Start the frontend server:**
```bash
npm run dev
```

Frontend will run on: **http://localhost:3000**

---

## Architecture

### Frontend (Next.js)
- **Port:** 3000
- **Tech:** React 19, Next.js 15, TailwindCSS
- **API Client:** Built-in HTTP client with token management
- **Authentication:** JWT-based with localStorage

### Backend (FastAPI)
- **Port:** 8000
- **Tech:** FastAPI, SQLAlchemy, Pydantic
- **Database:** MySQL (TiDB Cloud)
- **Authentication:** JWT tokens
- **CORS:** Configured for localhost:3000

### Database
- **Type:** MySQL
- **Service:** TiDB Cloud (cloud-hosted)
- **Connection:** Configured in `.env`

---

## Testing Communication

### Verify Backend is Running
```bash
curl http://localhost:8000/health
```

Expected response:
```json
{"status": "healthy"}
```

### Verify Frontend to Backend Communication
1. Open http://localhost:3000
2. Open browser DevTools (F12)
3. Go to **Network** tab
4. Try logging in with test credentials
5. Look for `POST /api/v1/auth/login` request
6. Check the response from backend

---

## Key Endpoints

### Authentication
- `POST /api/v1/auth/login` - User login
- `POST /api/v1/auth/register/patient` - Patient registration
- `POST /api/v1/auth/register/doctor` - Doctor registration
- `GET /api/v1/auth/me` - Get current user

### Patients
- `GET /api/v1/patients` - List patients
- `POST /api/v1/patients` - Create patient
- `GET /api/v1/patients/{id}` - Get patient details

### Health Predictions
- `POST /api/v1/predictions/assess` - Assess heart disease risk
- `GET /api/v1/predictions/{id}` - Get prediction history

### Reports
- `POST /api/v1/reports` - Generate health report
- `GET /api/v1/reports/{id}` - Download report

---

## Troubleshooting

### Backend won't start
```bash
# Check if port 8000 is in use
lsof -i :8000  # On Mac/Linux
netstat -ano | findstr :8000  # On Windows
```

### Frontend can't connect to backend
- Verify backend is running on http://localhost:8000
- Check that CORS is enabled (should be by default)
- Open browser DevTools → Network tab → look for CORS errors
- Ensure `.env.local` has correct API URL

### Database connection error
- Verify DATABASE_URL in `.env` is correct
- Check internet connection (if using cloud database)
- Verify database credentials and host

### Dependencies installation issues
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install

# For Python
pip install --upgrade pip
pip install -r requirements.txt --force-reinstall
```

---

## Project Structure

```
HeartShield/
├── Front-end/              # Next.js frontend
│   ├── src/
│   │   ├── app/           # Pages and routes
│   │   ├── components/    # React components
│   │   ├── context/       # Context providers
│   │   └── lib/           # API client
│   ├── package.json
│   └── .env.local
│
├── Back-end/               # FastAPI backend
│   ├── app/
│   │   ├── api/           # API routes
│   │   ├── models/        # Database models
│   │   ├── schemas/       # Request/Response schemas
│   │   ├── core/          # Security, config
│   │   └── database/      # Database connection
│   ├── requirements.txt
│   └── .env
│
└── README.md
```

---

## Environment Variables Reference

### Backend (.env)
| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | MySQL connection string | `mysql+pymysql://user:pass@host/db` |
| `JWT_SECRET_KEY` | Secret key for JWT signing | Random 32+ character string |
| `JWT_ALGORITHM` | JWT algorithm | `HS256` |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | Token expiration time | `1440` (24 hours) |
| `GEMINI_API_KEY` | Google Gemini API key | Get from Google AI Studio |
| `SMTP_HOST` | Email server | `smtp.gmail.com` |
| `SMTP_PORT` | Email server port | `587` |
| `SMTP_USERNAME` | Email address | Your email |
| `SMTP_PASSWORD` | Email app password | Generate from email provider |

### Frontend (.env.local)
| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_API_URL` | Backend API URL | `http://localhost:8000/api/v1` |

---

## Features

### Patient Portal
- User registration and authentication
- Health assessment questionnaire
- Heart disease risk prediction
- Health reports generation
- Recommendation engine

### Doctor Portal
- View patient information
- Review assessments
- Provide recommendations
- Access to analytics

### Admin Dashboard
- User management
- System monitoring
- Analytics and statistics

---

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Review the API logs (terminal output)
3. Check browser console for frontend errors (F12)
4. Verify database connection

---

## License

This project is confidential and proprietary.