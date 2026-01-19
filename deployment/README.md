# Kanban App Deployment

## Overview
This deployment script clones the kanban app from a git repository and sets it up on EC2 instances.

## Usage with Terraform

Update your compute module to use this script:

```hcl
user_data = base64encode(templatefile("${path.module}/../../kanban-app/deployment/user-data.sh", {
  GIT_REPO_URL = var.git_repo_url        # e.g., "https://github.com/youruser/kanban-app.git"
  GIT_BRANCH   = var.git_branch          # e.g., "main" or "production" (optional)
  DB_HOST      = split(":", var.db_endpoint)[0]
  DB_USER      = var.db_username
  DB_PASSWORD  = var.db_password
  DB_NAME      = var.db_name
}))
```

## Required Variables

Add to your `modules/compute/variables.tf`:

```hcl
variable "git_repo_url" {
  description = "Git repository URL for the kanban application"
  type        = string
}

variable "git_branch" {
  description = "Git branch to checkout (optional, defaults to repo default branch)"
  type        = string
  default     = ""
}
```

## Push kanban-app to Git

1. Initialize git in kanban-app folder (excluding deployment/):
   ```bash
   cd kanban-app
   git init
   git add package.json server.js public/
   git commit -m "Initial kanban app"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. Update Terraform variables with your repo URL

3. Run `terraform apply`

## Benefits
- Clean separation: app code in git, infrastructure in Terraform
- Easy updates: push to git, cycle EC2 instances
- Version control for application code
- Supports multiple environments via git branches
