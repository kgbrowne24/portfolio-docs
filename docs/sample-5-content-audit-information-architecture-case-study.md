---
title: "Sample 5: Content Audit and Rewrite"
sidebar_position: 5
description: A content audit, information architecture redesign, and documentation rewrite for a fictional data platform.
---

# Content Audit and Information Architecture Redesign


## About This Sample

**Objective:** Demonstrate how a content audit and information architecture redesign can improve the clarity, organization, and usability of technical documentation.

**Approach:** Evaluated a fictional data platform's documentation for structural, editorial, and usability issues. Developed a content inventory, identified opportunities to consolidate and reorganize information, and proposed a revised navigation structure. Included a before-and-after content example to demonstrate how individual pages could be improved.

**Key documentation decisions:**
- Organized documentation around user tasks rather than internal product terminology.
- Consolidated overlapping content to reduce duplication and maintenance overhead.
- Revised page titles and navigation labels to improve discoverability.
- Applied task-oriented writing principles to improve clarity and usability.
- Defined success criteria for evaluating the proposed changes.

**Skills demonstrated:** Content strategy, information architecture, content auditing, technical editing, documentation usability, and UX writing.

*Portfolio sample based on a fictional data platform. Findings and recommendations are illustrative; improvements have not been measured against a live documentation site.*

## Project overview

**Scenario:** Meridian Data Platform provides tools for configuring data sources, ingesting datasets, managing access, and monitoring processing jobs. As the platform evolved, its documentation grew without a consistent structure. Related instructions appeared in multiple locations, page titles reflected internal team terminology, and users had difficulty identifying where to start.

**Objective:** Evaluate a representative set of documentation pages and propose a task-oriented structure that helps developers and data engineers find the right instructions with fewer decisions.

**Audience:** Developers integrating with the platform, data engineers configuring ingestion workflows, and administrators managing access.

**Scope:** A sample inventory of 12 fictional documentation pages, navigation redesign, and a representative content rewrite. This exercise does not include user research or implementation in a live product.

## 1. Audit approach

I assessed the sample pages against five criteria:

| Criterion | Review question |
| --- | --- |
| Findability | Can users predict where a page lives from its title and navigation label? |
| Task completion | Does the page provide prerequisites, ordered steps, and a verifiable outcome? |
| Accuracy and consistency | Are terms, commands, and cross-references internally consistent? |
| Redundancy | Does content duplicate or conflict with another page? |
| Maintenance | Is ownership or review status clear enough to support updates? |

Each page received a recommended action: **keep**, **revise**, **merge**, **move**, or **retire**. These are editorial recommendations, not evidence of completed changes.

## 2. Representative content inventory

| ID | Existing page | Observed issue | Recommended action | Proposed destination |
| --- | --- | --- | --- | --- |
| 01 | Platform Overview | Describes features but offers no next step | Revise | Start here / Overview |
| 02 | First Steps | Vague title; prerequisites scattered elsewhere | Revise | Start here / Quickstart |
| 03 | Credentials | Mixes key creation with authorization concepts | Split and revise | Security / API keys; Security / Permissions |
| 04 | Sources | Broad reference page with setup instructions embedded | Split and revise | Connect data / Supported sources; Connect data / Configure a source |
| 05 | Upload Data | Overlaps with Batch Import | Merge | Ingest data / Submit a dataset |
| 06 | Batch Import | Duplicates upload instructions with different terminology | Merge | Ingest data / Submit a dataset |
| 07 | Processing States | Explains status values without showing how to check them | Revise | Monitor jobs / Check job status |
| 08 | Job Errors | Troubleshooting separated from job status workflow | Move and revise | Monitor jobs / Resolve failed jobs |
| 09 | API Basics | Authentication and request conventions buried in prose | Revise | API reference / API conventions |
| 10 | Roles Matrix | Useful reference but difficult to discover | Move | Security / Roles and permissions |
| 11 | FAQ | Mixed questions repeat several task pages | Distribute; retire shell | Relevant task pages |
| 12 | Legacy Connector Setup | Uses a discontinued integration pattern in the scenario | Retire with redirect | Connect data / Configure a source |


## 3. Information architecture: before and after

### Before: feature- and team-oriented navigation

```text
Documentation
├── Platform Overview
├── First Steps
├── API Basics
├── Credentials
├── Sources
├── Upload Data
├── Batch Import
├── Processing States
├── Job Errors
├── Roles Matrix
├── FAQ
└── Legacy Connector Setup
```

**Problems:** All pages compete at the same level; related tasks are separated; vague labels require users to guess; and deprecated content remains alongside current instructions.

### After: user-task-oriented navigation

