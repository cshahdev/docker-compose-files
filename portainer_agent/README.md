# Portainer Agent

Remote management agent for Portainer Server. Runs on Docker nodes to enable centralized control.

## Prerequisites

- Docker & Docker Compose
- External network `internal-net` (or custom)
- Portainer Server instance

## Configuration

```bash
cp .env.example .env
```

| Variable | Default | Description |
|----------|---------|-------------|
| `IMAGE_TAG` | `2.33.3` | Agent version |
| `NETWORK_NAME` | `internal-net` | External network name |
| `AGENT_PORT` | `9001` | Agent port |
| `AGENT_SECRET` | `my-secret-token` | Auth secret (must match server) |

## Usage

```bash
# Start
docker compose up -d

# Stop
docker compose down

# Logs
docker compose logs -f

# Update
docker compose pull && docker compose up -d
```

## Network

Create external network if needed:

```bash
docker network create internal-net
```

## Connect to Server

1. Portainer UI → **Environments** → **Add environment**
2. Select **Agent**
3. Enter endpoint: `<agent-ip>:9001`
4. Enter `AGENT_SECRET`
5. **Connect**

## Volumes

- `/var/run/docker.sock` - Container management
- `/var/lib/docker/volumes` - Volume access
- `/:/host` - System info

## Security

- Agent has privileged Docker socket + filesystem access
- Use strong `AGENT_SECRET` in production
- Restrict port 9001 via firewall
- Trust Portainer Server instances only

## Troubleshooting

**Connection fails:**
- Verify `AGENT_SECRET` matches server
- Check network connectivity on port 9001
- Review logs: `docker compose logs portainer_agent`

**Permission errors:**
- Ensure Docker socket accessible
- Check container permissions

## Resources

- [Agent Docs](https://docs.portainer.io/admin/environments/add/docker/agent)
- [Portainer](https://www.portainer.io/)
