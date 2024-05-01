# AnjunaSoftHSM
Anjuna Deployment of SoftHSM

## Prerequisites
- Anjuna Runtime Installed on Amazon EC2 Instance with Nitro Flag Enabled.
- Docker Installed on the Parent Host

## Setup
1. Clone this repository:

# Usage (Before Running in Anjuna Seaglass)

1. Start the containers using Docker Compose:

This command will build the images (if not already built) and start the containers with the specified configuration.

2. The PKI key generation container will connect to the SoftHSM server running in the SoftHSM container over TCP/IP and generate an RSA key pair.

# Configuration

- The SoftHSM container is configured with the following environment variables:
- `SOFTHSM2_TOKEN_LABEL`: The label of the SoftHSM token (default: "my-token").
- `SOFTHSM2_TOKEN_PIN`: The PIN for the SoftHSM token (default: "1234").
- `SOFTHSM2_TOKEN_SO_PIN`: The Security Officer PIN for the SoftHSM token (default: "1234").
- The PKI key generation container is configured with the following environment variables:
- `SOFTHSM2_SERVER_IP`: The IP address or hostname of the SoftHSM container (default: "softhsm-container").
- `SOFTHSM2_SERVER_PORT`: The port number of the SoftHSM server (default: "5657").
- `SOFTHSM2_TOKEN_PIN`: The PIN for the SoftHSM token (default: "1234").

## Configuration

The SoftHSM container is configured with the following environment variables:

- `SOFTHSM2_TOKEN_LABEL`: The label of the SoftHSM token (default: "my-token").
- `SOFTHSM2_TOKEN_PIN`: The PIN for the SoftHSM token (default: "1234").
- `SOFTHSM2_TOKEN_SO_PIN`: The Security Officer PIN for the SoftHSM token (default: "1234").

The PKI key generation container is configured with the following environment variables:

- `SOFTHSM2_SERVER_IP`: The IP address or hostname of the SoftHSM container (default: "softhsm-container").
- `SOFTHSM2_SERVER_PORT`: The port number of the SoftHSM server (default: "5657").
- `SOFTHSM2_TOKEN_PIN`: The PIN for the SoftHSM token (default: "1234").
