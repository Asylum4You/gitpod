```markdown
# gitpod Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides a comprehensive guide to the development patterns used in the `gitpod` repository. The codebase is primarily written in TypeScript and does not use a specific framework. It follows consistent coding conventions and includes automated workflows for dependency management, especially for Go modules. This guide covers file organization, import/export styles, testing patterns, and details on running common workflows.

## Coding Conventions

### File Naming
- **Style:** camelCase
- **Example:**  
  ```
  userSettings.ts
  workspaceManager.ts
  ```

### Import Style
- **Style:** Relative imports
- **Example:**
  ```typescript
  import { getUserSettings } from './userSettings';
  ```

### Export Style
- **Style:** Named exports
- **Example:**
  ```typescript
  // userSettings.ts
  export function getUserSettings() { ... }
  export const DEFAULT_SETTINGS = { ... };
  ```

### Commit Patterns
- **Type:** Freeform (no enforced prefixes)
- **Average Length:** ~62 characters

## Workflows

### Go Module Dependency Bump
**Trigger:** When Go dependencies (modules) need to be updated across the monorepo, typically for security, new features, or regular maintenance.

**Command:** `/bump-go-modules`

**Step-by-step:**
1. Identify outdated Go modules in each component or directory.
2. Update the version of dependencies in all relevant `go.mod` files.
3. Regenerate `go.sum` files to reflect the updated dependencies.
4. Repeat the update process for each affected component or directory.
5. Commit all changed `go.mod` and `go.sum` files together in a single commit.

**Files Involved:**
- `*/go.mod`
- `*/go.sum`
- `*/*/go.mod`
- `*/*/go.sum`
- `*/*/*/go.mod`
- `*/*/*/go.sum`

**Example:**
```sh
# Update dependencies in a Go module
cd my-component
go get -u
go mod tidy

# Repeat for each component, then commit all changes
git add */go.mod */go.sum */*/go.mod */*/go.sum
git commit -m "chore: bump Go module dependencies"
```

## Testing Patterns

- **Framework:** Unknown (no specific testing framework detected)
- **File Pattern:** Test files follow the `*.test.*` naming convention.
- **Example:**
  ```
  workspaceManager.test.ts
  ```

## Commands

| Command            | Purpose                                            |
|--------------------|----------------------------------------------------|
| /bump-go-modules   | Update all Go module dependencies across the repo  |
```
