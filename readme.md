# Docker Compose Setup

This repository contains Docker Compose configurations for various services including a Portainer admin interface and a MySQL-Redis database stack. The services are organized under the `stacks` directory and extend common configurations from the `configs` directory.

## Directory Structure

- **configs**
  - `services.yaml`: Base service configurations used by the Docker Compose files.
- **stacks**
  - **admin**
    - `docker-compose.yaml`: Docker Compose file for Portainer service.
  - **databases**
    - `docker-compose.yaml`: Docker Compose file for MySQL and Redis services.

## Configurations

### 1. `configs/services.yaml`
This file contains the base configurations for various services which are extended in the Docker Compose files within the `stacks` directory.

### 2. `stacks/admin/docker-compose.yaml`
This file sets up the Portainer service, a web-based interface for managing Docker environments.

- **Service**: Portainer
- **Extends**: `../../configs/services.yaml`
- **Ports**: 
  - Maps port `9000` on the host to port `9000` in the container.

### 3. `stacks/databases/docker-compose.yaml`
This file sets up a MySQL database and a Redis service.

- **Services**:
  - **MySQL**:
    - **Extends**: `../../configs/services.yaml`
    - **Volumes**: 
      - `db_data:/var/lib/mysql` to persist MySQL data.
    - **Ports**: 
      - Maps port `3306` on the host to port `3306` in the container.
  - **Redis**:
    - **Extends**: `../../configs/services.yaml`
    - **Ports**: 
      - Maps port `6379` on the host to port `6379` in the container.

## Usage

1. **Admin Stack**:
   - Navigate to `stacks/admin` and run:
     ```bash
     docker-compose up -d
     ```
   - Access Portainer at `http://localhost:9000`.

2. **Database Stack**:
   - Navigate to `stacks/databases` and run:
     ```bash
     docker-compose up -d
     ```

## Notes

- Ensure the `configs/services.yaml` file is correctly set up with the necessary base configurations before starting the services.
- The services in each stack extend their base configurations from the common `services.yaml` file, allowing for consistent setup across different environments.
