# Contributing to Live Server++

Thank you for your interest in contributing to Live Server++! This document provides guidelines and instructions for contributing.

## Table of Contents
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Making Changes](#making-changes)
- [Testing](#testing)
- [Submitting Changes](#submitting-changes)
- [Git Workflow](#git-workflow)
- [Code Style](#code-style)

---

## Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/vscode-live-server-plus-plus.git
   cd vscode-live-server-plus-plus
   ```

3. **Add upstream remote:**
   ```bash
   git remote add upstream https://github.com/Helhum-coder/vscode-live-server-plus-plus.git
   ```

---

## Development Setup

### Prerequisites
- Node.js (v10 or higher)
- npm (v6 or higher)
- Visual Studio Code (v1.33.0 or higher)
- Git

### Installation

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Compile the project:**
   ```bash
   npm run compile
   ```

3. **Watch for changes during development:**
   ```bash
   npm run watch
   ```

### Running the Extension

1. Open the project in VS Code
2. Press `F5` to open a new Extension Development Host window
3. Test the extension in the development window

---

## Making Changes

### Branch Naming
Create a descriptive branch for your changes:
```bash
git checkout -b feature/add-new-setting
git checkout -b fix/port-conflict-issue
git checkout -b docs/improve-readme
```

### Commit Messages
Write clear, concise commit messages:
- Use present tense ("Add feature" not "Added feature")
- Use imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit first line to 72 characters
- Reference issues when applicable (#123)

**Examples:**
```
Add support for custom SSL certificates

Fix port conflict detection on Windows

Update troubleshooting documentation
```

---

## Testing

### Compile and Test
```bash
npm run compile
npm test
```

### Manual Testing
1. Start the extension in debug mode (`F5`)
2. Open an HTML project in the Extension Development Host
3. Test all commands:
   - `Live Server++: Open Server`
   - `Live Server++: Close Server`
4. Verify hot reload functionality
5. Test with different browsers and ports

---

## Submitting Changes

### Before Submitting

1. **Ensure code compiles:**
   ```bash
   npm run compile
   ```

2. **Run tests:**
   ```bash
   npm test
   ```

3. **Check for linting errors:**
   ```bash
   npm run lint
   ```

4. **Update documentation** if needed

### Creating a Pull Request

1. **Push your changes** to your fork:
   ```bash
   git push origin feature/your-branch-name
   ```

2. **Create a Pull Request** on GitHub:
   - Provide a clear title and description
   - Reference related issues (e.g., "Fixes #123")
   - Include screenshots for UI changes
   - List any breaking changes

3. **Wait for review:**
   - Address feedback from maintainers
   - Make requested changes
   - Push updates to your branch

---

## Git Workflow

### Keeping Your Fork Updated

1. **Fetch upstream changes:**
   ```bash
   git fetch upstream
   ```

2. **Merge upstream changes into your main branch:**
   ```bash
   git checkout main
   git merge upstream/main
   ```

3. **Push updates to your fork:**
   ```bash
   git push origin main
   ```

### Resolving Conflicts

If you encounter merge conflicts:

1. **Fetch latest changes:**
   ```bash
   git fetch upstream
   ```

2. **Rebase your branch:**
   ```bash
   git checkout your-branch
   git rebase upstream/main
   ```

3. **Resolve conflicts** in your editor

4. **Continue rebase:**
   ```bash
   git add .
   git rebase --continue
   ```

5. **Force push** (only to your own branch):
   ```bash
   git push --force origin your-branch
   ```

### Common Git Issues

**Divergent Branches:**
```bash
# Configure merge strategy
git config pull.rebase false

# Pull with merge
git pull origin main
```

**Undo Last Commit (not pushed):**
```bash
git reset --soft HEAD~1
```

**Undo Changes to a File:**
```bash
git checkout -- filename.ts
```

---

## Code Style

### TypeScript Guidelines
- Use TypeScript strict mode
- Define types for all function parameters and return values
- Use interfaces for complex types
- Follow existing code patterns

### Naming Conventions
- **Classes**: PascalCase (`LiveServerPlusPlus`)
- **Functions/Methods**: camelCase (`goLive()`)
- **Constants**: UPPER_SNAKE_CASE (`INJECTED_TEXT`)
- **Files**: kebab-case (`live-server-plus-plus.ts`)

### Code Organization
- Keep functions small and focused
- Add comments for complex logic
- Use meaningful variable names
- Follow DRY (Don't Repeat Yourself) principle

### Example:
```typescript
interface IServerConfig {
  port: number;
  root: string;
  indexFile: string;
}

class LiveServer {
  private config: IServerConfig;

  constructor(config: IServerConfig) {
    this.config = config;
  }

  public start(): Promise<void> {
    // Implementation
  }
}
```

---

## Questions?

If you have questions or need help:
1. Check the [Troubleshooting Guide](./docs/TROUBLESHOOTING.md)
2. Search [existing issues](https://github.com/Helhum-coder/vscode-live-server-plus-plus/issues)
3. Create a new issue with the `question` label

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

Thank you for contributing! 🎉
