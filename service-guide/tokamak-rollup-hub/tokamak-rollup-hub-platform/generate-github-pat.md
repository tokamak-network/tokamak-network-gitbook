---
description: How to generate a GitHub Personal Access Token (PAT) required for registering rollup metadata on Tokamak Rollup Hub.
---

# Generate a GitHub Personal Access Token (PAT)

A GitHub PAT (Personal Access Token) is required to fork, commit, push changes, and submit a pull request for metadata registration. Follow the steps below to generate one.

1. Log in to GitHub and go to [Developer Settings](https://github.com/settings/developers).

2. Under the **Personal Access Tokens** section, select the **Tokens (classic)** tab and click **Generate new token**. In the dropdown, select **Generate new token (classic)**.

3. Set the required scopes: enable **`repo`** and **`workflow`**, and add any additional scopes as needed. (Check the `repo` scope checkbox to grant full repository access, and check `workflow` to allow triggering GitHub Actions.)

4. Click **Generate token**, then copy the token immediately — it will not be shown again.

{% hint style="warning" %}
Store your token securely. GitHub will only display the token once. If you lose it, you must generate a new one.
{% endhint %}
