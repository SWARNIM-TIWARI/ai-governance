AI Safety & Governance Stack

A production-ready system for safe, responsible AI deployment. Four interconnected systems evaluate every aspect of AI autonomy: decision authority, cost implications, readiness assessment, and incident prevention.

Status: ✅ Fully functional | 📊 Case studies included | 🚀 Cloud-ready

---

🎯 The Problem This Solves

Companies ship AI systems without asking critical questions:

- When should AI be allowed to act? (Authorization gap)
- How much human oversight is actually needed? (Cost/risk trade-off)
- Should this ship at all? (Readiness gap)
- What went wrong when things fail? (Learning gap)

This project builds the governance infrastructure to answer all four.

---

🏗️ Architecture

┌────────────────────────────────────────────────────────────────┐
│                     SHARED AUDIT LOG                           │
│            (Immutable decision record for all tasks)           │
└────────────────────────────────────────────────────────────────┘
                              ▲
                 ┌────────────┼────────────┐
                 │            │            │
        ┌────────▼──────┐ ┌──▼────────┐ ┌─▼──────────────┐
        │ AUTHORITY     │ │  COST     │ │  READINESS    │
        │ ENGINE        │ │OPTIMIZER  │ │  FRAMEWORK    │
        │               │ │           │ │               │
        │ Routes:       │ │ Answers:  │ │ Answers:      │
        │ • Auto-act    │ │ How much  │ │ Should we     │
        │ • Escalate    │ │ review?   │ │ deploy?       │
        │ • Refuse      │ │ At what   │ │               │
        │               │ │ cost?     │ │ Score: 0-1    │
        └────────┬──────┘ └──────────┘ └─────────┬──────┘
                 │                               │
                 └───────────────┬────────────────┘
                                 │
                        ┌────────▼──────────┐
                        │ INCIDENT          │
                        │ ANALYZER          │
                        │                   │
                        │ Answers:          │
                        │ What could go     │
                        │ wrong? Why?       │
                        │ How to prevent?   │
                        └───────────────────┘

Key Design:

- All subsystems feed from one immutable audit log
- Each system can operate independently
- Designed for real deployment, not just education

---

🚀 Quick Start (5 minutes)

Prerequisites

- Python 3.9+
- pip
- Docker (optional, for cloud)
- Git

Local Setup

# 1. Clone and enter directory
git clone <your-repo-url>
cd ai-safety-portfolio

# 2. Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run tests to verify installation
python -m pytest tests/ -v

# 5. Start the server
python main_app.py

Server runs on "http://localhost:5000" ✅

---

📖 System Overview

System 1: Authority Decision Engine

«"When should AI be allowed to act?"»

curl -X POST http://localhost:5000/api/v1/decide \
  -H "Content-Type: application/json" \
  -d '{
    "task_id": "mod_12345",
    "domain": "moderation",
    "model_confidence": 0.92,
    "risk_level": 0.15,
    "reversibility": 0.8
  }'

Response:

{
  "decision": "auto_act",
  "logic": "High confidence (0.92) + low risk (0.15)",
  "risk_flags": []
}

---

System 2: Cost Optimizer

«"How much human oversight do we need?"»

curl -X POST http://localhost:5000/api/v1/cost/optimize \
  -H "Content-Type: application/json" \
  -d '{
    "error_rate": 0.05,
    "error_cost": 1000,
    "human_review_cost": 5,
    "scale": 1000
  }'

Response:

{
  "optimal_review_rate": 0.25,
  "total_monthly_cost": 12500,
  "human_reviews_per_day": 50,
  "recommendation": "Review 25% of decisions"
}

---

System 3: Readiness Framework

«"Should we ship this AI product?"»

curl -X POST http://localhost:5000/api/v1/readiness/evaluate \
  -H "Content-Type: application/json" \
  -d '{
    "system_name": "content_moderation_v2",
    "reliability_score": 0.82,
    "misuse_risk_score": 0.45,
    "harm_potential_score": 0.35,
    "explainability_score": 0.70,
    "governance_score": 0.80
  }'

Response:

{
  "decision": "SHIP",
  "overall_score": 0.702,
  "recommendation": "Meets readiness criteria. Safe to deploy."
}

---

System 4: Incident Analyzer

