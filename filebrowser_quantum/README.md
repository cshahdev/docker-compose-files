# FileBrowser Quantum

Advanced fork of FileBrowser. Self-hosted web file manager with multi-source support, 2FA, office docs preview/edit.

## Prerequisites

- Docker & Docker Compose
- External network `internal-net` (or `fury-net`)
- External volume `filebrowser_tmp` for temp storage

## Configuration

```bash
cp .env.example .env
```

| Variable                     | Default              | Description                  |
| ---------------------------- | -------------------- | ---------------------------- |
| `IMAGE_TAG`                  | `latest`             | FileBrowser version          |
| `NETWORK_NAME`               | `internal-net`       | External network name        |
| `TZ`                         | `Asia/Kolkata`       | Timezone                     |
| `UID`                        | `1000`               | User ID for file permissions |
| `GID`                        | `1000`               | Group ID for file permissions |
| `FILEBROWSER_ADMIN_PASSWORD` | `change-me`          | Admin password               |
| `FILEBROWSER_PORT`           | `8080`               | Web UI port                  |
| `FILEBROWSER_DATA_PATH`      | `./filebrowser_data` | Config/database storage path |

## Custom Volume Mounts

Add personal folders via `compose.custom.yml`:

```yaml
services:
  filebrowser_quantum:
    volumes:
      - /host/path:/container/path
```

File is git-ignored for personal configs.

## Usage

```bash
# Start (base only)
docker compose up -d

# Start with custom volumes
docker compose -f compose.yml -f compose.custom.yml up -d

# Stop
docker compose down

# Logs
docker compose logs -f

# Update
docker compose pull && docker compose up -d
```

## Access

- URL: `http://localhost:8080` (or configured port)
- Default user: `admin`
- Password: Set via `FILEBROWSER_ADMIN_PASSWORD`

## Network

Create external network:

```bash
docker network create fury-net
```

## Volumes

- `filebrowser_data` - Config file (`config.yaml`), database, user settings (bind mount)
- `filebrowser_tmp` - Temp storage for uploads/operations (external volume, must exist)
- Custom mounts - Defined in `compose.custom.yml`

**Create tmp volume:**
```bash
docker volume create filebrowser_tmp
```

## Configuration File

Config stored at `/home/filebrowser/data/config.yaml` inside container.

**Location via env:** `FILEBROWSER_CONFIG=data/config.yaml`

**Common settings:**
```yaml
server:
  port: 80
  sources:
    - name: "Files"
      path: "/folder"

auth:
  method: "password"  # Options: password, oidc, proxy

frontend:
  theme: "dark"  # UI theme
```

Config changes require container restart. See [docs](https://filebrowserquantum.com/en/docs/) for full options.

## Security

- Change default admin password immediately
- Restrict port access via firewall for production
- Review file permissions on mounted volumes
- Use HTTPS reverse proxy (Traefik/Caddy) for public access

## Troubleshooting

**Can't login:**

- Verify `FILEBROWSER_ADMIN_PASSWORD` in `.env`
- Check logs: `docker compose logs filebrowser_quantum`

**Custom volumes not mounting:**

- Ensure using: `docker compose -f compose.yml -f compose.custom.yml up -d`
- Verify paths exist on host
- Check permissions

**Permission denied on files:**

- Match `UID`/`GID` in `.env` to host user
- Check host directory ownership: `chown -R 1000:1000 /path`
- Verify volume paths in `compose.custom.yml`

## Resources

- [FileBrowser Quantum Docs](https://filebrowserquantum.com/en/docs/)
- [GitHub](https://github.com/gtstef/filebrowser)
