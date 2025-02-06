# Developer Guide

## <a name="installation"></a>Development Environment Setup

### Required Software

| Software   | URL                                                                    |
|------------|------------------------------------------------------------------------|
| git        | https://git-scm.com/downloads                                          |
| Python     | https://www.python.org/downloads/release/python-3131/                  |
| Terraform  | https://www.terraform.io/downloads.html                                |
| pre-commit | https://pre-commit.com/#install                                        |
| trivy      | https://verifa.io/blog/how-to-secure-terraform-trivy/#installing-trivy |

### Repository Setup
* Clone the Repository
  ```shell
  # Clone using SSH
  git clone git@github.com:go-gsd/demo.git

  # Navigate to project directory
  cd demo
  ```

### Development Workflow

This repository uses [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow). The core idea
behind Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the `main` branch. This
encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase. It also means the
main branch will never contain broken code, which is a huge advantage for continuous integration environments.

1. **Create a Feature Branch.** Replace `your-feature-name` with a descriptive name for your feature.
  ```shell
  git checkout -b feature/your-feature-name
  ```

2. **Make Changes.** Edit, add, or remove files related to your feature.*

3. **Run Code Quality Checks.** This will execute code quality checks configured in the `pre-commit-config.yaml` file.
  ```shell
  pre-commit run --all-files
  ```
4. **Commit Changes.** Commit your changes regularly.
  ```shell
  # Stage all changes
  git add -A 
  
  # Commit with a clear, descriptive message
  git commit -m "My clear, descriptive message"
  ```

5. **Push and Create Pull Request.**
  ```shell
  # Push your feature branch to remote
  git push origin feature/your-feature-name
  ```
- Navigate to GitHub and create a pull request from your feature branch (`feature/your-feature-name`) to the main branch (`main`).
- Code owners specified in the [CODEOWNERS](CODEOWNERS) file are automatically requested to review pull requests.
- Ensure all code quality checks pass.

6. **Post-Merge Cleanup.**
  ```shell
  # Delete local feature branch after successful merge
  git checkout main
  git pull
  git branch -d feature/your-feature-name
  
  # Delete remote feature branch
  git push origin --delete feature/your-feature-name
  ```

### Best Practices
- Always pull the latest main before creating a new feature branch.
- Keep feature branches small and focused.
- Write clear, atomic commits.
- Communicate with team during collaborative development.
- Ensure pre-commit checks pass before pushing.
