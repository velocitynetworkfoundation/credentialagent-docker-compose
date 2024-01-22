# credentialagent-docker-compose
Credential Agent Docker Compose

This agent can be deployed on a single instance as a docker compose that will run the agent and an instance of mongo.
It is **not recommended** to use docker-compose in a production environment.

This has been tested on Version 19 of docker and 1.26 of docker-compose. Your mileage may vary on other versions.

## Getting Started

Use the credentialagent-docker-compose repo 
1. `git clone https://github.com/velocitynetworkfoundation/credentialagent-docker-compose.git`
1. `cd credentialagent-docker-compose`
1. `cp .env_example .env`
1. Fill in empty values (and optionally modify existing ones) in the .env. (See [Credential Agent Configuration](https://www.velocitynetwork.foundation/main/developers-guide-credential-agent-operation#agent-server-configuration))
1. `docker-compose pull`
1. `docker-compose up`
1. `curl http://localhost:8080` should return a successful response


#### Agent Env Configuration

See [Credential Agent Configuration](https://www.velocitynetwork.foundation/main/developers-guide-credential-agent-operation#agent-server-configuration)
for more information about setting up environment variables and configuring the credential agent
