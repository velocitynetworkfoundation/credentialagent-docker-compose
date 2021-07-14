# credentialagent-docker-compose
Credential Agent Docker Compose

This agent can be deployed on a single instance as a docker compose that will run the agent and an instance of mongo.
It is **not recommended** to use docker-compose in a production environment.

This has been tested on Version 19 of docker and 1.26 of docker-compose. Your mileage may vary on other versions.

## Docker Prerequisites
1. Go to https://github.com/settings/tokens/new
1. Specify what the token can do (add at least read:packages)
1. Save the token into your working dir in a file named vnf-github-package.token.
1. cat ./vnf-github-package.token | docker login https://ghcr.io -u USERNAME --password-stdin where USERNAME is the github username.

## Getting Started

Use the credentialagent-docker-compose repo 
1. `git clone https://github.com/velocitynetworkfoundation/credentialagent-docker-compose.git`
1. `cd credentialagent-docker-compose`
1. `cp .env_example .env`
1. Update the .env file if necessary (e.g. generating new `SECRET` or pointing at a different `VENDOR_URL`)
1. `docker-compose pull`
1. `docker-compose up`
1. `curl http://localhost:8080` should return a successful response


#### Agent Env Configuration

The agent runs on HTTPS or HTTP. If you would like to use TLS (recommended) to connect to the agent either:

- use the SERVER_CERTIFICATE_\* to have the agent run TLS termination directly
- run a reverse proxy for TLS termination (nginx is much more efficient than your typical application server)

| _Env Var_                   | _Sample Value_                                                             | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_description_&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
| --------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NODE_ENV                    | dev (optionally you can use staging or testnet)                            | The node environment variable. (never set development or test)                                                                                                                                                                                                                                                            |
| PORT                        | 3000                                                                       | The port exposed by the docker container for serving requests. Your reverse proxy should handle SSL termination and                                                                                                                                                                                                       |
| HOST                        | 0.0.0.0                                                                    | The host listened to. Typically this does not need to be changed.                                                                                                                                                                                                                                                         |
| LOG_SEVERITY                | debug                                                                       | debug or info                                                                                                                                                                                                                                                                                                             |
| SECRET                      | SAJDK...0SAC                                                               | A unique HS256 key used for signing JWTs for the holder app. Please ensure your key encodes at least 256 bits (64 hex chars). It can be rotated at any time. Use https://www.grc.com/passwords.htm if you don't have a internal procedure for doing this.
| MONGO_SECRET                | 4CBDB...2D22                                                               | A unique HS256 key used for encrypting secret keys. Please ensure your key encodes at least 256 bits (64 hex chars). It can be rotated at any time. Use https://www.grc.com/passwords.htm if you don't have a internal procedure for doing this.
| MONGO_URI                   | mongodb://velocity-mongo:27017/credentialagent | The Mongo db url                                                                                                                                                                                                                                                                                                          |
| RPC_NODE_URL                | http://34.244.131.79:8547                                                  | The blockchain node to connect to. Typically this does not need to be changed.                                                                                                                                                                                                                                            |
| CONTRACT_ADDRESS            | 0xf49e283837D11C7c18Fb6176C29ecc3d2B2b97F9                                 | encoded address for the velocity DID registry contact on testnet. Typically this does not need to be changed.                                                                                                                                                                                                             |
| VENDOR_URL                  | https://apigateway.vendor.com                                              | The base url of the vendor gateway api endpoints. The relative path for generating offers should be `/offers/generate`                                                                                                                                                                                                    |
| BEARER_TOKEN                | eyJhbGciOi...dQssw5c                                                       | (optional) JWT token used to authenticate the agent with the vendor gateway api                                                                                                                                                                                                                                           |
| SERVER_CERTIFICATE_FILE     | ./server.crt                                                               | (optional) The certificate for the agent to run HTTPS                                                                                                                                                                                                                                                                     |
| SERVER_CERTIFICATE_KEY_FILE | ./server.key  
