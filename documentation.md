# 🧠 Introduction to GitHub Apps

## What Are GitHub Apps?

GitHub Apps are the official way to build integrations with GitHub. They are applications that:

- Operate as **independent identities** (not tied to a user account)
- Have **fine-grained permissions** (e.g., read-only access to issues)
- Can be **installed on specific repositories or organizations**
- Communicate with GitHub via **API** and **webhooks**

---

## 🔄 GitHub App vs OAuth App

| Feature         | GitHub App                          | OAuth App                          |
|----------------|--------------------------------------|------------------------------------|
| Identity        | Acts as an app                      | Acts as a user                     |
| Permissions     | Granular, per repo/org              | Broad, user-level                  |
| Installation    | On repositories or organizations    | On user accounts                   |
| Webhooks        | Built-in support                    | Must be implemented manually       |
| Authentication  | JWT + installation token            | OAuth token                        |

**In short**: GitHub Apps are more secure, flexible, and better suited for external integrations.

---

## ⚙️ How Does a GitHub App Work?

1. The app generates a **JWT** signed with its private key.
2. The JWT is exchanged for an **installation token** for a specific installation.
3. The installation token is used to make authenticated API calls to GitHub.
4. GitHub sends **webhooks** to the app when events occur (e.g., push, PR).
5. The app can respond by taking actions like adding comments, labels, or triggering external processes.

---

## 🧰 Typical Use Cases for GitHub Apps

- **Bots**: e.g., automatically labeling issues, closing stale tickets
- **External integrations**: e.g., syncing with Jira, Slack, or CI/CD tools
- **Secure API access**: apps can be scoped to specific repos with limited permissions
- **Process automation**: e.g., reacting to pull requests, pushes, or comments

---

## 🧪 Example Use Case

> A GitHub App listens for the `pull_request` webhook. When a PR is opened, it checks the title and automatically adds a `needs-review` label.


# GitHub Apps vs GitHub Actions

| Feature           | GitHub Apps                                                                 | GitHub Actions                                                             |
|------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Purpose**       | Build external integrations with GitHub (e.g., bots, services)              | Automate workflows like CI/CD inside a GitHub repository                   |
| **Execution**     | Runs externally (e.g., on your server or cloud platform)                    | Runs inside GitHub-hosted runners                                          |
| **Authentication**| Uses JWT + installation tokens                                              | Uses `GITHUB_TOKEN` provided by GitHub                                     |
| **Installation**  | Installed on repos/orgs with specific permissions                           | Defined in `.github/workflows/*.yml` in the repo                           |
| **Event Handling**| Listens to GitHub webhooks (e.g., `issues`, `pull_request`)                 | Reacts to GitHub Actions events (e.g., `push`, `pull_request`)            |
| **Use Cases**     | Bots, integrations with external systems (Slack, Jira, CI/CD)               | Build, test, deploy code; automate repo-specific tasks                     |
| **Security**      | Fine-grained, per-repo/org permissions                                       | Scoped to the repository and workflow context                              |
| **Flexibility**   | Highly customizable, reusable across multiple repos/orgs                    | Tightly coupled to the repository it lives in                              |

## Summary

- Use **GitHub Apps** when you need to build **external services** that interact with GitHub via API and webhooks.
- Use **GitHub Actions** when you want to **automate internal workflows** like testing, building, or deploying code directly in your repository.
