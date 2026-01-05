
# Automate iOS Config Sync: `.env` to Xcode with GitHub PRs and Email Notifications

This workflow automatically detects changes to `.env.staging` files, compares them against iOS Xcode configuration files, creates GitHub Pull Requests to sync updated values, invalidates the Xcode build cache when required, and notifies your team via email.

It ensures configuration consistency across environments while eliminating manual sync errors.

---

## Quick Implementation Steps

1. Import the workflow JSON into your n8n instance
2. Configure credentials for:

   * GitHub
   * Email (SMTP)
3. Set up the webhook URL in your GitHub repository
4. Customize parameters in the **Set Configuration** node
5. Activate the workflow

---

## What It Does

This automation keeps iOS configuration files in sync with environment files by monitoring `.env.staging`:

* Detects changes to `.env.staging`
* Compares values with iOS config files (`Info.plist`, `.xcconfig`)
* Creates a new branch with synced updates
* Opens a GitHub Pull Request
* Triggers cache invalidation when required
* Sends detailed email notifications summarizing changes

---

## Who’s It For

* iOS engineering teams managing multiple environments
* DevOps engineers enforcing configuration consistency
* Mobile teams using `.env`-based workflows
* Teams following CI/CD best practices for iOS
* Projects suffering from environment configuration drift

---

## Requirements

* n8n (cloud or self-hosted)
* GitHub repository containing the iOS project
* GitHub access token with `repo` scope
* SMTP email credentials for notifications
* Environment file (`.env.staging` or similar)
* iOS configuration files (`Info.plist`, `.xcconfig`)

---

## How It Works

1. **GitHub Webhook Trigger**
   Listens for `push` events on the repository.

2. **Configuration Setup**
   Defines file paths, branches, and environment settings.

3. **File Change Detection**
   Checks whether `.env.staging` has changed.

4. **Config Diff Analysis**
   Compares environment variables with iOS config files.

5. **Branch Creation**
   Creates a new, uniquely named branch.

6. **Prepare File Updates**
   Generates updated config file content.

7. **Create Pull Request**
   Opens a PR with all synchronized changes.

8. **Invalidate Cache**
   Flags build cache invalidation when necessary.

9. **Email Notification**
   Sends a detailed summary to the configured recipients.

---

## How to Customize

* **Add more config files**
  Extend the `configFiles` array in the **Set Configuration** node.

* **Adjust cache invalidation logic**
  Modify `cacheInvalidationKeys` to trigger only on specific changes.

* **Customize PR details**
  Update the PR title, description, labels, or reviewers.

* **Personalize email notifications**
  Adjust subject lines, templates, or recipients.

* **Multi-environment support**
  Add support for `.env.production`, `.env.dev`, etc.

---

## Add-Ons

* Multi-environment syncing (`.env.dev`, `.env.prod`)
* Validation logic before syncing values
* Auto-merge PRs when checks pass
* Change history logging (database or dashboard)
* Approval workflow before PR creation

---

## Use Case Examples

1. **API Key Rotation** – Sync updated API keys safely across configs
2. **Environment Promotion** – Move staging changes into production
3. **Bundle Versioning** – Auto-update versions in `Info.plist`
4. **Feature Flag Management** – Sync new flags across environments
5. **Multi-Target Projects** – Apply changes to apps, extensions, and frameworks

---

## Troubleshooting Guide

| Issue                          | Possible Cause                  | Solution                                            |
| ------------------------------ | ------------------------------- | --------------------------------------------------- |
| Webhook not triggering         | Webhook misconfigured in GitHub | Verify webhook URL and delivery logs                |
| Changes not detected           | Incorrect `envFilePath`         | Validate path in **Set Configuration** node         |
| Branch creation fails          | Insufficient token permissions  | Ensure GitHub token has `repo` scope                |
| File update errors             | Invalid config file paths       | Verify paths in `configFiles` array                 |
| PR creation fails              | Target branch does not exist    | Confirm `targetBranch` value                        |
| Emails not sent                | SMTP misconfiguration           | Check credentials and recipient settings            |
| Cache invalidation not working | Missing or incorrect logic      | Update cache invalidation step for your CI/CD setup |

---

## Need Help?

If you need help setting up or extending this iOS configuration sync workflow — including CI/CD integration, environment validation, or multi-project support — the **n8n automation experts at WeblineIndia** can help tailor it to your development process.
