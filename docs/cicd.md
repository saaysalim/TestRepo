# CI/CD Pipeline Documentation

## Overview

This project uses **GitHub Actions** to automate building, testing, and deploying the application. The CI/CD pipeline runs automatically on every push and pull request.

## Workflow Files

### Main Workflow: `.github/workflows/ci-cd.yml`

This is the primary workflow that handles:
- **Code Quality Checks**: ESLint, TypeScript compilation
- **Testing**: Jest test suite with coverage
- **Building**: Production build verification
- **Deployment**: Automatic deployment on main branch

## Workflow Triggers

| Trigger | Action |
|---------|--------|
| `push` to `main` | Full pipeline runs → Deploy to production |
| `push` to `develop` | Full pipeline runs → Deploy to staging |
| `pull_request` | Full pipeline runs → Check status |
| `pull_request_review` | Deployment check on approval |

## Pipeline Stages

### 1. Install Dependencies
```
Checkout code → Install npm packages → Cache dependencies
```

### 2. Code Quality
```
TypeScript Check → ESLint → Code Format Check
```

### 3. Test
```
Run Unit Tests → Run Integration Tests → Generate Coverage Report
```

### 4. Build
```
Build Production Bundle → Verify Bundle Size → Artifact Upload
```

### 5. Deploy (Main Branch Only)
```
Build Docker Image → Push to Registry → Deploy to Production
```

## Environment Variables

Required environment variables for deployment:

| Variable | Description | Required |
|----------|-------------|----------|
| `VITE_API_URL` | Backend API URL | Yes |
| `VITE_ENV` | Environment (dev/staging/prod) | Yes |
| `DOCKER_USERNAME` | Docker registry username | Yes (for deploy) |
| `DOCKER_PASSWORD` | Docker registry password | Yes (for deploy) |
| `DEPLOY_TOKEN` | Deployment authentication token | Yes (for deploy) |

## Setting Up Secrets

Go to **Settings → Secrets and variables → Actions** and add:

```bash
# Production Deployment
DOCKER_USERNAME = your_docker_username
DOCKER_PASSWORD = your_docker_password
DEPLOY_TOKEN = your_deployment_token
PROD_DATABASE_URL = your_prod_database_url
```

## Pipeline Status

View pipeline status at: https://github.com/saaysalim/TestRepo/actions

### Understanding Status Indicators
- 🟢 **Success**: All checks passed
- 🔴 **Failed**: One or more checks failed
- 🟡 **In Progress**: Pipeline is running
- ⚪ **Skipped**: Stage was skipped

## Failure Handling

### Common Failures

#### 1. Test Failures
```
❌ Issue: Tests failed
✅ Solution: 
- Check test output in GitHub Actions
- Run tests locally: npm test
- Fix failing tests and push again
```

#### 2. Build Failures
```
❌ Issue: Build failed
✅ Solution:
- Check build logs in GitHub Actions
- Run locally: npm run build
- Fix issues and re-push
```

#### 3. Linting Errors
```
❌ Issue: ESLint errors
✅ Solution:
- Run: npm run lint
- Fix issues or run: npm run format
- Commit and push
```

## Best Practices

### 1. Keep Pipeline Fast
- Optimize test suite
- Cache dependencies
- Minimize build steps

### 2. Early Failure Detection
- Run tests locally before pushing
- Use pre-commit hooks
- Check linting locally

### 3. Clear Commit Messages
```
feat: Add new feature
fix: Fix bug in component
docs: Update documentation
test: Add tests
ci: Update CI/CD pipeline
```

### 4. Use Feature Branches
```bash
git checkout -b feature/my-feature
# Make changes
git push origin feature/my-feature
# Create PR
```

## Skipping CI

To skip the CI pipeline for a commit:

```bash
git commit -m "docs: Update README [skip ci]"
```

## Monitoring & Alerts

### GitHub Notifications
- Branch protection rules prevent merging if CI fails
- Failed workflows send notifications to watchers

### Manual Workflow Trigger

You can manually trigger workflows from **Actions → Select Workflow → Run workflow**

## Performance Metrics

The workflow collects:
- Build time
- Test duration
- Code coverage percentage
- Bundle size

View metrics in the **Summary** tab of each workflow run.

## Troubleshooting

### Workflow Won't Run
1. Check branch protection rules
2. Verify repository has Actions enabled
3. Check if `.github/workflows/` folder exists
4. Ensure YAML syntax is correct

### Cache Not Working
```bash
# Clear workflow cache
gh actions-cache delete <cache_key> --branch main
```

### Secrets Not Available
1. Go to Settings → Secrets
2. Verify secret is spelled correctly
3. Secrets are case-sensitive
4. Secrets available in job context, not in scripts

## Related Documentation

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Getting Started Guide](./getting-started.md)
- [Contributing Guidelines](../CONTRIBUTING.md)

## Support

For CI/CD issues:
- 🐛 [Report Issue](https://github.com/saaysalim/TestRepo/issues)
- 💬 [Ask Question](https://github.com/saaysalim/TestRepo/discussions)
- 📧 Contact maintainers

---

**Last Updated**: November 16, 2026
