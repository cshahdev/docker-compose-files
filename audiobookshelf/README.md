# Audiobookshelf

Self-hosted audiobook and podcast server for managing your personal audio library.

## Quick Start

1. Copy the environment file:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` to set your docker volume path:
   ```bash
   DOCKER_VOLUME_PATH=/data/docker_volumes
   ```

3. Start the service:
   ```bash
   docker compose up -d
   ```

## Configuration

- **Port**: 13378 (mapped to container port 80)
- **Timezone**: Asia/Kolkata
- **Network**: internal-net (external)

## Volumes

- `audiobookshelf_audiobooks`: Store your audiobook files
- `audiobookshelf_config`: Application configuration
- `audiobookshelf_metadata`: Book metadata and covers

## Access

Once running, access Audiobookshelf at: http://localhost:13378

## Version

Currently running Audiobookshelf v2.29.0