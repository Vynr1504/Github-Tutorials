# GitHub CLI Authentication Guide

## Overview
This guide walks you through the process of authenticating with GitHub using the GitHub CLI (gh) tool on Windows. This allows you to seamlessly work with GitHub repositories from your command line.

## Prerequisites
- Windows OS with PowerShell
- Internet connection
- GitHub account (in this example: `Vynr1504`)

## Step-by-Step Process

### 1. Configure Git User Information

First, set up your global Git configuration with your GitHub username:

```powershell
git config --global user.name "Vynr1504"
```

Verify or set your email address:

```powershell
# Check current email configuration
git config --global user.email

# Set email if not configured
git config --global user.email "your-email@example.com"
```

### 2. Install GitHub CLI

Check if GitHub CLI is already installed:

```powershell
gh --version
```

If not installed, use Windows Package Manager (winget) to install:

```powershell
winget install --id GitHub.cli
```

### 3. Refresh Environment Variables

After installation, refresh the PATH environment variable to use the newly installed GitHub CLI:

```powershell
$env:PATH = [System.Environment]::GetEnvironmentVariable("PATH","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("PATH","User")
```

Verify installation:

```powershell
gh --version
```

Expected output:
```
gh version 2.78.0 (2025-08-21)
https://github.com/cli/cli/releases/tag/v2.78.0
```

### 4. Authenticate with GitHub

Start the authentication process:

```powershell
gh auth login
```

You'll be prompted with several options:

1. **Where do you use GitHub?**
   - Select: `GitHub.com`

2. **What is your preferred protocol for Git operations?**
   - Select: `HTTPS` (recommended for most users)

3. **Authenticate Git with your GitHub credentials?**
   - Select: `Yes`

4. **How would you like to authenticate GitHub CLI?**
   - Select: `Login with a web browser`

### 5. Complete Browser Authentication

1. The CLI will display a one-time code (e.g., `3CB9-95D6`)
2. Press Enter to open the GitHub device login page in your browser
3. Enter the provided code on the GitHub website
4. Complete the authentication in your browser
5. Return to the terminal

Expected success output:
```
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as Vynr1504
```

### 6. Verify Authentication

Check your authentication status:

```powershell
gh auth status
```

Expected output:
```
github.com
  ✓ Logged in to github.com account Vynr1504 (keyring)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'
```

## Available Commands After Authentication

Once authenticated, you can use various GitHub CLI commands:

### Repository Operations
```powershell
# List your repositories
gh repo list

# Clone a repository
gh repo clone username/repo-name

# Create a new repository
gh repo create repo-name

# Fork a repository
gh repo fork owner/repo-name
```

### Issue Management
```powershell
# List issues
gh issue list

# Create an issue
gh issue create --title "Issue title" --body "Issue description"

# View issue details
gh issue view 123
```

### Pull Request Operations
```powershell
# List pull requests
gh pr list

# Create a pull request
gh pr create --title "PR title" --body "PR description"

# Review a pull request
gh pr review 123
```

### Workflow Management
```powershell
# List workflows
gh workflow list

# Run a workflow
gh workflow run workflow-name

# View workflow runs
gh run list
```

## Troubleshooting

### Common Issues and Solutions

1. **GitHub CLI not recognized after installation**
   - Restart your terminal or refresh environment variables
   - Use the PATH refresh command mentioned in step 3

2. **Authentication fails**
   - Ensure you're using the correct one-time code
   - Check your internet connection
   - Try clearing browser cookies and retry

3. **Token permissions issues**
   - Re-authenticate with `gh auth login` to refresh token scopes
   - Check token scopes with `gh auth status`

### Re-authentication

If you need to re-authenticate or switch accounts:

```powershell
# Logout current account
gh auth logout

# Login with new account
gh auth login
```

## Security Notes

- Your authentication token is stored securely in your system's keyring
- Tokens have specific scopes (`gist`, `read:org`, `repo`, `workflow`)
- Never share your authentication tokens
- Regularly review and rotate your tokens for security

## Configuration Files

GitHub CLI stores configuration in:
- Windows: `%APPDATA%\GitHub CLI\`
- Config file: `config.yml`
- Hosts file: `hosts.yml`

## Additional Resources

- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub CLI Repository](https://github.com/cli/cli)
- [GitHub Token Management](https://github.com/settings/tokens)

---

**Created**: September 3, 2025  
**Author**: GitHub Copilot  
**Last Updated**: September 3, 2025
