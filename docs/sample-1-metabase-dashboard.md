---
title: "Sample 1: Build Your First Dashboard in Metabase"
sidebar_position: 1
description: A help center guide for new Metabase users, from a blank screen to a working dashboard.
---

## About This Sample

**Objective:** Demonstrate how to create task-oriented product documentation that helps users complete a workflow in a business intelligence application.

**Approach:** Created a sample procedural guide using a fictional dashboard-building scenario in Metabase. Structured the content around a typical user workflow, from selecting data and configuring visualizations to assembling and saving a dashboard. The instructions are illustrative and have not been validated against a live application.

**Key documentation decisions:**
- Used task-oriented headings to help readers navigate the workflow.
- Organized instructions in the order users would perform them.
- Used numbered steps for actions and explanatory text for supporting information.
- Applied consistent terminology to make instructions easier to follow.
- Included context where needed to help users understand the purpose of each action.

**Skills demonstrated:** User documentation, procedural writing, business intelligence concepts, technical editing, and task-based information design.

**Audience:** New Metabase users with no SQL experience <br />
**Goal:** Go from a blank screen to a working dashboard in about 10 minutes <br />
**Tools:** Metabase (open source) and its built-in Sample Database

**What is Metabase?** Metabase is an open source Business Intelligence (BI) analytics platform that lets users query data, build visualizations, and share dashboards.

## Before you begin

You need access to a Metabase instance. This guide uses the Sample Database that comes with Metabase, so you don't need to connect your own data.

## Step 1: Ask a question

1. Select **+ New** in the top navigation bar, then choose **Question**.
2. Under **Pick your starting data**, choose **Sample Database**, then **Orders**.
3. Select **Summarize**, then choose **Count of rows**.
4. Under **Pick a column to group by**, choose **Created At**, and set the grouping to **Month**.
5. Select **Visualize**. Metabase shows a line chart of orders per month.

## Step 2: Save the question

1. Select **Save**.
2. Name the question **Orders per month**.
3. Choose a collection, then select **Save** again.

## Step 3: Create a dashboard

1. Select **+ New**, then **Dashboard**.
2. Name the dashboard **Sales overview**, choose a collection, and select **Create**.
3. Select the **+** icon to add a chart, then choose **Orders per month**.
4. Drag the chart to where you want it, then select **Save**.

## Step 4: Add a date filter

1. Open the dashboard and select the **pencil** icon to edit it.
2. Select the **filter** icon and choose **Time**.
3. When prompted, select the **Created At** column on your chart.
4. Select **Done**, then **Save**.

You can now use the filter at the top of the dashboard to look at a specific date range.

## Troubleshooting

- **I don't see the Sample Database.** An admin may have hidden it. Ask your Metabase admin to turn it back on.
- **My chart shows one data point.** Check that you grouped by **Created At** and chose **Month**, not **Year**.
- **The filter doesn't change my chart.** Edit the dashboard and confirm the filter is connected to the **Created At** column.

## Next steps

Add a second chart that shows orders by product category, then arrange both charts on the dashboard.