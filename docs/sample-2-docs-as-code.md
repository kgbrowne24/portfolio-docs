---
title: "Sample 2: Docs-as-Code Site"
sidebar_position: 2
description: How this portfolio is built with Markdown, Git, pull requests, and Docusaurus on GitHub Pages.
---

## About This Sample

**Objective:** Demonstrate how a docs-as-code workflow supports collaborative documentation development, version control, and consistent publishing.

**Approach:** Created a documentation sample using Markdown, Git, GitHub, and Docusaurus. Organized the content to illustrate how documentation changes can be authored, reviewed, and maintained through a version-controlled workflow.

**Key documentation decisions:**
- Used Markdown to keep documentation portable, readable, and easy to maintain.
- Organized documentation within a Docusaurus site to demonstrate structured navigation and publishing.
- Illustrated how Git branches and pull requests support collaborative review.
- Applied consistent formatting and content organization to improve maintainability.
- Used GitHub to make the documentation source accessible alongside the published site.

**Skills demonstrated:** Docs-as-code, Markdown/MDX, Git, GitHub, Docusaurus, documentation maintenance, and technical collaboration.


**Audience:** Hiring managers and engineers reviewing my workflow <br />
**What it shows:** Markdown authoring, Git branches and pull requests, and a static site built with Docusaurus

## Repository layout

```
portfolio-docs/
├── docs/
│   ├── intro.md
│   ├── sample-1-metabase-dashboard.md
│   ├── sample-2-docs-as-code.md
│   ├── sample-3-wifi-troubleshooting.md
│   ├── sample-4-git-basics-training.md
│   └── sample-5-content-audit.md
├── static/img/
├── docusaurus.config.js
├── sidebars.js
├── README.md
└── package.json
```

## README.md

```markdown
# Kelly Browne: Documentation Portfolio

Writing samples for technical documentation, help center content, and training.

## View the site

https://kgbrowne24.github.io/portfolio-docs/

## Run it locally

1. Install a current LTS version of Node.js.
2. Clone this repository and run `npm install`.
3. Run `npm start`. The site opens at http://localhost:3000/portfolio-docs/.

## How I work

- Each sample is a Markdown file in `docs/`.
- I make changes on a branch and merge them through a pull request.
- I publish the site with `npm run deploy`.
```

## Site configuration (excerpt)

```js
// docusaurus.config.js
module.exports = {
  title: 'Kelly Browne: Documentation Portfolio',
  tagline: 'Technical writing, help content, and training',
  url: 'https://kgbrowne24.github.io',
  baseUrl: '/portfolio-docs/',
  organizationName: 'kgbrowne24',
  projectName: 'portfolio-docs',
  trailingSlash: false,
  onBrokenLinks: 'throw',
};
```

## Sample page with front matter

```markdown
---
id: wifi-no-internet
title: Wi-Fi is connected but there is no internet
sidebar_position: 1
description: Steps to restore internet access when your device shows Wi-Fi connected.
---

Your device shows a Wi-Fi connection, but pages won't load.

:::tip
Check whether other devices have the same problem first. It tells you whether the issue is your device or your network.
:::
```

## Example pull request

**Title:** Add Wi-Fi troubleshooting articles

**What changed:** Added three troubleshooting articles to `docs/` and linked them in the sidebar.

**Why:** Readers asked for self-service steps for the most common home network problems.

**How to review:** Run `npm start`, open the Wi-Fi section, and follow each procedure. Confirm that every step is accurate and that no links are broken.