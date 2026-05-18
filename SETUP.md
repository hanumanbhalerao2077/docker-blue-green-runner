# SETUP.md (Phase 1)

## Prerequisites
- Docker Engine installed and running
- Docker Compose plugin available (or `docker-compose` v1)
- Bash + coreutils available (WSL recommended on Windows)
- `curl`, `git` installed

## Docker installation (Windows 11)
1. Install **Docker Desktop**.
2. Ensure Docker is running.
3. In Docker Desktop: enable WSL integration if using WSL.

## docker compose setup
Check both commands:
```bash
docker --version
docker compose version
# optional (older projects)
docker-compose --version
```

If `docker compose version` works but `docker-compose --version` doesn’t, the repo may still use the v1 binary in some scripts.
- In Phase 1 we removed deprecated compose syntax (`version:` key).
- The script-level fallback layer can be added later (Phase 2/3) if you want full v1/v2 compatibility.

## Linux/WSL fixes
- If running in WSL and you see CRLF errors like `$'\r': command not found`, run:
```bash
bash prevent-crlf.sh
bash prevent-crlf.sh
```

## First-time setup
1. Copy an example env:
```bash
cp -f .env.example.node .env
```
2. (If needed) generate/prepare permissions:
```bash
bash run.sh
```
If you hit permission errors, follow README security instructions and run:
```bash
sudo bash apply-security.sh
```
Then re-run:
```bash
bash run.sh
```

## Sample commands
```bash
# check current state
bash check-current-states.sh

# run deployment
bash run.sh

# view logs
docker ps
docker logs -f <your-project-name>-nginx
```

## Troubleshooting
### Docker daemon connectivity fails
- Verify Docker Desktop is running.
- Try:
```bash
docker info
```

### CRLF errors in scripts
- Re-run:
```bash
bash prevent-crlf.sh
```

### docker-compose command missing
- Verify:
```bash
docker-compose --version
docker compose version
```
- If `docker-compose` is missing but `docker compose` exists, the runner may need a fallback wrapper (recommended improvement in later phases).

