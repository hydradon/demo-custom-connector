# Self Managed Connectors

This directory contains some tooling and docker compose images for spinning up self-managed
Kafka Connect pointed at Confluent Cloud. 

## Generating from template
`ccloud-env.template` defines a series of variables which are then inserted into docker-compose files
for launching docker containers as well as shell scripts for deploying connectors. 

Make your own ccloud-env file:

``cp ccloud-env.template ccloud-env``

Edit ccloud-env with the required information, including:
-Your Confluent Cloud host
-Your Confluent Cloud schema registry URL, API key and Secret
-Your Conflunet Cloud API Key and Secret
-AWS region, access key and secret key for configuring the DynamoDB Connector

Run

``ccloud-env.sh``

This will create:
-A docker-compose-ccloud-connect.yml file that will spin up a kafka-connect
worker node that can connect to Confluent Cloud
-A ``create-dynamodb-connector.sh`` that will upload the install and configure
the dynamodb connector in your local connect worker.

Copy the manifest zip file from kafka-connect-dynamodb to the ``files`` directory
so it is picked up by the docker container

-Spin up the images in docker:

``docker-compose -f ./docker-compose-ccloud-connect.yml up``

## Deploying the connector

To install the dynamoDB connector, run:

``./create-dynamodb-connector.sh``

To check its status, run:

``check-connectors.sh``
or
``debug-connectors.sh``

 
