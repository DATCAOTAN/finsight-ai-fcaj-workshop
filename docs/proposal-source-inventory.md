# FinSight AI Proposal source inventory

This internal inventory records the evidence used for the bilingual FCAJ Proposal. It is not Hugo content and does not appear in site navigation.

## Authoritative application sources inspected

- `README.md`
- `infrastructure/template.yaml` and `samconfig.toml` (configuration structure only; sensitive deployment values were not copied)
- `backend/shared/analysis.py`, document-state helpers, extraction helpers, and the upload, confirmation, extraction, analysis, result, retry, and deletion handlers
- `frontend/src/App.tsx`, `frontend/src/api.ts`, `frontend/src/auth.ts`, and `frontend/src/types.ts`
- `docs/contracts/result-schema-v1.md` and extraction/processing contracts
- `docs/architecture/current-system-inventory.md`, `cost-and-cleanup.md`, phase documents, authentication/frontend notes, and extraction-quality notes
- `docs/security/ai-data-egress.md` and `cross-owner-testing.md`
- provider ADRs, release-readiness evidence, project worklogs, and release notes
- backend, frontend, infrastructure, and deployed-test evidence
- Git history and release tags, including `v1.1.0-gemini-dev`

## Verified services and components

- React, Vite, TypeScript, private Amazon S3 frontend origin, and Amazon CloudFront with Origin Access Control
- Amazon Cognito User Pool and Identity Pool, confirmed-email registration, temporary credentials, and browser SigV4
- Amazon API Gateway with `AWS_IAM` authorization and AWS Lambda handlers
- private, versioned Amazon S3 document/artifact storage
- Amazon DynamoDB in on-demand mode with DynamoDB Streams
- Amazon SQS processing queue and dead-letter queue
- AWS Step Functions Standard workflow
- Amazon CloudWatch Logs, embedded metrics, metrics, and 10 alarms
- AWS Secrets Manager for external-provider credentials
- Amazon Bedrock provider implementation, Google Gemini provider implementation, and retained Groq provider implementation
- AWS SAM and AWS CloudFormation for Infrastructure as Code

## Provider state

- Active development provider: Google Gemini, model `gemini-2.5-flash`
- Source/template default: Amazon Bedrock; live acceptance remains blocked by account-level quota
- Implemented but inactive: Groq
- Provider selection is trusted server-side deployment configuration
- No automatic provider fallback exists
- In Gemini mode, trusted extracted page text and bounded extraction metadata leave AWS; the original PDF binary stays in private AWS storage

## Verified final evidence used selectively

- Release tag: `v1.1.0-gemini-dev`
- Release merge: `fd253c20035872c4840e5b2811424b27e38dbd49`
- Classification: `FINSIGHT_AI_PROJECT_COMPLETE_GEMINI_DEVELOPMENT_PROVIDER`
- Server-side analysis limit: 1,000,000 characters, with no silent truncation
- Long-document acceptance: 214,091 characters, 67,723 input tokens, 609 output tokens, one provider call, terminal state `ANALYZED`
- Oversized-input acceptance: 1,368,551 characters, `ANALYSIS_INPUT_TOO_LARGE`, zero provider calls
- Security acceptance: owner isolation, safe foreign-access 404, unsigned API 403, and direct S3 403
- Test evidence: 288 backend tests at 86% coverage and 22 frontend tests
- AWS snapshot: `UPDATE_COMPLETE`, 73 healthy resources, 10/10 alarms `OK`, clean processing queue and DLQ, no running workflow, and acceptance data removed

## Project dates

- Eight-week FCAJ period: 22 June 2026 through 15 August 2026
- Evidence cutoff for completed work in this Proposal: 29 July 2026
- Weeks 1–5: completed
- Week 6: in progress
- Weeks 7–8: planned

## Explicitly excluded or not implemented

- Amazon Textract and OCR execution
- RAG, vector search, and Amazon OpenSearch
- Amazon RDS, Amazon ECS, Amazon EKS, and Amazon SageMaker
- Route 53, AWS WAF, AWS X-Ray, AWS CloudTrail, and AWS Config as application components
- customer-managed AWS KMS keys
- NAT Gateway and continuously running compute
- model fine-tuning, automatic trading, investment recommendations, and a production SLA
- multi-region disaster recovery and legal or regulatory certification

## Unsupported claims avoided

- The Gemini development deployment is not described as fully AWS-native.
- No AWS service is described as free or infinitely scalable.
- No exact project cost or remaining promotional-credit balance is claimed.
- No production certification, guaranteed accuracy, guaranteed compliance, or financial recommendation is claimed.
- No company, bank, fund, or financial-institution adoption is claimed.
- No second team-member identity, individual responsibility, contribution split, or commit attribution is published.

## Unresolved Proposal information

- The authoritative architecture diagram is maintained separately and awaits manual Draw.io validation before insertion.
- Live Amazon Bedrock inference remains blocked by account-level quota.
- AWS promotional-credit balance, expiry, and eligibility remain operator evidence outside source control.
- An authoritative resource-attributed project cost total is unavailable; Cost Explorer evidence is account-level.
- OCR remains outside the current release.
