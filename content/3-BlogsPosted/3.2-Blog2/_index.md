---
title: "Blog 2"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon S3 Express One Zone - Hyper-fast Storage for Database and Analytics

We typically think of Amazon S3 as cheap, highly durable object storage, but with "moderate" retrieval speeds. However, after reading an AWS Storage Blog post about how Turso (a distributed database) utilizes S3, my perspective completely changed, thanks to **Amazon S3 Express One Zone**.

### The Core Difference
**S3 Express One Zone** is a new storage class purpose-built for data-intensive workloads that demand consistent **single-digit millisecond latency**.

The blog details how Turso used this class as the durability layer for their transactional database. Instead of relying on expensive EBS volumes or EFS, they write data directly to S3 Express One Zone while still achieving astonishing database performance.

### Why is it so fast?
* **Single-Zone Architecture:** Unlike S3 Standard, which replicates data across at least three Availability Zones (AZs), Express One Zone stores data in a single AZ of your choosing. This eliminates inter-datacenter replication latency.
* **API Optimization:** It utilizes a distinct session-based authentication mechanism that dramatically speeds up API call response times.

While storing data in a single AZ entails a slightly higher risk in the event of an AZ-level disaster, S3 Express One Zone is the perfect drop-in replacement for caching layers, AI/ML data processing, or financial modeling where raw speed is the ultimate priority.

*Reference: [How Turso built a transactional database using Amazon S3 Express One Zone](https://aws.amazon.com/blogs/storage/)*
