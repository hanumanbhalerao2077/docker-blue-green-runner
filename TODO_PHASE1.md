# TODO_PHASE1

- [ ] STEP 1: full repo scan (CRLF, permissions, deprecated compose, broken paths, shell compatibility, dependencies, env refs)
- [ ] STEP 2: inspect .docker/nginx/Dockerfile + templates + activation scripts + verify prepared templates exist
- [ ] STEP 3: apply safest fixes
  - [ ] backup critical files before changes
  - [ ] remove deprecated compose `version:` keys from root compose originals (+ sample if safe)
  - [ ] add docker-compose v1/v2 fallback wrapper (without breaking existing usage)
  - [ ] normalize CRLF handling (only where safe)
  - [ ] ensure executable permissions for .sh files (repo-level)
- [ ] STEP 4: create docs
  - [ ] CHANGELOG.md
  - [ ] SETUP.md
  - [ ] DEBUGGING.md
- [ ] STEP 5: run validation commands (docker versions + bash run.sh + docker ps/logs + curl health)
- [ ] STEP 6: final Phase 1 report (fixes + remaining risks)

