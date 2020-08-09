# credentialagent-docker-compose
Credential Agent Docker Compose

This agent can be deployed on a single instance as a docker compose that will run the agent and an instance of mongo.
It is **not recommended** to use docker-compose in a production environment.

Use the credentialagent-docker-compose repo 
1. `git clone https://github.com/velocitynetworkfoundation/credentialagent-docker-compose.git`
1. `cd credentialagent-docker-compose`
1. `cp .env_example .env`
1. Update the .env file if necessary (e.g. generating new secrets)
1. `docker-compose pull`
1. `docker-compose up`
