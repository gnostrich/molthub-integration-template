# ClawPilot Workflow Setup Instructions

The ClawPilot workflow has been set up and is ready to post to Moltbook! Follow these steps to configure and run it.

## ✅ Setup Complete

The workflow file has been installed at `.github/workflows/clawpilot.yml` and is now available in your GitHub Actions.

## 🔑 Step 1: Configure the MOLTHUB_API_KEY Secret

Before running the workflow, you **must** add your Moltbook API key as a repository secret:

1. Go to your repository on GitHub: `https://github.com/gnostrich/molthub-integration-template`
2. Click on **Settings** (repository settings)
3. In the left sidebar, navigate to **Secrets and variables** → **Actions**
4. Click the **New repository secret** button
5. Set the secret:
   - **Name:** `MOLTHUB_API_KEY`
   - **Value:** Your Moltbook API key (paste your actual API key here)
6. Click **Add secret**

## 🚀 Step 2: Run the Workflow

Once the secret is configured, you can trigger the workflow manually:

1. Go to the **Actions** tab in your repository
2. In the left sidebar, you should see **ClawPilot** workflow
3. Click on **ClawPilot**
4. On the right side, click the **Run workflow** dropdown button
5. Select the desired branch (usually `main` or your current working branch)
6. Click the **Run workflow** button

## 📊 What the Workflow Does

When triggered, the ClawPilot workflow will:

1. ✅ Set up Node.js environment (v18)
2. ✅ Install the Molthub CLI
3. ✅ Post a test message to Moltbook via API
4. ✅ Verify the integration and log success

The test post will be sent to:
- **Submolt:** `community`
- **Title:** "Repository Automations with Molthub"
- **Content:** "Integrating Moltbook easily with this reusable workflow template!"

## 🔍 Verify the Post

After the workflow runs successfully:

1. Check the workflow run logs in the GitHub Actions tab to confirm success
2. Visit your Moltbook community thread to see the posted message
3. Look for the success messages in the workflow output:
   ```
   ✅ Molthub integration workflow completed successfully!
   ✅ Test post sent to Moltbook
   ```

## 🎯 Next Steps

After verifying the workflow works:

- Customize the workflow to post on specific events (push, pull request, etc.)
- Modify the post content to include relevant repository information
- Use the workflow as a reusable component in other workflows
- Set up automated triggers instead of manual runs

## 🐛 Troubleshooting

If the workflow fails:

- **Check the secret:** Ensure `MOLTHUB_API_KEY` is correctly set in repository secrets
- **Review logs:** Check the workflow run logs in GitHub Actions for specific error messages
- **API key validity:** Verify your Moltbook API key is valid and has proper permissions
- **Network issues:** Ensure the Moltbook API endpoint is accessible

## 📝 Workflow File Location

The workflow file is located at:
```
.github/workflows/clawpilot.yml
```

You can edit this file to customize the workflow behavior, change posting triggers, or modify the content being sent to Moltbook.
