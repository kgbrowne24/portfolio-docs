---
title: "Sample 1: Build Your First Dashboard in Tableau Public"
sidebar_position: 1
description: A help center guide for new Tableau Public users, from a CSV file to a published dashboard, with no software to install.
---

## About This Sample

**Objective:** Show how I write task-based help content that takes a new user from a data file to a finished dashboard in a business intelligence tool.

**Audience:** New Tableau Public users with no prior experience

**Goal:** Build and publish a two-chart dashboard in about 20 minutes

**Tools:** Tableau Public web authoring (free, runs in a browser) and a small sample CSV file

**Tested with:** Tableau Public web authoring, November, 2026.

**Approach:** I wrote this guide after completing the workflow myself. I used a short fictional dataset that readers can download, so everyone works with the same data and sees the same results. I split the task into four stages (connect to data, build two charts, assemble a dashboard, publish) and ended each stage with a visible result, so readers can stop and resume without losing their place.

**Key documentation decisions:**

- **Started with the reader's goal.** Headings describe what the reader is doing, such as "Build a dashboard," instead of naming product features.
- **Required no installation.** The guide uses web authoring, so readers need only a free account and a browser.
- **Supplied the data.** A small downloadable file means readers don't have to find or clean a dataset before they begin.
- **Matched the interface exactly.** Button, menu, and field names appear in bold, in the order readers will see them.
- **Planned for common problems.** The troubleshooting section covers the issues a new user is most likely to hit.
- **Warned about public data.** Anything published to Tableau Public is visible to everyone, so the guide says so before the publish step.

**Skills demonstrated:** User documentation, procedural writing, task-based information design, technical editing, and business intelligence concepts.

---

## Before you begin

You need a free Tableau Public account and the sample data file. You don't need to install anything.

1. Go to [public.tableau.com](https://public.tableau.com) and select **Sign Up** to create a free account. Activate it using the email Tableau sends you.
2. Download the sample file: [coffee-sales.csv](./assets/coffee-sales.csv).

The file contains a year of fictional sales for a coffee company, with these columns:

| Column | What it contains |
| --- | --- |
| **Order Date** | The date of the sales record |
| **Region** | East, West, or Central |
| **Product Category** | Beans or Equipment |
| **Sales** | Sales in dollars |
| **Quantity** | Number of items sold |

:::caution
Tableau Public makes everything you publish visible to anyone. Use only data that is safe to share. The sample file is fictional, so it's safe to publish.
:::

## Step 1: Connect to the data

1. Sign in to Tableau Public and select **Create**, then **Web Authoring**.
2. Upload **coffee-sales.csv** by selecting the file or dragging it into the window.
3. On the data source page, check that the five columns appear in the preview.
4. Select **Sheet 1** at the bottom of the window to open the workspace.

## Step 2: Build a chart of sales over time

1. Drag **Order Date** to **Columns**.
2. Select the arrow on the **Order Date** field and choose **Month**. Choose the version that shows month names, not the version that shows only month numbers.
3. Drag **Sales** to **Rows**.
4. Tableau draws a line chart of sales by month.
5. Right-click the **Sheet 1** tab, choose **Rename**, and enter **Sales by month**.

## Step 3: Build a chart of sales by region

1. Select the **New Worksheet** icon at the bottom of the window.
2. Drag **Region** to **Columns**.
3. Drag **Sales** to **Rows**. Tableau draws a bar chart with one bar for each region.
4. Drag **Product Category** to **Color** on the **Marks** card. Each bar now shows how much came from Beans and how much from Equipment.
5. Rename the sheet **Sales by region**.

## Step 4: Build the dashboard

1. Select the **New Dashboard** icon at the bottom of the window.
2. Drag **Sales by month** from the sheet list into the dashboard area.
3. Drag **Sales by region** below it.
4. Select the **Sales by region** chart, then select the **Use as Filter** icon (a funnel) in the chart's top-right corner.
5. Select a bar. The **Sales by month** chart updates to show only that selection. Select the same bar again to clear it.
6. Rename the dashboard **Coffee sales overview**.

## Step 5: Save and publish

1. Click the blue **Publish** button in the top toolbar.
2. Enter a name for the workbook, such as **Coffee sales dashboard**, then select **Publish**.
3. Open your Tableau Public profile to view the published dashboard.

You can share your dashboard by copying the link from your browser.

## Troubleshooting

- **My file won't upload.** Check that the file ends in `.csv` and wasn't changed when you opened it in a spreadsheet program. Download it again if needed.
- **Order Date shows as text, not a date.** On the data source page, select the data type icon next to **Order Date** and choose **Date**.
- **My line chart shows one point per year.** Change **Order Date** to **Month**, as described in Step 2.
- **The filter doesn't change the other chart.** Select the **Sales by region** chart in the dashboard and confirm that the **Use as Filter** icon is turned on.
- **I don't see Web Authoring.** Confirm that you're signed in and that you activated your account from the email Tableau sent.

## Next steps

Add a third chart that shows the quantity sold by product category, then add it to your dashboard.
