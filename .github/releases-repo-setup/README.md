# Releases Repo Setup

These files need to be placed in the **public** `conical-io/joomla-plugins-releases` repo.

## Steps to set up the releases repo

1. Create a new **public** repo: `conical-io/joomla-plugins-releases`

2. Copy `deploy-pages.yml` to `.github/workflows/deploy-pages.yml` in that repo

3. Create an `updates/` directory with empty stubs (or let the first release create them)

4. In the releases repo: Settings → Pages → Source → select **"GitHub Actions"**

5. In the **private** repo (`conical-io/joomla-plugins`):
   - Go to Settings → Secrets and variables → Actions
   - Create a secret named `RELEASES_REPO_TOKEN`
   - Value: a GitHub Personal Access Token (classic) with `repo` and `workflow` scopes
     - The token must belong to a user with push access to `conical-io/joomla-plugins-releases`

## How it works

When a tag is pushed to the private repo (e.g., `wwcc_sef_api-v1.1.0`), the workflow:
1. Builds the installable ZIP in the private repo
2. Pushes the update XML and creates a GitHub Release in this public repo
3. Triggers the Pages deploy workflow here to update the hosted update feed

Joomla sites fetch the update XML from:
`https://conical-io.github.io/joomla-plugins-releases/updates/{element}.xml`
