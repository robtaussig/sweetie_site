---
name: update
description: Commit all current changes and push them to main on GitHub. Use when the user runs /update or asks to save/publish/push their changes.
disable-model-invocation: true
---

# Update

Commit everything in the working tree and push it to `main` on GitHub (`origin`).

The user has already asked for this by running /update, so commit and push without asking first.

## Steps

1. Run `git status --short` and `git diff --stat` (plus `git diff` for small changes) to see what changed.
   - If nothing has changed and nothing is waiting to be pushed, tell the user everything is up to date and stop.
2. Make sure you're on `main`. If you're on another branch, stop and tell the user instead of switching.
3. Stage everything: `git add -A`. `.gitignore` already leaves out junk files like `.DS_Store` and `.fuse_hidden*`.
4. Before committing, check for anything that doesn't belong: secrets, `.env` files, or very large files (over about 50MB, which GitHub rejects). If you find any, unstage them and tell the user.
5. Commit with a short message that describes the actual changes (for example, "Hide Resume nav link on mobile"), not just "update". End the message with the attribution line from the session's system reminder, if there is one.
6. Push: `git push origin main`.
   - If the push is rejected because the remote has new commits, run `git pull --rebase origin main` and push again. If the rebase hits conflicts, stop and explain them to the user. Never force-push.
7. Report back in one or two lines: the commit message, how many files changed, and that it's live on GitHub.