```text
Documentation
├── Start here
│   ├── Overview
│   └── Quickstart
├── Connect data
│   ├── Supported sources
│   └── Configure a source
├── Ingest data
│   └── Submit a dataset
├── Monitor jobs
│   ├── Check job status
│   └── Resolve failed jobs
├── Security
│   ├── API keys
│   └── Roles and permissions
└── API reference
    └── API conventions
```

**Benefits:** The new top-level categories reflect tasks and questions users bring to the site. Action-oriented page titles clarify expected outcomes. Reference material remains available but does not interrupt the primary onboarding and ingestion paths.


## 4. Example rewrite: from feature description to task guide

### Before: “Processing States” (excerpt)

> Processing states show what is happening with jobs. Jobs can be pending, running, completed, or failed. The jobs interface contains information about the state of each job. Users should check the interface to see if their jobs are done. If a job fails, review the errors and try again.

**Issues identified:** The title describes a concept rather than a task; the text gives no location, prerequisite, procedure, or completion criterion; and “try again” may be unsafe for non-idempotent submissions.

### After: “Check job status” (proposed replacement)

# Check job status

After submitting a dataset, check its ingestion job to confirm whether processing has finished.

**Before you begin**

- Obtain the `job_id` returned by the dataset submission request.
- Configure an API key with permission to read job status.

**Procedure**

1. Send a `GET` request to `/v1/jobs/{job_id}`.
2. Read the `status` field in the response.
3. If the status is `pending` or `running`, wait before checking again.
4. If the status is `completed`, confirm that the processed record count matches your expectations.
5. If the status is `failed`, review the job error details before deciding whether to resubmit data.

**Example request**

```bash
curl --request GET \
  --url "https://api.example.com/v1/jobs/job_7821" \
  --header "Authorization: Bearer $MERIDIAN_API_KEY"
```

**Example response**

```json
{
  "job_id": "job_7821",
  "status": "completed",
  "records_processed": 2,
  "records_failed": 0
}
```

**Expected result:** The job reports `completed`, and the processed record count is consistent with the submitted dataset.

**If the job fails:** Open **Resolve failed jobs** to inspect error details. Do not automatically resubmit the same data unless the API guarantees safe retries or supports idempotency.

> The endpoint, permissions, and responses above are fictional examples and have not been validated against a live API.

### What changed—and why

| Before | After | Benefit to evaluate |
| --- | --- | --- |
| Concept-focused title | “Check job status” | Clearer task recognition |
| Descriptive paragraph | Prerequisites and numbered procedure | More actionable instructions |
| No technical example | Request and sample response | Easier implementation |
| “Try again” | Conditional failure guidance | Lower risk of duplicate ingestion |
| No success criterion | Explicit expected result | Easier verification |

## 5. Proposed implementation plan

1. **Validate with SMEs:** Review navigation and terminology with representative developers and platform subject-matter experts.
2. **Confirm content ownership:** Assign maintainers to each section and flag pages requiring technical verification.
3. **Implement navigation:** Create the new section hierarchy and descriptive titles in the documentation site.
4. **Migrate content:** Merge duplicates, rewrite priority task pages, and update cross-references.
5. **Handle retired pages:** Add redirects or deprecation notices where appropriate; check for broken links.
6. **Quality-check:** Test procedures, review terminology, check accessibility, and confirm navigation works on mobile and desktop.
7. **Evaluate:** Collect feedback and measure whether users can locate and complete key tasks.

## 6. Success criteria and measurement plan

Because this is a hypothetical redesign, the following are **proposed measures**, not achieved outcomes.

| Goal | Proposed measure | Evaluation method |
| --- | --- | --- |
| Improve findability | Time and success rate for locating key tasks | Moderated or unmoderated task tests before and after |
| Reduce duplication | Number of overlapping instructions | Follow-up content inventory |
| Improve task completion | Percentage of testers who finish a documented workflow | Scenario-based usability testing |
| Improve maintenance | Percentage of pages with an owner and review date | Documentation metadata audit |
| Reduce dead ends | Broken-link count and navigation exits | Link checker and analytics, where available |


## 7. Deliverables and skills demonstrated

**Deliverables in this case study:** A sample content inventory, editorial recommendations, before-and-after navigation model, task-based rewrite, implementation plan, and evaluation framework.

**Skills demonstrated:** Content auditing, information architecture, audience-centered organization, technical editing, task-based documentation, cross-reference strategy, and documentation governance.

## Limitations

This is a conceptual portfolio exercise, not a report of work performed for a real client. The inventory is intentionally small, the platform is fictional, and the recommended structure has not been validated with actual users. A real project would require stakeholder interviews, technical review, analytics, and usability testing before rollout.
