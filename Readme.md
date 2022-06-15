# Simple configuration template for sorry cypress

## Aim

The aim of this repository is to provide a template on how one should
create a secured `sorry-cypres` setup.

The security is provided by the following way:
 - the dashboard and API server is not directly accessible, rather it is behind an nginx proxy
 - there is an oauth2-proxy server, which only allows traffic through for logged in users
 - the mongo db is not accessible at all
 - the director is only accessible with the valid key

## Setup

 1. configure the `oauth-proxy`. The documentation for it can be found [here](
        https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview
    )
 2. Generate a secure key for the director and add it to allowed keys. You could use the following
    command to generate the key:
    ```
    dd if=/dev/urandom bs=32 count=1 2>/dev/null | base64 | tr -d -- '\n' | tr -- '+/' '-_'; echo
    ```
 3. Setup the correct configuration variables for the docker images depending the enviroment where
    it is deployed
 4. Start the images with `docker-compose up`

## Optional improvments

Depending on your usage it might make sense to setup `https` for nginx
