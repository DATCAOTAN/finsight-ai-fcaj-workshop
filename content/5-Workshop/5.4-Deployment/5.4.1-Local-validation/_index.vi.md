---
title: "Kiểm tra cục bộ"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b>5.4.1.</b> "
---

## Backend và hạ tầng

Từ thư mục gốc của repository ứng dụng:

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

Mọi lệnh phải thành công trước khi deploy. Unit test sử dụng fixture xác định và không gọi Gemini thật.

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

Xác nhận repository vẫn sạch:

```powershell
git status --short --branch
```

Nếu configuration sinh ra, credential, PDF hoặc build output xuất hiện như source được theo dõi, hãy dừng lại và sửa môi trường cục bộ trước khi tiếp tục.