«"What went wrong and how do we prevent it?"»

curl -X POST http://localhost:5000/api/v1/incidents/analyze \
  -H "Content-Type: application/json" \
  -d '{
    "task_id": "mod_12345",
    "actual_outcome": "false_positive"
  }'

Response:

{
  "root_cause": "model_uncertainty",
  "preventability_score": 0.75,
  "recommendations": [
    "Increase confidence threshold for borderline cases",
    "Add ensemble voting for moderation decisions"
  ]
}

---

📁 Project Structure

ai-safety-portfolio/
│
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── docker-compose.yml                 # Local Docker setup
├── Dockerfile                         # Production container
├── .env.example                       # Environment variables
├── .gitignore                         # Git ignore rules
│
├── core/                              # Shared infrastructure
│   ├── __init__.py
│   ├── models.py                      # AITask, DecisionRecord, etc.
│   ├── storage.py                     # AuditLog, persistence
│   ├── enums.py                       # Decision, FailureType enums
│   └── config.py                      # Configuration management
│
├── authority/                         # System 1: Decision Authority
│   ├── __init__.py
│   ├── engine.py                      # AuthorityDecider logic
│   ├── routes.py                      # Flask endpoints
│   └── validators.py                  # Input validation
│
├── cost_optimizer/                    # System 2: Cost Analysis
│   ├── __init__.py
│   ├── optimizer.py                   # HumanInTheLoopOptimizer
│   ├── routes.py                      # Flask endpoints
│   └── models.py                      # CostModel dataclasses
│
├── readiness/                         # System 3: Readiness Framework
│   ├── __init__.py
│   ├── framework.py                   # ReadinessScorer logic
│   ├── routes.py                      # Flask endpoints
│   ├── dimensions.py                  # Scoring dimensions
│   └── case_studies.py                # Built-in case studies
│
├── incidents/                         # System 4: Incident Analysis
│   ├── __init__.py
│   ├── analyzer.py                    # IncidentAnalyzer logic
│   ├── routes.py                      # Flask endpoints
│   ├── taxonomy.py                    # Failure taxonomy
│   └── postmortem.py                  # Postmortem generation
│
├── api/                               # Unified API layer
│   ├── __init__.py
│   ├── v1.py                          # API v1 routes
│   ├── middleware.py                  # Logging, error handling
│   └── schemas.py                     # Request/response validation
│
├── case_studies/                      # Real-world data sets
│   ├── moderation_demo.json           # Content moderation scenarios
│   ├── lending_demo.json              # Credit decision scenarios
│   ├── hiring_demo.json               # Recruitment AI scenarios
│   ├── healthcare_demo.json           # Healthcare triage scenarios
│   └── README.md                      # Case study documentation
│
├── tests/                             # Comprehensive test suite
│   ├── __init__.py
│   ├── conftest.py                    # Pytest fixtures
│   ├── test_authority.py              # Authority engine tests
│   ├── test_cost_optimizer.py         # Cost optimizer tests
│   ├── test_readiness.py              # Readiness framework tests
│   ├── test_incidents.py              # Incident analyzer tests
│   ├── test_integration.py            # End-to-end tests
│   └── test_api.py                    # API endpoint tests
│
├── main_app.py                        # Flask application entry point
├── wsgi.py                            # WSGI entry for production
└── scripts/                           # Deployment & utility scripts
    ├── run_local.sh                   # Local development runner
    ├── run_docker.sh                  # Docker runner
    ├── load_case_studies.py           # Load demo data
    └── generate_report.py             # Generate analysis reports

---

🛠️ Setup & Installation

Option 1: Local Development (Recommended for learning)

# 1. Clone repository
git clone <your-repo>
cd ai-safety-portfolio

# 2. Create & activate virtual environment
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Verify installation (run tests)
python -m pytest tests/ -v --tb=short

# 5. Start development server
python main_app.py

# 6. Open browser to http://localhost:5000

Expected output:

 * Running on http://127.0.0.1:5000
 * Debug mode: on
Press CTRL+C to quit

---

Option 2: Docker (Local)

# 1. Build image
docker build -t ai-safety:latest .

# 2. Run container
docker run -p 5000:5000 -e FLASK_ENV=development ai-safety:latest

# 3. Access at http://localhost:5000

---

