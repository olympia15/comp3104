#### COMP3104 – Developer Operations
-- Olympia Santaguida-Antunes

# GitHub Action Status Badge

[![CI](https://github.com/olympia15/comp3104/actions/workflows/ci.yml/badge.svg)](https://github.com/olympia15/comp3104/actions/workflows/ci.yml)

# Commit Message Hook (Enforce Commit Message Format)
Ensures commit messages follow a specific pattern.
File: .git/hooks/commit-msg

```
#!/bin/sh
COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat $COMMIT_MSG_FILE)

if ! echo "$COMMIT_MSG" | grep -Eq "^(feat|fix|docs|style|refactor|test|chore): .+"; then
  echo "Commit message must follow the"
  echo "Expected format: <type>(<scope>): <subject>"
  exit 1
fi
```

# Pre-Commit Hook (Lint Code Before Commit)
Ensures that the code is linted before committing.
File: .git/hooks/pre-commit

```
#!/bin/sh
echo "Running pre-commit hook: Linting code..."
npm --version
if [ $? -ne 0 ]; then
  echo "Linting failed. Fix errors before committing."
  exit 1
fi
```

# Pre-Push Hook (Run Tests Before Push)
Runs tests before allowing a push.
File: .git/hooks/pre-push

```
#!/bin/sh
echo "Running pre-push hook: Running tests..."
npm test
if [ $? -ne 0 ]; then
  echo "Tests failed. Fix errors before pushing."
  exit 1
fi
```