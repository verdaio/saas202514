# Development Guide

**Project:** {{PROJECT_NAME}}
**Last Updated:** {{CREATION_DATE}}

---

## 🎯 Quick Start

This guide covers everything you need to develop, test, and deploy this project.

**New to the project?** Start here, then see `_START-HERE.md` for planning workflows.

---

## 📋 Tooling Requirements

### Required Software

| Tool | Minimum Version | Purpose | Installation |
|------|----------------|---------|--------------|
| **Node.js** | 18+ | Frontend/backend JavaScript runtime | [nodejs.org](https://nodejs.org) |
| **npm** | 9+ | Package manager (comes with Node.js) | Included with Node.js |
| **Docker Desktop** | Latest | Container runtime | [docker.com](https://www.docker.com/products/docker-desktop) |
| **Docker Compose** | v2+ | Multi-container orchestration | Included with Docker Desktop |
| **Azure CLI** | 2.60+ | Azure deployment (optional) | [docs.microsoft.com](https://docs.microsoft.com/cli/azure/install-azure-cli) |
| **Git** | 2.30+ | Version control | [git-scm.com](https://git-scm.com) |

### Verify Installation

```bash
# Check versions
node --version        # Should show v18.x.x or higher
npm --version         # Should show 9.x.x or higher
docker --version      # Should show 20.x.x or higher
docker compose version # Should show v2.x.x (NOT v1!)
az --version          # Should show 2.60.x or higher (if using Azure)
git --version         # Should show 2.30.x or higher
```

**Important:** Ensure Docker Compose is **v2** (command: `docker compose`) not v1 (`docker-compose`).

---

## 🖥️ Operating System Notes

### Windows

**Scripts:** Use `.ps1` (PowerShell) or `.bat` files in `scripts/` directory.

**PowerShell Execution Policy:**
```powershell
# If you get "script execution disabled" error:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**Docker:** Requires WSL2 backend for best performance.

### macOS / Linux

**Scripts:** Use `.sh` (bash/shell) files in `scripts/` directory.

**Make executable:**
```bash
chmod +x scripts/*.sh
```

**Docker:** Native support, no special configuration needed.

---

## 🐳 Docker & Infrastructure

### Docker Compose Basics

**Start all services:**
```bash
docker compose up -d
```

**Stop all services:**
```bash
docker compose down
```

**View running containers:**
```bash
docker compose ps
```

**View logs:**
```bash
# All services
docker compose logs -f

# Specific service
docker compose logs -f postgres
docker compose logs -f redis
docker compose logs -f backend
```

### Infrastructure Diagnostics

**Before deploying changes, always validate:**

```bash
# 1. Validate docker-compose.yml syntax
docker compose config

# 2. Check running services
docker compose ps

# 3. Check service health
docker compose ps --format json | jq '.[].Health'

# 4. View resource usage
docker stats
```

**Common Issues:**

| Problem | Diagnosis | Solution |
|---------|-----------|----------|
| Port already in use | `netstat -ano \| findstr :{{PROJECT_PORT_FRONTEND}}` (Windows)<br>`lsof -i :{{PROJECT_PORT_FRONTEND}}` (Mac/Linux) | Kill process using port or change port in `.env.local` |
| Container won't start | `docker compose logs [service-name]` | Check logs for errors, verify environment variables |
| Database connection failed | `docker compose exec postgres pg_isready` | Ensure PostgreSQL is running and healthy |
| Out of disk space | `docker system df` | Run `docker system prune` to clean up |

### Port Allocation

**This project uses:**
- **Frontend:** {{PROJECT_PORT_FRONTEND}}
- **Backend:** {{PROJECT_PORT_BACKEND}}
- **PostgreSQL:** {{PROJECT_PORT_POSTGRES}}
- **Redis:** {{PROJECT_PORT_REDIS}}
- **MongoDB:** {{PROJECT_PORT_MONGO}}

**Check port conflicts:**
```bash
# Windows
netstat -ano | findstr :{{PROJECT_PORT_FRONTEND}}

# Mac/Linux
lsof -i :{{PROJECT_PORT_FRONTEND}}
```

---

## 📁 Generated Files & Artifacts

### What Gets Committed

**DO commit these generated files:**
- `fundraising/*.docx` - Pitch decks, investor documents
- `docs/*.pdf` - Exported documentation
- `package-lock.json` / `yarn.lock` - Dependency locks
- `.vscode/*.json` - Shared editor settings

**Example:**
```bash
# Generate pitch deck
node scripts/create-pitch-deck.js
# → Outputs: fundraising/02-PITCH-DECK.docx
# ✅ Commit this file

git add fundraising/02-PITCH-DECK.docx
git commit -m "docs: add investor pitch deck"
```

### What Gets Ignored

**DO NOT commit:**
- `.env.local` - Local environment variables (secrets)
- `node_modules/` - Dependencies (restored via npm install)
- `dist/`, `build/` - Build artifacts (recreated on deploy)
- `.DS_Store`, `Thumbs.db` - OS-specific files
- `*.log` - Log files

See `.gitignore` for complete list.

---

## 🧪 Testing & Validation

### Pre-Commit Checklist

Before committing code:

- [ ] **Lint:** `npm run lint` passes with no errors
- [ ] **Format:** `npm run format` applied
- [ ] **Tests:** `npm test` all passing
- [ ] **Build:** `npm run build` succeeds
- [ ] **Docker:** `docker compose config` validates

### Smoke Tests

**After major changes, run smoke tests:**

```bash
# 1. Start fresh environment
docker compose down -v
docker compose up -d

# 2. Wait for services to be healthy
sleep 10

# 3. Test endpoints
curl http://localhost:{{PROJECT_PORT_BACKEND}}/health
curl http://localhost:{{PROJECT_PORT_FRONTEND}}

# 4. Check database connection
docker compose exec postgres pg_isready

# 5. Check Redis
docker compose exec redis redis-cli ping
```

### Infrastructure Validation

**Before deploying to production:**

```bash
# Validate all configurations
docker compose config

# Test database migrations
npm run migrate:test

# Verify environment variables
npm run env:check

# Run integration tests
npm run test:integration

# Build production images
docker compose -f docker-compose.prod.yml build

# Security scan (if available)
npm audit
docker scan {{PROJECT_NAME}}-backend:latest
```

---

## 🚀 Development Workflow

### Starting Development

```bash
# 1. Install dependencies
npm install

# 2. Copy environment template
cp .env.example .env.local

# 3. Start infrastructure
docker compose up -d postgres redis mongo

# 4. Run database migrations
npm run migrate

# 5. Start dev servers
npm run dev
```

### Daily Development

```bash
# Start dev servers (hot reload enabled)
npm run dev

# In separate terminal: watch tests
npm run test:watch

# View logs
docker compose logs -f
```

### Before Pushing Code

```bash
# 1. Run linter
npm run lint

# 2. Run tests
npm test

# 3. Build to verify no errors
npm run build

# 4. Validate Docker config (if changed)
docker compose config

# 5. Stage and commit
git add .
git commit -m "feat: description"
git push
```

---

## 🔧 Troubleshooting

### Common Commands

```bash
# Reset database (destructive!)
docker compose down -v
docker compose up -d postgres
npm run migrate

# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# View Docker logs for specific service
docker compose logs -f backend

# Enter container shell
docker compose exec postgres psql -U postgres
docker compose exec redis redis-cli
docker compose exec backend sh

# Check disk space
docker system df
docker system prune  # Clean up unused resources
```

### Getting Help

1. **Check logs:** `docker compose logs -f [service]`
2. **Verify environment:** `cat .env.local`
3. **Check ports:** `docker compose ps`
4. **Review this guide:** `DEVELOPMENT-GUIDE.md`
5. **Check style guide:** `STYLE-GUIDE.md`
6. **See testing checklist:** `TESTING-CHECKLIST.md`

---

## 📚 Additional Resources

- **Planning & Documentation:** `_START-HERE.md`
- **Code Style & Naming:** `STYLE-GUIDE.md`
- **Testing:** `TESTING-CHECKLIST.md`
- **Architecture Decisions:** `technical/adr/`
- **API Documentation:** `technical/api-spec/`
- **Deployment Guide:** `technical/infrastructure/AZURE-DEPLOYMENT-GUIDE.md`

---

**Questions?** Check `CLAUDE.md` for AI assistant guidance or ask your team lead.

**Version:** 1.0
**Last Updated:** {{CREATION_DATE}}
