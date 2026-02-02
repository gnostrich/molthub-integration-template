# Molthub Integration Workflow Fixes

## Issues Fixed

### 1. Missing Secrets Declaration in Reusable Workflow
**File:** `.github/workflows/molthub-template.yml`

**Problem:** The reusable workflow did not declare the `MOLTHUB_API_KEY` secret as an input, which prevented the test workflow from passing secrets to it.

**Solution:** Added the `secrets` section to the `workflow_call` trigger:
```yaml
on:
  workflow_call:
    secrets:
      MOLTHUB_API_KEY:
        required: true
        description: 'API key for Molthub authentication'
```

### 2. YAML Indentation Issues
**Files:** Both `.github/workflows/molthub-template.yml` and `.github/workflows/test-molthub.yml`

**Problem:** Steps were using 2-space indentation instead of the required 4-space indentation for GitHub Actions workflows.

**Solution:** Fixed all step indentation to use proper 4-space indentation (2 spaces per level).

## Configuration Verified

✅ **Reusable Workflow Reference:** Correctly uses `gnostrich/molthub-integration-template/.github/workflows/molthub-template.yml@main`

✅ **Secrets Passing:** Test workflow correctly passes `MOLTHUB_API_KEY` to the reusable workflow

✅ **YAML Syntax:** Both workflow files now have valid YAML syntax

✅ **API Call Configuration:** The curl command in the reusable workflow properly uses the API key from secrets

## Testing the Workflow

To test the fixed workflow:

1. Go to the GitHub repository's **Actions** tab
2. Select the "Test Molthub Workflow" from the workflows list
3. Click "Run workflow" button
4. The workflow will execute and should complete successfully (provided the `MOLTHUB_API_KEY` secret is set in the repository settings)

## Note on Secrets

The workflow requires the `MOLTHUB_API_KEY` secret to be configured in the repository settings:
- Navigate to Settings → Secrets and variables → Actions
- Add a repository secret named `MOLTHUB_API_KEY` with the appropriate value

If the secret is not set, the workflow will fail at the "Push Update to Moltbook" step.
