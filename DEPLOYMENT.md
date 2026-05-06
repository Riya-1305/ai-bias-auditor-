# Deployment Guide for AI Bias Auditor

This guide covers different ways to deploy the AI Bias Auditor Streamlit application, including the recommended approach.

## Prerequisites

- Python 3.8+
- Git
- Access to a deployment platform

## Different Deployment Methods

### 1. Streamlit Cloud (Recommended)

**Description:** Official platform for Streamlit apps, free for public repositories.

**Steps:**
1. Push code to a public GitHub repo
2. Go to [share.streamlit.io](https://share.streamlit.io)
3. Connect GitHub, select repo/branch
4. Set main file to `app.py`
5. Deploy

**Pros:** Free, automatic updates, no server management, built-in sharing
**Cons:** Requires public repo, limited customization

### 2. Heroku

**Description:** Cloud platform supporting various languages.

**Steps:**
1. Create `Procfile`: `web: streamlit run app.py --server.port $PORT --server.headless true`
2. Create `runtime.txt`: `python-3.9.7`
3. Install Heroku CLI: `heroku create app-name`
4. Deploy: `git push heroku main`

**Pros:** Supports private apps, free tier available
**Cons:** May sleep after inactivity, requires CLI

### 3. Docker + Cloud Platform

**Description:** Containerize the app and deploy to AWS/GCP/Azure.

**Steps:**
1. Create `Dockerfile`:
   ```
   FROM python:3.9-slim
   WORKDIR /app
   COPY requirements.txt .
   RUN pip install -r requirements.txt
   COPY . .
   CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
   ```
2. Build: `docker build -t ai-bias-auditor .`
3. Push to registry, deploy to cloud service

**Pros:** Scalable, portable
**Cons:** More complex setup

### 4. AWS Elastic Beanstalk

**Description:** AWS service for deploying web apps.

**Steps:**
1. Use EB CLI to initialize
2. Configure environment
3. Deploy via `eb deploy`

**Pros:** Scalable, integrates with AWS ecosystem
**Cons:** AWS costs, learning curve

### 5. Local/VPS Deployment

**Description:** Run on your own server.

**Steps:**
1. Install dependencies
2. Run `streamlit run app.py --server.port=8501 --server.address=0.0.0.0`
3. Use nginx/reverse proxy for production

**Pros:** Full control
**Cons:** No auto-scaling, manual maintenance

## Best Approach: Streamlit Cloud

**Why it's the best for this project:**
- **Ease of Use:** Simplest deployment process - just push to GitHub and click deploy
- **Cost:** Completely free for public repos, no hidden fees
- **Maintenance:** Automatic updates on code changes, no server management
- **Performance:** Optimized for Streamlit, handles scaling automatically
- **Sharing:** Built-in app sharing and embedding features
- **Suitability:** This is a demo/educational tool, so public deployment fits perfectly

For production enterprise use, Docker + cloud platform would be better for customization and security.

## Testing Deployment

Always test locally first:
```bash
pip install -r requirements.txt
streamlit run app.py
```