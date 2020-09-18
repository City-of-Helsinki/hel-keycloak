# hel-keycloak-deployment

Repository for setting up Keycloak as helsinki-tunnistus component.

helsinki-tunnistus is planned to be a service enabling two functions of Helsinki Profile:
* identification of users using different services linking users to either social media identities, population registry identity or workplace identity (for city employees)
* generation of tokens that allows applications to access data in different backends of behalf of users

Most of the user data and authorization information for the tokens would be kept in separate services, with keycloak based helsinki-tunnistus serving as a "token machine".

This repository will probably contain automation necessary to install Keycloak and any extensions necessary for implementing helsinki-tunnistus service.

## Requirements
This ansible playbook requires jmespath python package to run json queries. Install it with the command below

    pip install jmespath

# Usage

## Setup keycloak on localhost

This requires a functioning docker install:

    ansible-playbook -i inventory/local.yml keycloak_install.yml

The keycloak admin is defined in the inventory  (admin/4IdVwfO8o8RHwcL72MVK).

## Configure keycloak using REST API

Make sure to wait until the keycloak is available before running the configuration.
    
    docker logs keycloak_test --follow

Wait for a message like:

    10:31:51,870 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0051: Admin console listening on http://127.0.0.1:9990

The keycloak CLI client will be available on your local under ./bin.
This folder is copied from the docker container /opt/jboss/keycloak/bin folder.

Thereafter you can setup an example configuration using:

    ansible-playbook -i inventory/local.yml keycloak_config.yml

## Container management
You can remove the keycloak and database container as well as the database volume with the command:

    ansible-playbook -i inventory/local.yml keycloak_purge.yml

### Manual container management

Stop all containers:

    docker container stop $(docker container ls -q -f name=keycloak_test)

Remove all containers:

    docker container rm -v $(docker ps -aq -f name=keycloak_test)

Remove the database volume

    docker volume rm keycloak_test_database


## Adding configurations
- Create realms and clients using the keycloak admin console GUI
- Add realm and clients definitions to the group_vars/keycloak_servers
- Run ansible-playbook -i inventory/local.yml keycloak_export.yml. The files are stored under ./roles/shared
