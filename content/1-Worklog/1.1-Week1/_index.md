---
title: "Week 1 Worklog"
date: 2026-06-22
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

**Period:** 22–28 June 2026

## Objectives

- Define the FinSight AI problem, scope, and sensitive-data boundaries.
- Establish core AWS and shared-responsibility knowledge.
- Design the initial serverless architecture and Infrastructure as Code environment.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| AWS Global Infrastructure | Understood Regions, Availability Zones, and the choice of `ap-southeast-1`. |
| IAM and Shared Responsibility | Distinguished AWS and customer security duties and applied least privilege. |
| AWS SAM and CloudFormation | Learned to declare, validate, and repeatedly deploy serverless resources. |

### Work completed

- Analysed the backend path from API Gateway and Lambda to S3 and DynamoDB.
- Established IAM boundaries, private storage, and encryption as baseline requirements.
- Created the SAM/CloudFormation structure and template-validation workflow.

## Results and evidence

- Completed the architecture and MVP scope.
- Defined owner-scoped access, private documents, and the exclusion of investment advice.
- Organised the repository into backend, infrastructure, tests, and documentation.
