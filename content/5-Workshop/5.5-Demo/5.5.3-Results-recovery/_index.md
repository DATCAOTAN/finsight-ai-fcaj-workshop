---
title: "Results and recovery"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b>5.5.3.</b> "
---

## Successful result

When the status reaches **ANALYZED**, inspect:

- overview and key financial metrics;
- trends, risks, anomalies, and limitations;
- page citations that can be checked against the source PDF;
- extraction and analysis provenance;
- provider and model disclosure showing Gemini gemini-2.5-flash;
- the financial-analysis disclaimer.

The result should summarize the source document without inventing values or providing personalized investment advice.

![Structured analysis result](/images/5-Workshop/5.5-Demo/analysis-result-summary.png)

![Metrics, risks, and page citations](/images/5-Workshop/5.5-Demo/analysis-citations-provider.png)

## Controlled failure behavior

If analysis ends in **ANALYSIS_FAILED**:

1. Read the sanitized failure category shown by the UI.
2. Do not edit DynamoDB or re-send queue messages.
3. If the UI marks the failure retryable, wait for the displayed cooldown and choose **Retry analysis** once.
4. If the input is too large or unsuitable, use a smaller text-based PDF.

The system never automatically switches from Gemini to another provider.

## Delete the workshop document

After the document reaches a terminal state, choose **Delete document** and confirm. The application removes the owner's document artifacts and versions through the protected API. If processing is still active, deletion returns a conflict; wait for a terminal state instead of changing backend records.
