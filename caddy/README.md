# Caddy Reverse Proxy

This directory contains a Docker Compose setup for Caddy, a powerful web server with automatic HTTPS that serves as a reverse proxy for various services.

## Overview

Caddy acts as the entry point for web traffic, providing SSL termination and routing requests to backend services based on domain names.

## Files

- `compose.yaml` - Docker Compose configuration for Caddy
- `Caddyfile` - Caddy configuration with reverse proxy rules (currently commented out)
- `.env.example` - Environment variable template

## Setup

1. Copy the environment file:
   ```bash
   cp .env.example .env
   ```

2. Update the `DOCKER_VOLUME_PATH` in `.env` to match your system:
   ```
   DOCKER_VOLUME_PATH=/data/docker_volumes
   ```

3. Configure your services in the `Caddyfile` by uncommenting and modifying the relevant sections

4. Start the service:
   ```bash
   docker compose up -d
   ```

## Configuration

The `Caddyfile` contains example configurations for various services including:
- pgAdmin
- phpMyAdmin  
- Grafana
- Semaphore
- Calibre Web
- Authentication services (Authentik/Authelia)

Each service can be enabled by uncommenting the relevant section and updating the configuration as needed.

## Network

- **Ports**: 80 (HTTP), 443 (HTTPS), 443/UDP (HTTP/3)
- **Network**: Uses external `internal-net` network to communicate with other services
- **Volumes**: Persistent storage for certificates and configuration

## Prerequisites

- External network `internal-net` must exist
- External volume `caddy_data` must exist
- Backend services should be running and accessible on the internal network