Option 3: Docker Compose (Full stack)

# 1. Start services
docker-compose up -d

# 2. View logs
docker-compose logs -f

# 3. Stop services
docker-compose down

---

📊 Testing the System

Run All Tests

python -m pytest tests/ -v

Run Specific Test Suite

# Authority engine tests only
python -m pytest tests/test_authority.py -v

# Integration tests only
python -m pytest tests/test_integration.py -v

# With coverage report
python -m pytest tests/ --cov=core --cov=authority --cov-report=html

Manual Testing with cURL

# Test 1: Authority decision
curl -X POST http://localhost:5000/api/v1/decide \
  -H "Content-Type: application/json" \
  -d @case_studies/moderation_demo.json

# Test 2: Cost analysis
curl http://localhost:5000/api/v1/cost/case-study/moderation

# Test 3: Readiness evaluation
curl http://localhost:5000/api/v1/readiness/case-study/chatgpt-gpt4

# Test 4: Incident analysis
curl -X POST http://localhost:5000/api/v1/incidents/analyze \
  -H "Content-Type: application/json" \
  -d '{"task_id": "mod_001", "outcome": "false_positive"}'

---

🌩️ Cloud Deployment

Deploy to Heroku (Free tier available)

# 1. Install Heroku CLI
# See: https://devcenter.heroku.com/articles/heroku-cli

# 2. Login
heroku login

# 3. Create app
heroku create your-app-name

# 4. Deploy
git push heroku main

# 5. View logs
heroku logs --tail

# 6. Open in browser
heroku open

Environment variables:

heroku config:set FLASK_ENV=production
heroku config:set SECRET_KEY=your-secret-key

---

Deploy to Google Cloud Run (Serverless)

# 1. Install gcloud CLI
# See: https://cloud.google.com/sdk/docs/install

# 2. Login and set project
gcloud auth login
gcloud config set project YOUR_PROJECT_ID

# 3. Build and deploy
gcloud run deploy ai-safety-portfolio \
  --source . \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated

# 4. View service
gcloud run services describe ai-safety-portfolio

---

Deploy to AWS ECS

# 1. Create ECR repository
aws ecr create-repository --repository-name ai-safety

# 2. Push Docker image
docker build -t ai-safety:latest .
docker tag ai-safety:latest <AWS_ACCOUNT>.dkr.ecr.<REGION>.amazonaws.com/ai-safety:latest
docker push <AWS_ACCOUNT>.dkr.ecr.<REGION>.amazonaws.com/ai-safety:latest

# 3. Create ECS task definition (see ecs-task-definition.json)
aws ecs register-task-definition --cli-input-json file://ecs-task-definition.json

# 4. Create and run ECS service
aws ecs create-service --cluster my-cluster --service-name ai-safety \
  --task-definition ai-safety --desired-count 1 --launch-type FARGATE

---

🔧 Configuration

Environment Variables

Create a ".env" file (copy from ".env.example"):

# Flask
FLASK_ENV=development              # development or production
FLASK_DEBUG=True                   # Auto-reload on changes
SECRET_KEY=your-secret-key-here    # For session security

# Database
DATABASE_URL=sqlite:///audit_log.db # SQLite (local) or PostgreSQL
DATABASE_TYPE=sqlite                # sqlite or postgres

# Logging
LOG_LEVEL=INFO                     # DEBUG, INFO, WARNING, ERROR
LOG_FILE=logs/app.log              # Log file path

# API
API_RATE_LIMIT=1000                # Requests per hour
API_TIMEOUT=30                     # Seconds

# Features
ENABLE_CASE_STUDIES=True
ENABLE_MOCK_AI_MODELS=True

Local Configuration File ("config.py")

import os
from pathlib import Path

class Config:
    BASE_DIR = Path(__file__).parent
    SECRET_KEY = os.getenv('SECRET_KEY', 'dev-key-change-in-production')
    FLASK_ENV = os.getenv('FLASK_ENV', 'development')
    
    # Database
    DATABASE_URL = os.getenv('DATABASE_URL', 'sqlite:///audit_log.db')
    
    # Logging
    LOG_LEVEL = os.getenv('LOG_LEVEL', 'INFO')
    LOG_FILE = os.getenv('LOG_FILE', 'logs/app.log')

