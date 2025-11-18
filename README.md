# GitHub Stats

![Metrics](github-metrics.svg)

---

## GitHub Metrics Workflow Documentation

This repository includes an automated GitHub metrics workflow that generates and updates your GitHub statistics visualization.

### What It Does

The workflow automatically generates a comprehensive SVG image (`github-metrics.svg`) containing:
- **Contribution Calendar**: ISO calendar showing your contributions over the last 6 months
- **Language Statistics**: Most used programming languages across your repositories
- **Lines of Code**: Statistics about your code contributions
- **Activity Metrics**: Repository activity, community engagement, and metadata
- **Starred Repositories**: Your most recently starred repositories (up to 4)

### Setup Requirements

#### 1. Configure the METRICS_TOKEN Secret

The workflow requires a GitHub Personal Access Token (PAT) to access your GitHub statistics:

1. **Create a Personal Access Token**:
   - Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Give it a descriptive name (e.g., "GitHub Metrics")
   - Select scopes:
     - `public_repo` (for public repository stats)
     - `repo` (if you want to include private repository stats)
   - Click "Generate token" and copy the token

2. **Add the Token as a Repository Secret**:
   - Go to your repository: Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `METRICS_TOKEN`
   - Value: Paste your Personal Access Token
   - Click "Add secret"

### How the Workflow Runs

The workflow is configured to run automatically in three ways:

1. **Daily Schedule**: Runs automatically every day at midnight (UTC)
2. **On Push to Main**: Runs when code is pushed to `main` or `master` branches
3. **Manual Trigger**: Can be triggered manually from the Actions tab

### Running the Workflow Manually

1. Go to the **Actions** tab in your repository
2. Select **GitHub Metrics** from the workflow list
3. Click **Run workflow** dropdown
4. Click the green **Run workflow** button

### Workflow Configuration

The workflow is defined in `.github/workflows/blank.yml` and uses the official [lowlighter/metrics](https://github.com/lowlighter/metrics) action with the following configuration:

- **Template**: Classic layout
- **Base sections**: Header, activity, community, repositories, metadata
- **Timezone**: America/New_York (adjust as needed)
- **Plugins enabled**:
  - ISO Calendar (half-year duration)
  - Languages (top 8 languages)
  - Lines of code statistics
  - Starred repositories (4 most recent)

### Customization

To customize what metrics are displayed, edit `.github/workflows/blank.yml` and modify the plugin settings. See the [lowlighter/metrics documentation](https://github.com/lowlighter/metrics) for all available options.

### Troubleshooting

**Workflow not running:**
- Ensure `METRICS_TOKEN` secret is properly configured
- Check that the token has the required scopes
- Verify the workflow is enabled in Settings → Actions

**SVG not updating:**
- Check the Actions tab for workflow run status and error messages
- Ensure the workflow has `contents: write` permissions (already configured)
- Verify the token hasn't expired

**Metrics not displaying:**
- Check that `github-metrics.svg` exists in the repository root
- Ensure the README is viewing the correct branch (usually `main`)
- The SVG may take a few minutes to generate on first run

### Merging Changes

**Important**: The workflow only runs on the `main` or `master` branches. If you make changes on a feature branch:

1. Create a pull request to merge your changes to `main`
2. Merge the pull request
3. The workflow will automatically run on the `main` branch
4. The updated `github-metrics.svg` will be committed to the repository

---

For more information about the metrics action, visit: https://github.com/lowlighter/metrics
