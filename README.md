# SVG Unblocked Hosting

# (https://letrol21.github.io/svg-unblocked-hosting/)[https://letrol21.github.io/svg-unblocked-hosting/]

A client-side web application designed to automatically package, deploy, and host static HTML applications on GitHub via SVG embedding. The application utilizes public CDNs to serve the generated SVG assets, bypassing traditional static file restrictions.

---

## Features

* **Zero Backend:** Runs entirely in the browser using the GitHub REST API.
* **Automated Repository Creation:** Automatically authenticates, provisions a new repository, and commits required files.
* **Direct Token Integration:** Features a shortcut to generate a Personal Access Token with the exact required scopes.
* **Multi-CDN Provisioning:** Automatically generates and indexes ready-to-use distribution URLs from multiple providers including jsDelivr, esm.sh, Statically, and GitHack.
* **Built-in Clipboard Utilities:** Single-click copying for all generated distribution links.

---

## Technical Mechanism

The application works by wrapping an asymmetric loading script inside an SVG container using the `foreignObject` specification. 

1. **Storage:** The raw payload (`.html`) and the launcher (`.svg`) are stored in the same GitHub repository.
2. **Execution:** When the SVG is requested via a CDN, the embedded script executes a `fetch` request targeting the raw source file path:
   `https://raw.githubusercontent.com/{user}/{repo}/refs/heads/main/{filename}.html`
3. **Rendering:** The script programmatically initializes a clean browser context (`about:blank`) and streams the response text directly into the document object, executing the application without standard path resolution boundaries.

---

## How to Use

### 1. Prerequisites
You need a GitHub account and a Personal Access Token (PAT).
* The token requires the `repo` scope to create repositories and push commits.
* You can use the built-in "Generate Token" button to open the pre-configured creation page on GitHub.

### 2. Deployment Steps
1. Open `index.html` in any modern web browser.
2. Paste the raw source code of your web application into the HTML input area.
3. Define the internal filename (default is `index`).
4. Provide a unique name for the new GitHub repository.
5. Input your GitHub Personal Access Token.
6. Click **Create Repo & Deploy**.

### 3. Accessing Your Output
Once the status log confirms a successful deployment, the **Hosted CDN Links** panel will appear. You can copy any of the provided URLs to access or distribute your hosted application.

---

## Supported CDNs

The application pre-configures paths for the following content delivery networks:

* **jsDelivr:** `https://cdn.jsdelivr.net/gh/{user}/{repo}@main/clickopen.svg`
* **esm.sh:** `https://esm.sh/gh/{user}/{repo}@main/clickopen.svg?dev`
* **Statically:** `https://cdn.statically.io/gh/{user}/{repo}@main/clickopen.svg?v=0`
* **GitHack (Production):** `https://rawcdn.githack.com/{user}/{repo}/main/clickopen.svg`
* **GitHack (Development):** `https://raw.githack.com/{user}/{repo}/main/clickopen.svg?t=0`

---

## License

This project is intended for educational, testing, and development purposes. Ensure compliance with the terms of service of GitHub and the utilized CDN providers during deployment.