class DevelopmentConfig(Config):
    DEBUG = True
    TESTING = False

class TestingConfig(Config):
    TESTING = True
    DATABASE_URL = 'sqlite:///:memory:'

class ProductionConfig(Config):
    DEBUG = False
    TESTING = False

---

📚 API Documentation

Full API Reference

1. Authority Decision

POST /api/v1/decide
Content-Type: application/json

{
  "task_id": "unique_id",
  "domain": "moderation|lending|hiring|healthcare",
  "model_confidence": 0.0-1.0,
  "risk_level": 0.0-1.0,
  "reversibility": 0.0-1.0
}

Response (200):
{
  "decision": "auto_act|escalate|refuse",
  "logic": "explanation",
  "risk_flags": ["flag1", "flag2"]
}

---

2. Cost Optimizer

POST /api/v1/cost/optimize
Content-Type: application/json

{
  "error_rate": 0.0-1.0,
  "error_cost": 1000,
  "human_review_cost": 5,
  "scale": 1000
}

GET /api/v1/cost/case-study/{domain}
# Returns: optimal review rate, costs, recommendations

---

3. Readiness Framework

POST /api/v1/readiness/evaluate
Content-Type: application/json

{
  "system_name": "string",
  "reliability_score": 0.0-1.0,
  "misuse_risk_score": 0.0-1.0,
  "harm_potential_score": 0.0-1.0,
  "explainability_score": 0.0-1.0,
  "governance_score": 0.0-1.0
}

GET /api/v1/readiness/case-study/{case_name}
# Returns: ship/no-ship decision, score breakdown

---

4. Incident Analyzer

POST /api/v1/incidents/analyze
Content-Type: application/json

{
  "task_id": "string",
  "actual_outcome": "false_positive|false_negative|true_positive|true_negative"
}

GET /api/v1/incidents/summary/{domain}
# Returns: incident statistics, prevention rate

---

5. Dashboard

GET /api/v1/dashboard

Response:
{
  "total_decisions": 1000,
  "decisions_by_type": {...},
  "avg_confidence": 0.82,
  "incidents_prevented": 150
}

---

🧪 Testing Guide

Unit Tests

# Test individual components
python -m pytest tests/test_authority.py::test_high_confidence_low_risk -v

Integration Tests

# Test full pipeline
python -m pytest tests/test_integration.py -v

Load Testing (Optional)

pip install locust

locust -f tests/load_test.py --host=http://localhost:5000

---

📈 Monitoring & Observability

View Audit Log

sqlite3 audit_log.db "SELECT * FROM decisions LIMIT 10;"

Generate Report

python scripts/generate_report.py --domain moderation --output report.html

Check Health

curl http://localhost:5000/health

---

🚀 Production Checklist

- [ ] Set "FLASK_ENV=production"
- [ ] Use strong "SECRET_KEY"
- [ ] Switch to PostgreSQL database
- [ ] Enable HTTPS/SSL
- [ ] Configure logging to file/cloud
- [ ] Set up monitoring (New Relic, DataDog, etc.)
- [ ] Configure backup strategy
- [ ] Test disaster recovery
- [ ] Set up CI/CD pipeline
- [ ] Document runbooks for on-call

---

📞 Troubleshooting

Port 5000 Already in Use

# Find what's using port 5000
lsof -i :5000

# Kill the process
kill -9 <PID>

Virtual Environment Issues

# Deactivate and recreate
deactivate
rm -rf venv
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

Tests Failing

# Check test dependencies
pip install -r requirements-test.txt

# Run with verbose output
python -m pytest tests/ -vv --tb=long

Docker Issues

# Rebuild from scratch
docker system prune -a
docker build --no-cache -t ai-safety:latest .

---

📖 Additional Resources

- Architecture Documentation: See "docs/architecture.md"
- Case Studies: See "case_studies/README.md"
- API Examples: See "docs/api_examples.md"
- Deployment Guide: See "docs/deployment.md"
- Contributing: See "CONTRIBUTING.md"

---

📝 License

MIT License - See LICENSE file for details

---

🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch
3. Add tests for new functionality
4. Submit a pull request

See "CONTRIBUTING.md" for details.

---

📧 Questions?

Open an issue on GitHub or contact the maintainers.
