# Smoke Testing & CI/CD Pipeline Demo

> Forked from [eman289/smart-login-system](https://github.com/eman289/smart-login-system) — a static web app built with HTML, CSS and JavaScript.

---

## What I Added

This fork adds two DevOps files on top of the original project:

- **`Dockerfile`** — containerizes the static site using nginx so it can be deployed anywhere
- **`.github/workflows/ci_cd.yml`** — GitHub Actions pipeline that runs on every push to main

---

## CI/CD Pipeline

The pipeline automates 3 things: smoke testing, building a Docker image, and pushing it to DockerHub.

```
Push to main
     ↓
Checkout code
     ↓
Start Python web server (serves static files on port 3000)
     ↓
Smoke Test → curl index.html → is app responding?
    YES → Build Docker image → Push to DockerHub
    NO  → Pipeline stops, nothing gets built or pushed
```

### Why Smoke Testing?
Smoke testing is a quick sanity check — it doesn't test every feature, it just checks if the app is alive and responding. If it fails, there's no point building or deploying a broken image.

---

## Dockerfile

```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
```

Copies all static files into nginx's serving directory and exposes port 80.

---

## GitHub Secrets Required

Add these in **Settings → Secrets → Actions** before running the pipeline:

| Secret | Description |
|---|---|
| `DOCKERHUB_USERNAME` | Your DockerHub username |
| `DOCKERHUB_PASSWORD` | Your DockerHub password or access token |

---

## Credits
Original project by [eman289](https://github.com/eman289/smart-login-system)
