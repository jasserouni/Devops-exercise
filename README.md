# DevOps Exercise — CI/CD Pipeline & Deployment

## Overview

You are given a working **Flask web application** and a **Dockerfile**.
Your task is to **create a GitHub Actions CI/CD pipeline** that builds the Docker image and deploys it to a running EC2 instance.

**Time limit: 45 minutes**

---

## What's Already Done ✅

- Flask web app (`app/app.py`) — do not modify
- Dockerfile — do not modify
- EC2 instance — already running with Docker installed

---

## What You Need to Do 🔧

**Step 1 — Push to GitHub**

Create a new repository on your own GitHub account and push this project to it.

**Step 2 — Add GitHub Secrets**

Go to your repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

Add these 3 secrets:

| Secret Name | Value |
|-------------|-------|
| `EC2_HOST` | `3.79.9.72` |
| `EC2_USER` | `ec2-user` |
| `EC2_SSH_KEY` | *(ask the interviewer — paste the full key including `-----BEGIN` and `-----END` lines)* |

**Step 3 — Create the pipeline**

Create the file `.github/workflows/deploy.yml` that:
- Triggers on every push to `main`
- Builds the Docker image
- SSHs into the EC2 instance
- Stops any existing container and starts the new one on port `5000`

**Step 4 — Verify**

Once the pipeline runs successfully, open in your browser:

```
http://3.79.9.72:5000
```

You should see the **BeroeXnNnamu** page. Show this to the interviewer.

---

## How the SSH Access Works

You do **not** need AWS credentials. The pipeline connects to EC2 using an **SSH private key**.

```
GitHub Actions runner
       │
       │  SSH (using EC2_SSH_KEY secret)
       ▼
  EC2 instance (3.79.9.72)
       │
       │  docker build + docker run
       ▼
  App running on port 5000
```

The interviewer will give you the private key. You store it as the `EC2_SSH_KEY` GitHub Secret — your pipeline reads it from there to authenticate.

---

## Project Structure

```
.
├── app/
│   ├── app.py                 # Flask app — do not modify
│   ├── requirements.txt       # do not modify
│   └── templates/
│       └── index.html         # do not modify
├── Dockerfile                 # do not modify
├── .github/
│   └── workflows/
│       └── deploy.yml         # ← create this
├── .gitignore
└── README.md
```

---

## Rules

- ✅ Internet allowed (Google, Stack Overflow, GitHub docs, GitHub Actions marketplace)
- ❌ No AI tools (ChatGPT, Copilot, etc.)
- ❌ Do not modify the app code or Dockerfile
- ❌ Do not manually install anything on EC2 — everything must go through the pipeline

---

Good luck! 🚀
