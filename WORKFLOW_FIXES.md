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

**Problem:** Steps were not properly indented according to YAML standards.

**Solution:** Fixed all step indentation to use proper 2 spaces per indentation level, which is the standard for YAML and GitHub Actions workflows.

### 3. Incorrect Workflow Reference Format
**File:** `.github/workflows/test-molthub.yml`

**Problem:** The workflow used full repository path format (`owner/repo/.github/workflows/file@ref`) for calling a reusable workflow in the same repository, which caused the error "invalid value workflow reference: no version specified".

**Solution:** Changed to relative path format (`./.github/workflows/molthub-template.yml`) which is required for same-repository reusable workflow calls.

## Configuration Verified

✅ **Reusable Workflow Reference:** Correctly uses `./.github/workflows/molthub-template.yml` (relative path for same-repository workflows)

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

If the secret is not set, the workflow will fail at the "Push Update to Molthub" step.
