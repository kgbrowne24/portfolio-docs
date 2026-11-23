---
title: "Sample 4: Git Basics for Documentation Writers"
sidebar_position: 4
description: A 45-minute training module with objectives, agenda, hands-on exercise, job aid, and knowledge check.
---


## About This Sample

**Objective:** Demonstrate how to develop task-oriented technical training that helps beginners learn foundational Git concepts and workflows.

**Approach:** Designed an introductory training module that combines plain-language explanations, practical command examples, and hands-on exercises. Organized the content progressively, introducing core concepts before asking learners to apply them.

**Key documentation decisions:**
- Used accessible language to explain unfamiliar technical concepts without oversimplifying them.
- Sequenced the material from foundational concepts to practical Git workflows.
- Included command-line examples to reinforce learning through application.
- Structured the training around tasks learners are likely to perform in a real development environment.
- Incorporated hands-on practice to help learners build confidence using Git.

**Skills demonstrated:** Technical training, instructional design, developer education, task-based documentation, and technical communication.


**Audience:** Technical writers new to docs-as-code workflows <br />
**Length:** 45 minutes, instructor-led or self-guided <br />
**Prerequisites:** Git installed, a GitHub account, and a text editor

## Learning objectives

By the end of this module, learners will be able to:

- Explain what version control is and why docs teams use it
- Clone a repository and create a branch
- Edit a Markdown file, then commit and push the change
- Open a pull request for review

## Agenda

| Time | Activity |
| --- | --- |
| 0–5 min | Introduction: why docs teams use Git |
| 5–15 min | Demo: clone, branch, edit, commit |
| 15–30 min | Hands-on exercise: fix a typo in a practice repo |
| 30–40 min | Pull requests and review |
| 40–45 min | Knowledge check and questions |

## Hands-on exercise

Fork the practice repository, clone it, and create a branch named after yourself. Fix the typo in `README.md`, commit the change with a clear message, push the branch, and open a pull request.

## Job aid: Git quick reference

| I want to… | Command |
| --- | --- |
| Copy a repository to my computer | `git clone <url>` |
| Create and switch to a new branch | `git switch -c <branch-name>` |
| See which files I've changed | `git status` |
| Stage a file for commit | `git add <file>` |
| Save my staged changes | `git commit -m 'Describe the change'` |
| Send my branch to GitHub | `git push -u origin <branch-name>` |
| Get the latest changes | `git pull` |

**Good commit messages** are short and say what changed and why. For example: *Fix broken link in setup guide*.

## Knowledge check

1. What does a branch let you do?
2. Which command shows which files you've changed?
3. What is a pull request for?
4. Why is a clear commit message useful?
5. After you run `git commit`, is your change on GitHub yet?

**Answers**

1. Work on changes without affecting the main version of the files.
2. `git status`
3. Asking teammates to review your changes before they're merged.
4. It helps reviewers and future you understand what changed and why.
5. No. You need to run `git push` to send it to GitHub.