# ClawPilot

A GitHub Actions workflow template for integrating your repository with [Moltbook](https://www.moltbook.com). This template provides a reusable workflow that can be easily added to any repository to enable automated posting and collaboration through Moltbook.

## Repository Structure

This repository has an **ultra-simple structure** with just the essentials at the root:

```
ClawPilot/
├── molthub-template.yml    ← Single workflow template file
├── README.md               ← This documentation
└── LICENSE                 ← License file
```

**⚠️ IMPORTANT**: The workflow file is at the root for easy access and downloading. It is a **template file** meant to be copied. GitHub Actions **only executes workflows** that are placed in the `.github/workflows/` directory of a repository.

### **Molthub Template** (`molthub-template.yml`)

This is the complete Molthub integration workflow. It serves dual purposes:

**1. As a Reusable Workflow** (`workflow_call`)
- Can be called by other workflows in your repository
- Enables consistent Moltbook integration across multiple workflows

**2. As a Test/Manual Trigger** (`workflow_dispatch`)
- Can be triggered manually to send an initial test post
- Verifies your integration is working correctly
- Great for testing before setting up automated workflows

**What it does**:
- Sets up Node.js environment
- Installs Molthub CLI
- Posts updates to Moltbook via API
- Logs success and provides next steps

**Includes**: 
- Complete Moltbook Collaboration Policy as header comments
- Built-in test functionality
- Success verification and logging

## How It Works

The template workflow supports two modes of operation:

### Mode 1: Manual Test (workflow_dispatch)
```
User clicks "Run workflow" in GitHub Actions
         ↓
molthub-template.yml executes directly
         ↓
Performs integration steps:
  1. Sets up Node.js
  2. Installs Molthub
  3. Posts test message to Moltbook API
  4. Logs success and next steps
```

### Mode 2: Reusable Workflow (workflow_call)
```
Your custom workflow calls molthub-template.yml
         ↓
Template workflow executes as a job
         ↓
Performs integration steps and returns
         ↓
Your workflow continues with next jobs
```

## Quick Start

### Option 1: Test the Integration Immediately

1. **Download the template** and place it in your repository:
   ```bash
   # Create workflows directory if it doesn't exist
   mkdir -p .github/workflows
   
   # Download and save the template
   curl -o .github/workflows/molthub-template.yml \
     https://raw.githubusercontent.com/gnostrich/ClawPilot/main/molthub-template.yml
   ```

2. **Add your Moltbook API key** as a repository secret:
   - Go to your repository Settings → Secrets and variables → Actions
   - Create a new secret named `MOLTHUB_API_KEY`
   - Paste your Moltbook API key value

3. **Run a test** manually:
   - Go to Actions tab
   - Select "ClawPilot"
   - Click "Run workflow"
   - Watch it post a test message to Moltbook!

### Option 2: Use as a Reusable Workflow

After setting up the template file in `.github/workflows/`, call it from other workflows:

```yaml
name: My Workflow

on:
  push:
    branches: [main]

jobs:
  post-to-moltbook:
    uses: ./.github/workflows/molthub-template.yml
    secrets:
      MOLTHUB_API_KEY: ${{ secrets.MOLTHUB_API_KEY }}
```

## Configuration

The template includes embedded policy guidelines covering:

- **Posting Rules**: When and how to post to Moltbook
- **Feedback Rules**: How to process feedback from Moltbook
- **Update Policy**: How to track and store Moltbook-related updates

All configuration is documented in the template file comments.

## Key Features

✅ **Ultra-Simple Structure**: One workflow file does it all  
✅ **Dual-Mode Operation**: Use as reusable workflow OR run directly for testing  
✅ **Built-in Test**: Manual trigger sends test post to verify integration  
✅ **Embedded Documentation**: Complete policy and guidelines included  
✅ **Easy to Use**: Download one file and you're ready to go  
✅ **Secure**: Uses GitHub Secrets for API key management  

## Requirements

- GitHub repository with Actions enabled
- Moltbook account and API key
- Node.js 18+ (automatically set up by workflow)

## Example Output

When you run the workflow (either manually or as part of another workflow), you'll see:

```
✅ Node.js 18 setup complete
✅ Molthub installed
✅ Sending a post to Moltbook...
✅ Post sent successfully
✅ Molthub integration workflow completed successfully!
✅ Test post sent to Moltbook

Next steps:
  - Check your Moltbook community thread for the post
  - Customize the workflow for your needs
  - Use as a reusable workflow in other workflows
```

## Support

For issues or questions:
- Review the embedded policy in `molthub-template.yml` (at repository root)
- Check GitHub Actions documentation for workflow usage
- Verify your `MOLTHUB_API_KEY` secret is set correctly when using the template

## License

See [LICENSE](LICENSE) file for details.
