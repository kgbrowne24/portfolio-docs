---
title: "Sample 6: Integrate with the Meridian Data Platform API"
sidebar_position: 6
description: Use the Meridian Data Platform REST API to submit datasets, monitor ingestion jobs, and verify that data is available for downstream analytics.
---
import workflowImage from '@site/static/img/data-ingestion-workflow.png';

# Integrate with the Meridian Data Platform API

This guide walks through a basic integration, from authenticating an API request to confirming a successful ingestion.

## About This Sample

**Objective:** Demonstrate how to document a REST API integration for developers, using a fictional data ingestion platform.

**Approach:** Structured the guide around the developer's workflow, from authentication and dataset submission to monitoring ingestion and verifying results. Included example requests and responses, troubleshooting guidance, and a workflow diagram to support understanding.

**Key documentation decisions:**
- Organized the content by task rather than API endpoint.
- Used code examples and expected responses to clarify each step.
- Distinguished successful API submission from completed data processing.
- Included troubleshooting and error-handling guidance to support implementation.

**Skills demonstrated:** API documentation, developer documentation, information architecture, Markdown/MDX, and visual technical communication.

*Portfolio sample using a fictional API. Examples are illustrative and have not been validated against a live service.*

## Overview

The Meridian API enables applications and automated workflows to submit structured data for processing.

A typical integration follows four steps:

1. Authenticate using an API key.
2. Submit a dataset for ingestion.
3. Retrieve the ingestion job status.
4. Verify that processing completed successfully.

<img
  src={workflowImage}
  alt="Data ingestion workflow showing authentication, dataset submission, job monitoring, and verification"
  style={{ width: '100%', height: 'auto' }}
/>

### Prerequisites

Before you begin, make sure you have:

- Access to a Meridian development environment
- An API key with `datasets:write` and `jobs:read` permissions
- A terminal with cURL installed
- Basic familiarity with REST APIs and JSON

**Base URL**

All examples use the following placeholder URL:

`https://api.example.com/v1`

Replace this URL with the endpoint for your environment.

## Step 1: Configure authentication

Meridian uses API keys to authenticate requests. Include your API key in the `Authorization` header using the Bearer authentication scheme.

For security, store your key in an environment variable rather than embedding it directly in scripts.

**macOS or Linux**

```bash
export MERIDIAN_API_KEY="your-api-key"
```

To confirm that the variable is set without displaying the key:

```bash
if [ -n "$MERIDIAN_API_KEY" ]; then
  echo "API key configured"
fi
```

All subsequent requests use the environment variable.

**Authentication header**

```http
Authorization: Bearer <your-api-key>
```

Never commit API keys to source control or include them in application logs.

## Step 2: Submit a dataset

Send a `POST` request to `/datasets` to submit a dataset for asynchronous ingestion.

The request body includes the dataset name, data format, and records to process.

### Request

```bash
curl --request POST \
  --url https://api.example.com/v1/datasets \
  --header "Authorization: Bearer $MERIDIAN_API_KEY" \
  --header "Content-Type: application/json" \
  --data '{
    "name": "sales_transactions",
    "format": "json",
    "records": [
      {
        "transaction_id": "TXN-1001",
        "amount": 149.99,
        "currency": "USD"
      },
      {
        "transaction_id": "TXN-1002",
        "amount": 89.50,
        "currency": "USD"
      }
    ]
  }'
```

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | Yes | Unique dataset name within the workspace |
| `format` | string | Yes | Data format; this example supports `json` |
| `records` | array | Yes | One or more records to ingest |
| `transaction_id` | string | Yes | Unique transaction identifier |
| `amount` | number | Yes | Transaction amount |
| `currency` | string | Yes | Three-letter ISO currency code |

### Example response

**HTTP 202 Accepted**

```json
{
  "dataset_id": "ds_10482",
  "job_id": "job_7821",
  "status": "pending",
  "submitted_records": 2,
  "created_at": "2026-11-01T14:30:00Z"
}
```

A `202 Accepted` response indicates that the platform accepted the request for processing. It does not mean ingestion is complete.

