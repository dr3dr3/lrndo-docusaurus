---
sidebar_position: 1
tags:
  - Reference
---

# Variables / Configuration

## Developer Managed

- Environment agnostic
- Version control within code repository

### SOLN_GROUP

When a change to a repo happens that is part of a solution group, that change triggers deployment to STG and PRD environments for ALL related solutions (repos).

Example: The single front end can be comprised of a NextJS website and slides (bundled into the one solution). If a change happens to either, then a new deployment is required of both as a bundle.

- Repository variable
- Default value if omitted: `missing`

---

## Solution Architect Managed

### REPO_GITOPS

The GITOPS repo manages key configurations as code. Each micro-solution making up the overall solution need to have this variable set in their repository. Relevant configurations are used for administering the repositories, including setting the repository variables.

- Repository variable
- Default value if omitted: `missing`

### REPO_STAGE

To be changed in future. Purpose of this repository is for deployment to GitHub Pages (as the host for static sites). Current intentions were to also use the workflows in this repo to deploy elsewhere as well (i.e. Vercel, or for backend deployments for this environment).

- Repository variable
- Default value if omitted: `missing`

### REPO_PROD

Same as REPO_STAGE

---

## Platform Managed

### SITE_URL

Required if a custom domain is used. Format is like: `https://www.mydomain.com` (no trailing slash)

- Repository variable
- Default value if ommitted: `https://github-user-name.github.io/repository-name`

---

## Infra/Ops Managed

### DEPLOY_CI

Where to deploy for the CI environment

- Repository variable
- Default value if omitted: `GITHUB-PAGES`

### DEPLOY_BLUE

Where to deploy for the Production environment, being always "blue" in the green/blue deployment strategy

- Repository variable
- Default value if omitted: `GITHUB-PAGES`

### CHECK_LINKS

Used as toggle for checking links on post-deployed static sites using Linkinator

- Repository variable
- Default value if omitted: `false`
