---
title: "Local validation"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b>5.4.1.</b> "
---

## Backend and infrastructure

From the application repository root:

```powershell
$WorkshopRepository = "<path-to-finsight-ai>"
Set-Location $WorkshopRepository

py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"

python -m ruff check .
python -m ruff format --check .
python -m pytest -m "not integration" --cov=backend --cov-report=term-missing
cfn-lint infrastructure/template.yaml
sam validate --lint --template-file infrastructure/template.yaml --region ap-southeast-1
sam build --template-file infrastructure/template.yaml --config-env dev
```

Every command must succeed before deployment. Unit tests use deterministic fixtures and do not call live Gemini.

## Frontend

```powershell
Set-Location .\frontend
corepack pnpm install --frozen-lockfile
corepack pnpm run typecheck
corepack pnpm test
corepack pnpm run build
corepack pnpm audit --prod
Set-Location ..
```

Confirm the repository remains clean:

```powershell
git status --short --branch
```

If generated configuration, credentials, PDFs, or build output appears as tracked source, stop and correct the local setup before continuing.
