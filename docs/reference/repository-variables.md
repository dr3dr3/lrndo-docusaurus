---
sidebar_position: 1
---

# Variables / Configuration

## Developer Managed

* Environment agnostic
* Version control within code repository

### SOLN_GROUP

When a change to a repo happens that is part of a solution group, that change triggers deployment to STG and PRD environments for all related solutions (repos).

Example: The single front end can be comprised of a NextJS website and slides (bundled into the one solution). If a change happens to either, then a new deployment is required of both as a bundle.

* Repository variable
* Default value if omitted: na

### DEPLOY_CI

### DEPLOY_BLUE

### CHECK_LINKS

### REPO_GITOPS

### REPO_STAGE

### REPO_PROD

---

## Platform Managed

### SITE_URL
