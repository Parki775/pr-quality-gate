# Runbook (do the setup BEFORE class)

## Setup (once)
1. New PUBLIC repo on GitHub (rulesets are free on public repos only).
2. Push these files to `main`:
   git init && git add . && git commit -m "init" && git branch -M main
   git remote add origin https://github.com/<you>/pr-quality-gate.git && git push -u origin main
3. Wait for the Actions run to go green (the check must run once before you can pick it).
4. Settings > Rules > Rulesets > New branch ruleset
   - Name: protect-main, Enforcement: Active
   - Target: Include default branch
   - [x] Restrict deletions, [x] Block force pushes
   - [x] Require a pull request before merging (approvals: 0 if solo)
   - [x] Require status checks to pass > Add checks > type `test` > pick "GitHub Actions"
   - Bypass list: leave EMPTY (otherwise you, the admin, can still merge)
   - Create

## Live demo (2 min)
A) Bad PR (red):
   git checkout -b break-it
   # in calc.py change `return a + b` -> `return a - b`
   git commit -am "oops" && git push -u origin break-it
   Open PR -> `test` fails -> Merge button BLOCKED. Show the log.
B) Fix (green):
   # revert to a + b
   git commit -am "fix" && git push
   `test` passes -> Merge enabled -> merge.
C) Bonus: try `git push origin main` directly -> rejected (GH013: Repository rule violations).

Tip: pre-push the branches and keep both PRs open in tabs in case Wi-Fi dies.
