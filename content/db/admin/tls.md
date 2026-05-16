---
weight: 7
title: TLS Certificates
bookToc: true
---

# TLS Certificates

Setting up certificates allows the server accept **`HTTPS`** secure connections with clients.

It is mandatory for all external connections to include a valid TLS certificates and authentication tokens.
External connections must be allowed and [configured manually](/docs/db/admin/create) along side with the TLS
settings.

## Self-Signed Certificates

The following steps can be done to generate and use a minimal server self-signed server certificate (which will act as a CA certificate for clients):

{{% steps %}}
1. Generate a self-signed Certificate for the server

   ```sh
   # generate server private key
   openssl genrsa -out server.key 2048

   # generate server certificate
   openssl req -new -x509 -days 36500 -key server.key -out server.crt
   ```

2. Copy the server certificate and Key to the **`repo/certs`** directory

   ```sh
   cp server.crt repo/certs
   cp server.key repo/certs
   ```

3. Update the server configuration file settings **`repo/server.json`** matching your external interface:

   ```SQL
    {
	  "host": "<host_name>",
	  "port": 8080,
	  "tls": true,
	  "tls_cert": "certs/server.crt",
	  "tls_key": "certs/server.key"
	}]
   ```

4. Using server certificate as CA for client connections:

   ```sh
   # connect to the server using TLS
   amelie https://<host_name>

   # connect to the server using TLS (with server certificate validation)
   amelie https://<host_name> --tls_ca="server.crt"
   ```
{{% /steps %}}

Please note that the server does not verify client certificates in the following setup.
