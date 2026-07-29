---
title: "Authentication"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b>5.5.1.</b> "
---

1. Open the CloudFront URL stored in **$WorkshopFrontendUrl**.
2. Choose **Create account**.
3. Enter the controlled workshop email and a unique password that satisfies the displayed policy.
4. Submit the form. The account remains unconfirmed and cannot receive AWS credentials.

![Create a controlled workshop account](/images/5-Workshop/5.5-Demo/create-account-form.png)

5. Read the confirmation code from the controlled mailbox.
6. Choose **Confirm email**, enter the same email and code, and submit.
7. Choose **Sign in** and authenticate.

After sign-in, the browser exchanges Cognito tokens for short-lived Identity Pool credentials and uses them only in memory to sign API requests. Do not inspect, copy, or capture the token or credential values.

## Expected result

- An unconfirmed user cannot enter the private workspace.
- A confirmed user sees an empty owner-scoped document list.
- Refreshing the page restores the Cognito session without storing long-lived AWS credentials.

![Confirmed user workspace](/images/5-Workshop/5.5-Demo/confirmed-user-workspace.png)

![Empty owner-scoped document list](/images/5-Workshop/5.5-Demo/document-list-empty.png)

For an optional isolation check, create a second controlled user and verify that each account sees only its own document list. Do not show raw Cognito identity IDs.