Save the `job_id` from the response. You'll use it to check the ingestion status.

## Step 3: Monitor ingestion status

Ingestion jobs run asynchronously. Use the job ID returned in Step 2 to monitor processing.

### Request

```bash
curl --request GET \
  --url https://api.example.com/v1/jobs/job_7821 \
  --header "Authorization: Bearer $MERIDIAN_API_KEY"
```

### Example response

**HTTP 200 OK**

```json
{
  "job_id": "job_7821",
  "dataset_id": "ds_10482",
  "status": "completed",
  "records_processed": 2,
  "records_failed": 0,
  "completed_at": "2026-11-01T14:30:08Z"
}
```

### Job statuses

| Status | Description | Recommended action |
|---|---|---|
| `pending` | Job is queued for processing | Wait and check again |
| `running` | Records are being processed | Continue monitoring |
| `completed` | Processing finished successfully | Verify the dataset |
| `failed` | Processing stopped because of an error | Review the error details |

For automated integrations, poll the status endpoint until the job reaches `completed` or `failed`.

Start with a five-second polling interval and increase the interval for long-running jobs. Avoid sending continuous requests without a delay.

## Step 4: Verify the dataset

After the ingestion job completes, retrieve the dataset metadata to confirm that the expected records are available.

### Request

```bash
curl --request GET \
  --url https://api.example.com/v1/datasets/ds_10482 \
  --header "Authorization: Bearer $MERIDIAN_API_KEY"
```

### Example response

**HTTP 200 OK**

```json
{
  "dataset_id": "ds_10482",
  "name": "sales_transactions",
  "status": "available",
  "record_count": 2,
  "last_updated": "2026-11-01T14:30:08Z"
}
```

Confirm that:

- `status` is `available`.
- `record_count` matches the number of records submitted.
- `last_updated` reflects the latest ingestion.

If the record count is unexpected, review the job status and any record-level errors before retrying the request.



## Troubleshooting

The following table describes common API errors and recommended resolutions.

| HTTP status | Error | Possible cause | Resolution |
|---|---|---|---|
| 400 | Bad Request | Invalid JSON or missing required fields | Validate the request body and parameter names |
| 401 | Unauthorized | Missing, invalid, or expired API key | Verify the API key and authentication header |
| 403 | Forbidden | Insufficient API permissions | Confirm the key has the required scopes |
| 404 | Not Found | Invalid dataset or job ID | Verify the resource ID and environment |
| 429 | Too Many Requests | API rate limit exceeded | Wait before retrying; use `Retry-After` when provided |
| 500 | Internal Server Error | Unexpected server-side failure | Retry with backoff; contact support if the issue persists |

### Example error response

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "The 'name' field is required.",
    "request_id": "req_98342"
  }
}
```

Use the `request_id` when contacting support so the request can be traced in service logs.

### Retry recommendations

For production integrations:

- Retry temporary failures such as HTTP 429, 502, 503, and 504 using exponential backoff.
- Honor the `Retry-After` header when present.
- Do not automatically retry invalid requests (HTTP 400) without correcting the payload.
- Avoid automatically resubmitting ingestion requests unless the API supports idempotency, to prevent duplicate data.

## Integration checklist

Before moving your integration to production, verify that:

- [ ] API credentials are stored securely.
- [ ] Authentication and required permissions are configured.
- [ ] Dataset requests contain valid JSON.
- [ ] Ingestion jobs are monitored to completion.
- [ ] Processed record counts are verified.
- [ ] API errors are handled appropriately.
- [ ] Retry logic prevents unnecessary requests and duplicate ingestion.
- [ ] Sensitive information is excluded from application logs.

## Next steps

After validating basic integration, consider extending implementation to:

- Automate scheduled ingestion from external data sources.
- Add monitoring and alerting for failed ingestion jobs.
- Implement request logging and correlation IDs.
- Integrate the processed datasets with downstream reporting or analytics workflows.

---

*Portfolio demonstration — Fictional API and illustrative responses.*
