# DEBUGGING.md (Phase 1)

## Common failures
### 1) `docker-compose: command not found`
- Check:
```bash
docker-compose --version
docker compose version
```
- Phase 1 didn’t yet add a fallback wrapper; scripts currently check for v1 in `use-common.sh`.

### 2) CRLF errors like `$'\r': command not found`
- Run:
```bash
bash prevent-crlf.sh
```
- If running in WSL2, README recommends running it twice.

### 3) `.env` validation fails
- Ensure `.env` matches `.env.example` keys exactly.
- Ensure no empty values.

## Nginx issues
### 502 / upstream not found
- Ensure `nginx-blue-green-activate.sh` successfully copied prepared config.
- Inspect:
```bash
docker logs -f <project-name>-nginx
```

### Verify prepared template flow
- Nginx container expects templates copied into `/etc/templates` by the image entrypoint.
- If nginx activation fails, run emergency script:
```bash
bash emergency-nginx-restart.sh
```

## Blue-green issues
### Wrong state or no traffic switch
- Check current states:
```bash
bash check-current-states.sh
```
- Then verify nginx upstream:
```bash
docker exec -it <project-name>-nginx nginx -T | findstr -i blue
```
(Use `findstr` on Windows; inside bash you can use `grep`.)

## Rollback usage
### Roll back the app
```bash
bash rollback.sh
```

### Roll back and restart nginx (if applicable)
```bash
bash rollback.sh 1
```

## Docker logs usage
- Follow nginx logs:
```bash
docker logs -f <project-name>-nginx
```
- Debug inside nginx:
```bash
docker exec -it <project-name>-nginx bash
```

## Health-check debugging
- From outside (host):
```bash
curl -k -Isw '%{http_code}' <APP_URL>/<APP_HEALTH_CHECK_PATH>
```
- Inside app container (replace state):
```bash
docker exec -it <project-name>-blue sh -c "curl -s -k localhost:<APP_PORT>/<APP_HEALTH_CHECK_PATH>"
```

