# 🧠 Introduction to GitHub Apps

## 🚀 Overview
A **GitHub App** is a type of integration built specifically to interact with GitHub via its **API** and webhooks. Unlike traditional OAuth Apps that act on behalf of a user, **GitHub Apps act on behalf of themselves** and have **granular permissions**, making them more secure and scalable—especially for automation, bots, or CI/CD tools.

## 1. 👥 Installation
- A GitHub App is installed on an **organization** or **user account**.
- It can be granted access to **specific repositories**.
- Each installation gets a unique **installation ID**.

## 2. ⚖️ Permissions
- GitHub Apps request **fine-grained** access—e.g., read-only access to issues, or write access to pull requests.
- This is much safer than OAuth Apps, which get broad access to everything a user has.

## 3. 🔐 Authentication
GitHub Apps authenticate using:

- **JSON Web Tokens (JWT)** to identify themselves.
- They exchange this JWT for an **installation access token**, which lets them call GitHub APIs **on behalf of the installation**.

## 4. 📱 Webhooks
- GitHub Apps can subscribe to **webhook events** (like `push`, `pull_request`, `issues`).
- They react to changes in repositories (e.g., leave a comment when a PR is opened).

---

## 🔧 Technical Workflow

1. **App Registration**:
   - You create a GitHub App in your developer settings.
   - Define callback URLs, permissions, and webhook events.

2. **JWT Authentication**:
   - Your app generates a **JWT** (signed using its private key).
   - This is sent to GitHub to prove who the app is.

3. **Access Token Request**:
   - With the JWT, the app asks GitHub for an **installation access token**.
   - This token gives temporary, scoped access to a specific installation's resources.

4. **API Calls**:
   - Using the installation token, the app makes GitHub API requests to perform actions (e.g., open issues, comment on PRs, update files).

5. **Webhook Handling**:
   - GitHub sends webhooks to the app’s URL when events occur.
   - The app responds accordingly (e.g., triggering a CI build, assigning reviewers).

---

## 🤖 GitHub App vs OAuth App

| Feature                | GitHub App                             | OAuth App                         |
|------------------------|----------------------------------------|-----------------------------------|
| Authentication         | Acts as the app/installation           | Acts as the user                  |
| Permission Scope       | Fine-grained and repository-specific   | Broad user-level access           |
| Webhook Support        | Yes                                    | Limited                           |
| Ideal Use Case         | Bots, automation, integrations         | User login, delegated access      |
| Auth Method            | JWT + Access Token                     | OAuth 2.0 token                   |

---

## 🧠 Use Cases for GitHub Apps

- Auto-labeling PRs or issues.
- Code review bots.
- CI/CD pipeline triggers.
- Monitoring repo activity.
- Custom dashboards or tools integrated with GitHub.

---

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

# GitHub App vs GitHub Actions Comparison

## 👆 Key Differences

| Feature / Criteria        | **GitHub App**                                                 | **GitHub Actions**                                             |
|---------------------------|----------------------------------------------------------------|----------------------------------------------------------------|
| 🔧 **Purpose**            | Integration of external applications with GitHub (API + webhooks) | Automation of CI/CD processes (build, test, deploy)            |
| 🧠 **Acts as**            | External app with access to the GitHub API                     | Script or pipeline running directly on GitHub                  |
| 📤 **Triggered by**       | Webhooks or API requests                                       | Repository events (e.g., push, pull_request)                   |
| 🔐 **Permissions**        | Fine-grained (repo, issues, pull requests – per repository)     | Based on `GITHUB_TOKEN`, automatic within the repository       |
| 📁 **Installation**       | Requires installation on accounts/organizations                | Integrated directly within the repository                      |
| 📊 **Typical Use Cases**  | Bots, dashboards, external tools, API integrations             | Building, testing, linting, deploying applications             |
| 🛠️ **Development**        | Custom logic, usually in Node.js, Go, etc.                     | YAML workflow with ready-made or custom actions                |
| ⟳ **Can Call API?**      | Yes – full access via access token                             | Yes – usually via `actions/github-script` or curl              |

---

## 🔍 Example Difference

### GitHub App:
- You build a bot that automatically comments on pull requests.
- The bot runs outside of GitHub (e.g., on your own server) and responds to webhooks.
- It authenticates as an **app**, not a user.

