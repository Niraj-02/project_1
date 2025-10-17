# LLM Code Deployment

This project demonstrates an **automated application lifecycle** using **LLM-assisted code generation, deployment, and iterative updates**. Students build an app based on a brief, deploy it to GitHub Pages, and interact with an evaluation API to validate functionality. Instructors evaluate both static and dynamic behavior, then send follow-up requests to refine the project.

---

## Project Overview

The goal of this project is to simulate a full development workflow:
1. **Build**: Generate and deploy a minimal app from a JSON brief.
2. **Evaluate**: Run automated checks including static analysis, Playwright-based dynamic tests, and LLM-assisted code evaluations.
3. **Revise**: Modify the app based on instructor feedback and redeploy.

This workflow emphasizes automation, LLM-assisted development, GitHub integration, and evaluation pipelines.

---

## Features

- **JSON API Endpoint**: Accepts requests with app briefs, secrets, and attachments (Base64-encoded files).
- **LLM-Assisted Code Generation**: Automatically generates minimal HTML/CSS/JS apps.
- **GitHub Integration**: Creates a public repository, pushes code, adds MIT License, and enables GitHub Pages.
- **Dynamic Evaluation**: Notifies an instructor-provided evaluation API with repo URL, commit SHA, and Pages URL.
- **Iterative Development**: Supports multiple rounds of requests to refine and update the app based on evaluation feedback.
- **Attachment Handling**: Supports embedded images and other files as Base64 data URIs.
- **Automated Notifications**: Sends HTTP POST to the evaluation URL within 10 minutes of request handling.

---

## Request Structure

Incoming requests are JSON-formatted as follows:

```json
{
  "email": "student@example.com",
  "secret": "...",
  "task": "captcha-solver-...",
  "round": 1,
  "nonce": "ab12-...",
  "brief": "Create a captcha solver that handles ?url=https://.../image.png. Default to attached sample.",
  "checks": [
    "Repo has MIT license",
    "README.md is professional",
    "Page displays captcha URL passed at ?url=...",
    "Page displays solved captcha text within 15 seconds"
  ],
  "evaluation_url": "https://example.com/notify",
  "attachments": [
    { "name": "sample.png", "url": "data:image/png;base64,iVBORw..." }
  ]
}
