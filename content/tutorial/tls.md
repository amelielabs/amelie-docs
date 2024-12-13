---
weight: 7
title: TLS Certificates
bookToc: false
---

## TLS Certificates

Setting up certificates allows the server to create secure **`HTTPS TLS`** connections with clients.

The TLS support, along with the authentication, can be enabled (or turned off) for each listening address individually.
For example, it is possible to turn off the authentication for localhost and enable it for other network interfaces.

Learn more about the [Server TLS Settings](/docs/configuration/settings) and the [Server Configuration](/docs/configuration/settings).

## Self-Signed Certificates

The following steps can be done to generate and use a minimal server self-signed server certificate (which will act as a CA certificate for clients):

1. Generate a self-signed Certificate for the Server

   ```sh
   # generate server private key
   openssl genrsa -out server.key 2048

   # generate server certificate
   openssl req -new -x509 -days 36500 -key server.key -out server.crt
   ```

2. Copy the Server Certificate and Key to the **`repo/certs`** directory

   ```sh
   cp server.crt repo/certs
   cp server.key repo/certs
   ```

3. Update the Server configuration file settings **`repo/config.json`**:

   ```SQL
   "tls_cert": "certs/server.crt",
   "tls_key": "certs/server.key",
   "listen": [{
	  "host": "*",
	  "port": 3485,
	  "tls": true
	}]
   ```

4. Using server certificate as CA for client connections:

   ```sh
   # connect to the server using TLS
   amelie --uri="https://localhost:3485" --tls_ca="server.crt"

   # connect to the server using TLS (server certificate is not verified)
   amelie --uri="https://localhost:3485"
   ```

Please note that the server does not verify client certificates in the following setup.
The [Authentication](/docs/tutorial/auth) can be enabled to validate client requests over **`HTTPS`** connections.
