# 🧭 Stage 1: Introduction to GitHub Apps

## 🔍 What is a GitHub App?

A **GitHub App** is a type of integration that:
- Acts as a **separate identity** (not tied to a user account),
- Can be installed on multiple repositories or organizations,
- Has **fine-grained permissions** (e.g., read-only access to issues),
- Communicates with GitHub via **API** and **webhooks**.

## 🆚 GitHub App vs OAuth App

| Feature     | GitHub App                        | OAuth App                      |
|-------------|-----------------------------------|--------------------------------|
| Identity    | Acts as an app                    | Acts as a user                 |
| Permissions | Granular, per repo/org            | Broad, user-level              |
| Installation| Can be installed on multiple repos/orgs | Tied to a single user     |
| Webhooks    | Built-in support                  | Must be implemented manually   |

## 🔐 How does authentication work?

1. The GitHub App generates a **JWT (JSON Web Token)** signed with its private key.
2. The JWT is used to request an **installation token** for a specific installation.
3. The installation token is used to make authenticated API requests to GitHub.

 **Documentation**:
   - [GitHub Docs: About GitHub Apps](https://docs.github.com/en/apps/overview)
   

## About using GitHub Apps

