# Changelog

## 2026-05-18 (Phase 1 - Production-grade prep)
### Fixed
- Removed deprecated Compose `version:` keys from:
  - `docker-compose-app-original.yml`
  - `docker-orchestration-app-nginx-original.yml`
  - `samples/node-express-boilerplate/docker-compose.yml`

### Improved
- Normalized `run.sh` shebang to `/usr/bin/env bash` for better bash resolution across environments.

## Notes
- This Phase 1 update is designed to be low-risk and non-destructive.

