# Gophish Docker Setup

## Overview

This repository provides a Docker Compose setup for Gophish, a phishing simulation tool. The Docker Compose file defines a service for running Gophish with environment variables, port mappings, and volume bindings.

## Docker Compose Configuration

### `docker-compose.yml`

This configuration sets up Gophish with the following settings:

- **Image**: `gophish/gophish:${SOFTWARE_VERSION_TAG}`
- **Environment Variables**:
  - `GOPHISH_INITIAL_ADMIN_PASSWORD`: Admin password for Gophish.
- **Ports**:
  - `8443:8443`: Maps host port 8443 to container port 8443.
  - `8080:8080`: Maps host port 8080 to container port 8080.
  - `51766:3333`: Maps host port 51766 to container port 3333.
- **Volumes**:
  - `data:/opt/gophish`: Mounts the `data` volume to `/opt/gophish` inside the container.

### Example `docker-compose.yml`

```yaml
version: "3"
services:
  gophish:
    image: gophish/gophish:${SOFTWARE_VERSION_TAG}
    restart: always
    environment:
      - GOPHISH_INITIAL_ADMIN_PASSWORD=${ADMIN_PASSWORD}
    ports:
      - "8443:8443" # Map host port 8443 to container port 8443
      - "8080:8080" # Map host port 8080 to container port 8080
      - "51766:3333" # Map host port 51766 to container port 3333
    volumes:
      - data:/opt/gophish

volumes:
  data:
    driver: local
    driver_opts:
      type: none
      device: ${PWD}/data
      o: bind
```

## Common docker commands to go wit this (put this in termnal)

```bash

docker-compose up

docker-compose logs -f

docker-compose down

docker-compose config

```

- build image/run container
- logs container logs and outputs it to your local termnal
- stops container
- validate container
- press q to exit

# Use https for localhost not http what to copy and paste in your browser

https://localhost:51766/

## Refrences for the docker registery

https://hub.docker.com/r/elestio/gophish

https://getgophish.com/documentation/

https://getgophish.com/

### In gitignore

data
.env
# gophish-docker-container
