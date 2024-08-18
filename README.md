# ClamAV Stack

Docker Compose configuration for deploying a ClamAV-based antivirus stack, including Fangfrisch and ClamSMTP services.

## Overview

This stack consists of three primary services:

1. **Fangfrisch**: Updates and manages 3rd-party ClamAV virus signatures
2. **ClamSMTP**: Scans SMTP traffic for viruses using ClamAV
3. **ClamAV**: ClamAV Antivirus engine

All services are configured for persistent data storage using Docker volumes.

## Prerequisites

- Docker
- Docker Compose

## Usage

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/alexzeitgeist/clamav-docker-compose.git
   cd clamav-docker-compose
   ```

2. **Configuration**:

   Copy the example environment file and adjust the values to fit your environment:
   ```bash
   cp .env.example .env
   ```

3. **Start the Services**:

   Use Docker Compose to bring up the services:
   ```bash
   docker-compose up -d
   ```

4. **Stop the Services**:

   To stop the services, run:
   ```bash
   docker-compose down
   ```

## Directory Structure

- **`fangfrisch/`**: Fangfrisch configuration
- **`clamsmtp/`**: ClamSMTP configuration
- **`clamav/`**: ClamAV configuration
- **`.env.example`**: Example environment file

## Environment Variables

The `.env` file provides configuration for the services. Key variables include:

- `TZ`: Timezone for all containers
- `CLAMSMTP_HOST`: Host IP for ClamSMTP service
- `CLAMSMTP_PORT`: Port for ClamSMTP service
- `EMAIL_ADMIN`: Admin email address for alerts
- `EMAIL_SERVICE`: Email address used by ClamSMTP
- `QUARANTINE_FOLDER`: Directory for quarantined files
- `SMTP_HOST`: Host for SMTP traffic
- `SMTP_PORT`: Port for SMTP traffic

## Volumes

The following Docker volumes are used for data persistence:

- **clamav_cache**: ClamAV cache storage
- **clamav_quarantine**: Quarantined files storage
- **clamav_signatures**: ClamAV signature database
- **fangfrisch_db**: Fangfrisch data

## Logging

All services use syslog for logging.
