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
