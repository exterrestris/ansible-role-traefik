# Ansible role `exterrestris.traefik`

An Ansible role to install and configure [Traefik](https://traefik.io/traefik/) as either a Docker image using Docker Compose, or a system service

## Requirements

### Installed using Docker
- Docker
- Docker Compose
- docker and docker-compose Python libraries

### Installed as service
- systemd

## Role Variables

### Installation
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `traefik_install` | `"docker"` | Install method. Specify `"docker"` to install as Docker image, `"binary"` to install binary release as systemd service |

#### Install as Docker image
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `traefik_docker_image` | `"traefik:v2.4"` | Image to pull from Docker Hub |

#### Install as Service
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `traefik_version` | `"latest"` | Version to download. `"latest"` will select the most recent release |
| `traefik_download_dir` | `"/tmp/traefik"` | Directory to download/extract release archive |
| `traefik_install_dir` | `"/usr/local/bin"` | Directory to install binary to |
| `traefik_service_user` | `"traefik"` | System user to run service as |

