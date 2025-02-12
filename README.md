# Authentik Docker Compose Setup

This repository contains the necessary files to set up Authentik with Docker Compose. Authentik is an open-source identity provider for managing authentication and authorization across your services.

## Prerequisites

Before you start, ensure that you have the following:

- **Docker**: Installed and running on your machine.
- **Docker Compose**: Installed to manage multi-container Docker applications.

## Setup

### 1. Clone the Repository

First, clone this repository to your local machine:

```bash
git clone https://github.com/kahnu044/authentik-docker.git
cd authentik-docker
```

### 2. Configure the `.env` File

Ensure you have the `.env` file in the root of the repository. The `.env` file contains sensitive data such as database credentials, SMTP settings, and Authentik secret keys. The environment variables in the file are already defined as shown below:

```ini
PG_PASS=your_pg_password
AUTHENTIK_SECRET_KEY=your_secret_key
AUTHENTIK_ERROR_REPORTING__ENABLED=true

# SMTP Settings for Authentik to send emails
AUTHENTIK_EMAIL__HOST=localhost
AUTHENTIK_EMAIL__PORT=25
AUTHENTIK_EMAIL__USERNAME=your_smtp_username
AUTHENTIK_EMAIL__PASSWORD=password
AUTHENTIK_EMAIL__USE_TLS=false
AUTHENTIK_EMAIL__USE_SSL=false
AUTHENTIK_EMAIL__TIMEOUT=10
AUTHENTIK_EMAIL__FROM=authentik@localhost

# Authentik Web Ports
COMPOSE_PORT_HTTP=9000
COMPOSE_PORT_HTTPS=9443
```

You can modify the values in this file as per your setup. Make sure to change the database password, SMTP server settings, and other sensitive credentials.

### 3. Start Docker Compose

Once you have configured the `.env` file, you can bring up the Docker Compose environment by running the following command:

```bash
docker-compose up -d
```

This will pull the necessary images and start the containers in detached mode. The setup includes the following services:

- **PostgreSQL**: The database used by Authentik.
- **Redis**: A cache store for Authentik.
- **Authentik Server**: The main Authentik service.
- **Worker**: The worker service for background tasks in Authentik.

### 4. Access Authentik

Once the services are up, you can access Authentik through the following ports:

- **HTTP**: [http://localhost:9000](http://localhost:9000)
- **HTTPS**: [https://localhost:9443](https://localhost:9443)

### 5. Stopping the Services

To stop the services, run the following command:

```bash
docker-compose down
```

This will stop and remove all containers, but it will not remove the volumes, so your data persists between restarts.

### 6. Logs

You can view the logs of any container by running:

```bash
docker-compose logs <service_name>
```

For example, to view logs for the Authentik server:

```bash
docker-compose logs server
```

### 7. Customization

You can customize Authentik further by modifying the configuration files and volumes:

- **Custom Templates**: You can add custom templates by modifying the `./custom-templates` directory.
- **Persistent Media**: Media files are persisted in the `./media` directory.

### 8. Troubleshooting

If you encounter any issues during startup, use the following command to check the status of all services:

```bash
docker-compose ps
```

You can also view the logs to debug any specific service:

```bash
docker-compose logs <service_name>
```
