# Troubleshooting Guide

This guide helps you resolve common issues when using Live Server++.

## Table of Contents
- [macOS File System Errors](#macos-file-system-errors)
- [Git Issues](#git-issues)
- [Port Conflicts](#port-conflicts)
- [Missing Files](#missing-files)

---

## macOS File System Errors

### Problem: "EROFS: read-only file system" Error

**Error Message:**
```
Unable to write file '/private/var/folders/.../Visual Studio Code.app/...'
Error: EROFS: read-only file system
```

**Cause:**
This is caused by macOS App Translocation, a security feature that sandboxes applications downloaded from the internet into a read-only temporary location.

**Solution:**

1. **Move VS Code to Applications folder:**
   - Quit VS Code completely
   - Open Finder and go to your Downloads folder (or wherever VS Code is located)
   - Drag Visual Studio Code.app to your `/Applications` folder
   - Launch VS Code from the Applications folder
   - macOS will remove the App Translocation quarantine

2. **Alternative: Remove quarantine attribute manually:**
   ```bash
   xattr -dr com.apple.quarantine "/Applications/Visual Studio Code.app"
   ```

3. **Verify the fix:**
   - Restart VS Code
   - The error should no longer appear

**Prevention:**
- Always install applications to the `/Applications` folder
- Download VS Code from official sources

---

## Git Issues

### Problem: Divergent Branches

**Error Message:**
```
hint: You have divergent branches and need to specify how to reconcile them.
```

**Cause:**
Your local branch and the remote branch have different commits.

**Solution:**

1. **Configure Git to merge by default:**
   ```bash
   git config pull.rebase false
   ```

2. **Pull changes with merge strategy:**
   ```bash
   git pull --no-rebase origin <branch-name>
   ```

3. **Or configure Git to rebase by default:**
   ```bash
   git config pull.rebase true
   git pull origin <branch-name>
   ```

### Problem: Empty Pathspec Error

**Error Message:**
```
fatal: empty string is not a valid pathspec
```

**Cause:**
Git command has invalid or empty file path argument.

**Solution:**
- Remove trailing `--` without file paths: Use `git add -A` instead of `git add -A --`
- Ensure file paths are properly specified

### Problem: Unable to Commit or Push

**Solution:**
1. **Check git status:**
   ```bash
   git status
   ```

2. **Stage all changes:**
   ```bash
   git add .
   ```

3. **Commit changes:**
   ```bash
   git commit -m "Your commit message"
   ```

4. **Push to remote:**
   ```bash
   git push origin <branch-name>
   ```

---

## Port Conflicts

### Problem: Port Already in Use

**Error Message:**
```
5555 is already in use!
```

**Cause:**
Another application or server is using the configured port.

**Solutions:**

1. **Change the port in VS Code settings:**
   - Open Settings (Ctrl+, or Cmd+,)
   - Search for "Live Server++ Port"
   - Change to a different port (e.g., 5556, 8080, 3000)

2. **Use random port:**
   - Set port to `0` in settings
   - Live Server++ will automatically find an available port

3. **Find and stop the conflicting process:**
   
   **On macOS/Linux:**
   ```bash
   lsof -i :5555
   kill -9 <PID>
   ```
   
   **On Windows:**
   ```powershell
   netstat -ano | findstr :5555
   taskkill /PID <PID> /F
   ```

---

## Missing Files

### Problem: Logo or Asset Files Not Found

**Cause:**
Files might not be tracked by Git or were excluded by `.gitignore`.

**Solution:**

1. **Check if files are tracked:**
   ```bash
   git ls-files images/
   ```

2. **Check .gitignore:**
   ```bash
   cat .gitignore
   ```

3. **Add missing files:**
   ```bash
   git add images/
   git commit -m "Add missing image files"
   git push
   ```

4. **Verify files exist locally:**
   ```bash
   ls -la images/
   ```

---

## Getting Help

If you continue to experience issues:

1. Check the [GitHub Issues](https://github.com/ritwickdey/vscode-live-server-plus-plus/issues) page
2. Search for similar problems
3. Create a new issue with:
   - Error message (full text)
   - Steps to reproduce
   - Your environment (OS, VS Code version, extension version)
   - Screenshots if applicable

---

## Additional Resources

- [VS Code Documentation](https://code.visualstudio.com/docs)
- [Git Documentation](https://git-scm.com/doc)
- [macOS Security Features](https://support.apple.com/guide/security/welcome/web)
