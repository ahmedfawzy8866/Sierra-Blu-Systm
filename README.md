# Sierra-Blu-Systm

> **Status:** early scaffold — no application code yet.

## What is this?

Sierra-Blu-Systm is a Node.js project intended for deployment to Azure App Service.
Application source code has not been added yet; this repository currently contains only
the CI/CD scaffolding and project configuration.

---

## Prerequisites

| Tool | Minimum version |
|------|----------------|
| Node.js | 20.x |
| npm | 10.x |

## Local setup

```bash
# 1. Install dependencies (deterministic, uses lockfile)
npm ci

# 2. Run the app
npm start

# 3. Run tests
npm test

# 4. Run a build (if applicable)
npm run build
```

---

## CI/CD policy

| Event | Workflow | What it does |
|-------|----------|-------------|
| Push to `main` or any PR | `ci.yml` | Install (`npm ci`), test, build |
| Manual trigger only | `azure-webapps-node.yml` | Build + deploy to Azure App Service |

### Lockfile strategy

- **Always** commit `package-lock.json`.
- CI uses `npm ci` (not `npm install`) to ensure deterministic, locked installs.
- Never commit `node_modules/`.

---

## Deployment

Target: **Azure App Service**

Required repository secrets (Settings → Secrets → Actions):

| Secret | Description |
|--------|-------------|
| `AZURE_WEBAPP_PUBLISH_PROFILE` | Publish profile downloaded from the Azure Portal |

Required configuration (edit `.github/workflows/azure-webapps-node.yml`):

| Variable | Description |
|----------|-------------|
| `AZURE_WEBAPP_NAME` | Your Azure Web App name |
| `NODE_VERSION` | Node.js version (default `20.x`) |

---

## Repository conventions

- **Branches:** `main` (protected) · feature branches named `feature/<short-description>`
- **Lockfile:** `package-lock.json` must be committed and kept up to date
- **Releases:** tag `main` with `vMAJOR.MINOR.PATCH` after merging a release PR
- **CI gates:** all PRs must pass the `ci.yml` workflow before merging
