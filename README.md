# hel-keycloak-deployment

Repository for setting up Keycloak as helsinki-tunnistus component.

helsinki-tunnistus is planned to be a service enabling two functions of Helsinki Profile:
* identification of users using different services linking users to either social media identities, population registry identity or workplace identity (for city employees)
* generation of tokens that allows applications to access data in different backends of behalf of users

Most of the user data and authorization information for the tokens would be kept in separate services, with keycloak based helsinki-tunnistus serving as a "token machine".

This repository will probably contain automation necessary to install Keycloak and any extensions necessary for implementing helsinki-tunnistus service.

## Requirements
This ansible playbook requires jmespath python package to run json queries. Install it with the command below

`pip install jmespath`

## Usage

# Setup keycloak on localhost

This requires a functioning docker install:

`ansible-playbook -i local.inventory keycloak_install.yml`

Look inside keycloak_install.yml to see the default password for
"admin"-user (4IdVwfO8o8RHwcL72MVK).

# Configure keycloak using REST API

The keycloak CLI client will be available on your local under ./bin.
This folder is copied from the docker container /opt/jboss/keycloak/bin folder.


Then get the necessary tokens for administerin' keycloak:

`./bin/kcadm.sh config credentials --server http://localhost:9080/auth --realm master --user admin`

Enter the `keycloak_initial_admin_pw` from `keycloak_install.yml`

Thereafter you can setup an example configuration using:

`ansible-playbook -i local.inventory keycloak_config.yml`

# Container management
Stop all containers:
`docker container stop $(docker container ls -q -f name=keycloak_test)`

Remove all containers:
`docker container rm -v $(docker ps -aq -f name=keycloak_test)`

Remove the database volume
`docker volume rm keycloak_test_database`


