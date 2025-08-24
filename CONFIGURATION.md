# 🔧 Configuration Guide

This guide explains how to configure the LangChain AI Research Agent with FastAPI deployment.

## 📋 Environment Variables

The application uses environment variables for secure configuration management.

### 🔑 Required API Keys

#### **Gemini API Key** (Required)
```bash
GEMINI_API_KEY=your-gemini-api-key-here
```

**How to get:**
1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy the generated key

#### **Tavily API Key** (Optional)
```bash
TAVILY_API_KEY=your-tavily-api-key-here
```

**How to get:**
1. Visit [Tavily API](https://tavily.com/)
2. Sign up for an account
3. Get your API key from the dashboard

### 📁 Configuration Files

#### **.env File** (Recommended)
Create a `.env` file in the project root:

```bash
# Environment Variables for LangChain AI Research Agent

# Gemini API Configuration
GEMINI_API_KEY=AIzaSyCeQeHPZYUl2iZVMfNCs1hC3FeO23pkRag

# Tavily API Configuration (optional)
TAVILY_API_KEY=your-tavily-key-here

# Additional Configuration (if needed)
# OPENAI_API_KEY=your-openai-key-here
# ANTHROPIC_API_KEY=your-anthropic-key-here
```

#### **config.py** (Automatic Loading)
The configuration is automatically loaded:

```python
import os
from dotenv import load_dotenv

# Load environment variables from .env file
load_dotenv()

# Gemini API Configuration
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY", "")
GEMINI_MODEL = "gemini-2.5-flash"

# Tavily API Configuration
TAVILY_API_KEY = os.getenv("TAVILY_API_KEY", "")
```

## 🚀 Deployment Configurations

### 🖥️ **Development Setup**

1. **Create .env file**:
```bash
cp .env.example .env
# Edit .env with your API keys
```

2. **Install dependencies**:
```bash
pip install -r requirements.txt
```

3. **Test configuration**:
```bash
python -c "from config import GEMINI_API_KEY; print('✅ API Key loaded' if GEMINI_API_KEY else '❌ API Key missing')"
```

### 🌐 **FastAPI Production Setup**

#### **Environment Variables**
```bash
# Production environment variables
GEMINI_API_KEY=your-production-gemini-key
TAVILY_API_KEY=your-production-tavily-key

# FastAPI Configuration
FASTAPI_HOST=0.0.0.0
FASTAPI_PORT=8000
FASTAPI_WORKERS=4

# Security
API_SECRET_KEY=your-secret-key-here
ALLOWED_ORIGINS=https://yourdomain.com,https://api.yourdomain.com
```

#### **Docker Configuration**
```dockerfile
# Dockerfile example
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

# Environment variables can be set here or via docker-compose
ENV GEMINI_API_KEY=""
ENV TAVILY_API_KEY=""

EXPOSE 8000
CMD ["python", "fastapi_app.py"]
```

#### **Docker Compose**
```yaml
# docker-compose.yml
version: '3.8'
services:
  research-agent:
    build: .
    ports:
      - "8000:8000"
    environment:
      - GEMINI_API_KEY=${GEMINI_API_KEY}
      - TAVILY_API_KEY=${TAVILY_API_KEY}
    env_file:
      - .env
```

## 🔒 Security Best Practices

### ✅ **Do's**
- ✅ Use `.env` files for local development
- ✅ Use environment variables in production
- ✅ Add `.env` to `.gitignore`
- ✅ Use different API keys for dev/staging/prod
- ✅ Rotate API keys regularly
- ✅ Monitor API usage and quotas

### ❌ **Don'ts**
- ❌ Commit API keys to version control
- ❌ Share API keys in chat/email
- ❌ Use production keys in development
- ❌ Hardcode API keys in source code
- ❌ Use weak or default secret keys

## 🧪 Configuration Testing

### **Test API Key Loading**
```python
# test_config.py
from config import GEMINI_API_KEY, TAVILY_API_KEY

def test_api_keys():
    assert GEMINI_API_KEY, "Gemini API key not loaded"
    assert len(GEMINI_API_KEY) > 20, "Gemini API key seems invalid"
    print("✅ Configuration test passed")

if __name__ == "__main__":
    test_api_keys()
```

### **Test FastAPI Configuration**
```bash
# Test health endpoint
curl http://localhost:8000/health

# Test API info
curl http://localhost:8000/

# Expected response should show API is configured
```

## 🚨 Troubleshooting

### **Common Issues**

#### **API Key Not Loading**
```bash
# Check if .env file exists
ls -la .env

# Check file contents (be careful not to expose keys)
head -n 1 .env

# Test Python loading
python -c "from dotenv import load_dotenv; load_dotenv(); import os; print(bool(os.getenv('GEMINI_API_KEY')))"
```

#### **Import Errors**
```bash
# Install missing dependency
pip install python-dotenv

# Verify installation
python -c "import dotenv; print('✅ python-dotenv installed')"
```

#### **API Key Invalid**
```bash
# Test API key format (Gemini keys start with 'AIza')
python -c "from config import GEMINI_API_KEY; print('✅ Valid format' if GEMINI_API_KEY.startswith('AIza') else '❌ Invalid format')"
```

#### **Permission Errors**
```bash
# Check file permissions
ls -la .env

# Fix permissions if needed
chmod 600 .env
```

## 📊 Configuration Validation

### **Startup Validation**
The application validates configuration on startup:

```python
# In fastapi_app.py startup event
@app.on_event("startup")
async def validate_configuration():
    from config import GEMINI_API_KEY
    
    if not GEMINI_API_KEY:
        raise ValueError("GEMINI_API_KEY not configured")
    
    if not GEMINI_API_KEY.startswith('AIza'):
        raise ValueError("Invalid Gemini API key format")
    
    print("✅ Configuration validated successfully")
```

### **Runtime Health Checks**
```python
# Health check includes configuration status
@app.get("/health")
async def health_check():
    return {
        "status": "healthy",
        "configuration": {
            "gemini_api_configured": bool(GEMINI_API_KEY),
            "tavily_api_configured": bool(TAVILY_API_KEY)
        }
    }
```

## 🔄 Configuration Updates

### **Updating API Keys**
1. **Development**: Update `.env` file and restart application
2. **Production**: Update environment variables and restart service
3. **Docker**: Rebuild container or update environment variables

### **Adding New Configuration**
1. Add to `.env` file
2. Update `config.py` to load the variable
3. Update documentation
4. Add validation if needed

---

**Secure configuration is essential for production deployments!** 🔒

Always follow security best practices when handling API keys and sensitive configuration data.