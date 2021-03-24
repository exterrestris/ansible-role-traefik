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

### Configuration
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `traefik_config_dir` | `"/etc/traefik"` | Directory to store Traefik config files |
| `traefik_log_dir` | `"/var/log/traefik"` | Directory to store Traefik log files |
| `traefik_tls_certificates` | `[]` | Certificates to provide to Trafik |
| `traefik_providers` | `"{{ traefik_default_providers }}"` | Provider definitions |
| `traefik_routers` | `[]` | Router definitions |
| `traefik_services` | `[]` | Service definitions |
| `traefik_entrypoints` | `"{{ traefik_default_entrypoints }}"` | Entry Point definitions |
| `traefik_http_entrypoint_name` | `"http"` | Name for default HTTP entrypoint |
| `traefik_https_entrypoint_name` | `"https"` | Name for default HTTPS entrypoint |
| `traefik_insecure_api` | `false` | Enable insecure API access |
| `traefik_dashboard` | `true` | Enable dashboard |
| `traefik_dashboard_router_name` | `"dashboard"` | Name for dashboard router |
| `traefik_dashboard_entrypoints` | `["{{ traefik_http_entrypoint_name }}", "{{ traefik_https_entrypoint_name }}"]` | Entrypoints to bind dashboard router to |
| `traefik_log_enabled` | `no` | Enable system log |
| `traefik_log_file` | `"traefik.log"` | System log filename |
| `traefik_access_log_enabled` | `no` | Enable access log |
| `traefik_access_log_file` | `"access.log"` | Access log filename |
| `traefik_provider_file_directory` | `""{{ traefik_config_dir }}/conf.d""` | Directory for file-based dynamic configuration files |
| `traefik_provider_file_watch` | `"true"` | Watch files in `traefik_provider_file_directory` for changes |

#### Docker specific configuration
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `traefik_docker_compose` | `""{{ traefik_config_dir }}""` | Location for generated `docker-compose.yaml` |
| `traefik_docker_service_name` | `"traefik"` | Name of service in `docker-compose.yaml` |
| `traefik_docker_networks` | `"{{ traefik_default_docker_networks }}"` | Networks to create in `docker-compose.yaml`. Traefik container will be attached to all networks listed |
| `traefik_docker_network` | `"traefik"` | Name of default network |
| `traefik_docker_network_driver` | `"bridge"` | Driver type for default network  |
| `traefik_docker_network_driver_options` | `"{}"` | Driver options for default network |
| `traefik_docker_network_alias` | `""{{ traefik_docker_network }}""` | "Public" name for default network |
| `traefik_docker_socket` | `"/var/run/docker.sock"` | Path to Docker socket. Will be bound to same path in container |
| `traefik_provider_docker_endpoint` | `""unix://{{ traefik_docker_socket }}""` | Endpoint for Docker provider |

#### `traefik_tls_certificates[]`
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `cert` | *Required* | Path to the full certificate chain |
| `key` | *Required* | Path to the private key |
| `default` | `no` | Set as the default certificate |

#### `traefik_routers[]`
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `name` | *Required* | Router name |
| `type` | `"http"` | Router type: `"http"`, `"tcp"` or `"udp"`  |
| `rule` | *Required* | Rule to match |
| `service` | *Required* | Service to route to |
| `entrypoints` | `[]` | List of entrypoints to bind router definition to |
| `create` | `"both"` | For `"http"` and `"tcp"` router types, specifies whether to create secure (`"secure"`), insecure (`"insecure"`), or both secure and insecure (`"both"`) router defintions. If both secure and insecure definitions are created, the same settings will be applied to both definitions.

#### `traefik_services[]`
| Variable | Default | Comments |
| :--- | :--- | :--- |
| `name` | *Required* | Service name |
| `type` | `"http"` | Service type: `"http"`, `"tcp"` or `"udp"` |
| `servers` | *Required* | List of server URLs to load balance between |