### GitHub Actions:
- You want tests and deployment to run every time you push code.
- The workflow runs automatically on GitHub infrastructure.
- No external server needed.

---

## 🧠 When to Use Which?

| You Need...                                  | Use                |
|----------------------------------------------|--------------------|
| Automation for builds, tests, deployments     | **GitHub Actions** |
| Bots or API-based integrations from outside GitHub | **GitHub App**     |
| SaaS tools that interact with GitHub users    | **GitHub App**     |
| Reactions to repo changes without infrastructure | **GitHub Actions** |

## Summary

- Use **GitHub Apps** when you need to build **external services** that interact with GitHub via API and webhooks.
- Use **GitHub Actions** when you want to **automate internal workflows** like testing, building, or deploying code directly in your repository.




# Setting Up CircleCI as a GitHub App

This guide walks you through setting up CircleCI as a GitHub App and connecting it to your repositories for continuous integration and deployment.

---
# 🚀 Step-by-step: Using CircleCI as a GitHub App

CircleCI can be installed as a GitHub App to integrate CI/CD into your repositories. Here’s how to set it up and use it.

---

## ✅ Step 1: Install CircleCI GitHub App

1. Go to the **CircleCI GitHub App** page:  
   [https://github.com/apps/circleci](https://github.com/apps/circleci)

2. Click **"Set up a plan"** or **"Install it for free"**.

3. Choose the **GitHub organization** or **user account** where you want to install CircleCI.

4. Select the repositories to give CircleCI access to, or select all repositories.

5. Click **"Authorize"** to complete the installation.

---

## ✅ Step 2: Connect Your GitHub Repo to CircleCI

1. **Log in** to [https://circleci.com](https://circleci.com) using your **GitHub account**.

2. On the **CircleCI dashboard**, click **"Add Projects"**.

3. Find your installed repository and click **"Set Up Project"**.

4. CircleCI will detect your repo’s **language and framework** automatically.

---
# 🚀 Step-by-step: Using CircleCI as a GitHub App with Python

This guide shows you how to use CircleCI with a Python project, connected to GitHub.

---

## 📁 Project Structure

```
my-python-app/
├── .circleci/
│   └── config.yml
├── app.py
├── requirements.txt
└── test_app.py
```

---

## 🧠 Python Files Overview

### `app.py`
```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print("Add 1 + 2 =", add(1, 2))
```
**Explanation:**
- Defines a simple `add` function.
- When the script is run directly, it prints the result of `add(1, 2)`.

### `test_app.py`
```python
import unittest
from app import add

class TestApp(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(1, 2), 3)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)

if __name__ == "__main__":
    unittest.main()
```
**Explanation:**
- Uses Python’s built-in `unittest` to test the `add` function.
- Runs three test cases to verify the logic.

### `requirements.txt`
```
# No external dependencies for this example
```

---

## ⚙️ `.circleci/config.yml` Explained

```yaml
version: 2.1

jobs:
  test:
    docker:
      - image: cimg/python:3.10
    steps:
      - checkout
      - run:
          name: Install dependencies
          command: |
            python -m venv venv
            . venv/bin/activate
            pip install --upgrade pip
            pip install -r requirements.txt
      - run:
          name: Run tests
          command: |
            . venv/bin/activate
            python -m unittest discover

workflows:
  version: 2
  test_workflow:
    jobs:
      - test
```

### 🔍 Explanation:
- `version: 2.1` – defines config version.
- `jobs:` – defines a job named `test` that uses a Docker container.
- `docker:` – uses Python 3.10 container from CircleCI.
- `steps:` – what CircleCI does inside the container:
  - `checkout` – clones your GitHub repo.
  - Creates a virtual environment, installs pip + dependencies.
  - Runs all unit tests using `unittest discover`.
- `workflows:` – defines what jobs run and in which order. Here we run just the `test` job.

---

## 🚀 Connecting to CircleCI

1. Push the code to GitHub.
2. Go to [CircleCI](https://circleci.com/), sign in with GitHub.
3. Allow CircleCI GitHub App to access your repo.
4. CircleCI will auto-detect `.circleci/config.yml`.
5. On every push, CircleCI will run your tests!

---

## ✅ Done!

You now have:
- A simple Python app.
- Automated testing on every push using CircleCI.
- GitHub App integration for secure and easy setup.

You can extend this by adding linting, code formatting, or deployment.
