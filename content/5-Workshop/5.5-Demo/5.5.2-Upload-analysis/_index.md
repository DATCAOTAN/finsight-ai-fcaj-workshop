---
title: "Upload and analysis"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b>5.5.2.</b> "
---

## Select the document

Use a text-based PDF under 10 MiB. The document must be non-sensitive and must not contain secrets, personal data, real customer data, or instructions intended to manipulate the model.

1. Choose the upload control in the private workspace.
2. Select the PDF.

![Select a non-sensitive PDF](/images/5-Workshop/5.5-Demo/pdf-selected-for-upload.png)

3. Observe upload progress.

![PDF upload progress](/images/5-Workshop/5.5-Demo/pdf-upload-progress.png)

4. Wait for the document to appear in the owner-scoped list.
5. Open the document detail.

## Observe the asynchronous states

The normal path is:

**PENDING_UPLOAD → UPLOADED → QUEUED → EXTRACTING → EXTRACTED → ANALYZING → ANALYZED**

The browser polls with a bounded interval. Do not repeatedly upload the same document or refresh aggressively while processing is active.

![Document analysis in progress](/images/5-Workshop/5.5-Demo/document-processing-state.png)

## What happens behind the interface

- The backend generates the object key and constrained upload form.
- S3 receives the PDF without becoming public.
- Confirmation checks size, metadata, PDF signature, and SHA-256.
- DynamoDB Streams and SQS start the Step Functions workflow once.
- The extractor preserves page boundaries.
- Gemini analyzes the trusted extraction.
- The backend validates schema and citations before storing the result.

If the document has too little embedded text, the result may truthfully report that OCR is required. Do not describe this as an OCR success.
