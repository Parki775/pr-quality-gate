# PR quality gate demo

`main` is protected by a ruleset: **no merge unless the `test` check passes.**

- `calc.py` – tiny code under test
- `test_calc.py` – pytest suite
- `.github/workflows/ci.yml` – runs the tests on every PR to `main`

Green-path check: this line was merged through a passing PR.
