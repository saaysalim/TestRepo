# Contributing to TestRepo

Thank you for your interest in contributing to TestRepo! We appreciate all contributions.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Development Setup](#development-setup)
- [Submitting Changes](#submitting-changes)
- [Commit Messages](#commit-messages)
- [Pull Request Process](#pull-request-process)
- [Reporting Issues](#reporting-issues)

## Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

## How to Contribute

### Reporting Bugs
- **Check existing issues** before creating a new one
- **Be descriptive** - include steps to reproduce, expected vs actual behavior
- **Attach logs** - include error messages and stack traces
- **Specify environment** - OS, Node version, browser if applicable

### Suggesting Enhancements
- **Search existing issues** first
- **Be clear about the use case** - explain the problem you're trying to solve
- **Provide examples** - show how it would work
- **Consider alternatives** - what other solutions exist?

### Writing Documentation
- Fix typos and unclear explanations
- Add examples to existing docs
- Create new guides for common tasks
- Update outdated information

### Writing Code
- Fix bugs
- Implement features from open issues
- Improve performance
- Add tests

## Development Setup

### Prerequisites
- **Node.js** 16+ ([Download](https://nodejs.org/))
- **Git** ([Download](https://git-scm.com/))
- **npm** (comes with Node.js)

### Setup Steps

```bash
# 1. Fork the repository
#    Click "Fork" on GitHub

# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/TestRepo.git
cd TestRepo

# 3. Add upstream remote
git remote add upstream https://github.com/saaysalim/TestRepo.git

# 4. Create feature branch
git checkout -b feature/my-feature

# 5. Install dependencies
npm install

# 6. Start development server
npm run dev
```

## Submitting Changes

### Create a Feature Branch

```bash
# Always create a new branch for your work
git checkout -b feature/descriptive-name

# Branch naming conventions:
# - feature/add-new-component
# - fix/button-styling-issue
# - docs/update-readme
# - test/add-unit-tests
```

### Make Your Changes

```bash
# Edit files
# Test your changes locally

# Check code quality
npm run lint
npm run format

# Run tests
npm test
```

### Keep Your Branch Updated

```bash
# Fetch latest changes
git fetch upstream

# Rebase on main
git rebase upstream/main
```

## Commit Messages

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- **feat**: New feature
- **fix**: Bug fix
- **docs**: Documentation
- **style**: Code style (formatting, missing semicolons)
- **refactor**: Code refactoring
- **perf**: Performance improvement
- **test**: Test additions/updates
- **ci**: CI/CD configuration
- **chore**: Build, dependencies, tools

### Examples

```bash
# Good commit messages
git commit -m "feat(auth): add two-factor authentication"
git commit -m "fix(login): resolve password reset issue"
git commit -m "docs(readme): update installation steps"
git commit -m "test(api): add endpoint validation tests"
```

### Guidelines

- Use imperative mood ("add feature" not "added feature")
- Keep subject line under 50 characters
- Reference issues: "Fixes #123" or "Closes #456"
- Explain what and why, not how

## Pull Request Process

### Before Creating PR

1. **Update your branch**
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Run tests**
   ```bash
   npm test
   npm run lint
   ```

3. **Build the project**
   ```bash
   npm run build
   ```

### Create Pull Request

1. **Push to your fork**
   ```bash
   git push origin feature/my-feature
   ```

2. **Create PR on GitHub**
   - Go to [TestRepo](https://github.com/saaysalim/TestRepo)
   - Click "New Pull Request"
   - Select your branch
   - Fill in the PR template

### PR Template

```markdown
## Description
Brief description of what this PR does.

## Related Issues
Closes #123

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Changes Made
- Change 1
- Change 2

## Testing
How to test these changes:
1. Step 1
2. Step 2

## Checklist
- [ ] Tests pass locally
- [ ] No new linting errors
- [ ] Documentation updated
- [ ] Commits are descriptive
```

### PR Reviews

- Address feedback promptly
- Ask questions if unclear
- Request re-review after changes
- Keep discussion respectful and constructive

## Reporting Issues

### Use GitHub Issues

[Open an Issue](https://github.com/saaysalim/TestRepo/issues)

### Include

- **Descriptive title**
- **Clear description**
- **Steps to reproduce** (for bugs)
- **Expected behavior**
- **Actual behavior**
- **Screenshots** (if UI-related)
- **Environment info**:
  ```
  - OS: Windows 10
  - Node: v18.0.0
  - npm: 8.0.0
  ```

## Code Quality Standards

### TypeScript
```typescript
// Good: Use type annotations
function getUser(id: string): Promise<User> {
  return fetch(`/api/users/${id}`).then(r => r.json());
}

// Bad: Missing types
function getUser(id) {
  return fetch(`/api/users/${id}`).then(r => r.json());
}
```

### Testing
```typescript
// Every component should have tests
describe('Button Component', () => {
  it('should render with text', () => {
    const { getByText } = render(<Button>Click me</Button>);
    expect(getByText('Click me')).toBeInTheDocument();
  });
});
```

### Linting
```bash
# Run linter
npm run lint

# Auto-fix issues
npm run format
```

## Questions?

- 💬 [GitHub Discussions](https://github.com/saaysalim/TestRepo/discussions)
- 📧 Email: support@example.com
- 📖 [Documentation](./docs)

## Recognition

Contributors will be:
- Added to CONTRIBUTORS.md
- Thanked in release notes
- Featured in GitHub insights

---

**Thank you for contributing! 🎉**

