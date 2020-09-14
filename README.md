# hel-keycloak-deployment

Repository for setting up Keycloak as helsinki-tunnistus component.

helsinki-tunnistus is planned to be a service enabling two functions of Helsinki Profile:
* identification of users using different services linking users to either social media identities, population registry identity or workplace identity (for city employees)
* generation of tokens that allows applications to access data in different backends of behalf of users

Most of the user data and authorization information for the tokens would be kept in separate services, with keycloak based helsinki-tunnistus serving as a "token machine".

This repository will probably contain automation necessary to install Keycloak and any extensions necessary for implementing helsinki-tunnistus service.

## Usage

# Setup keycloak on localhost

This requires a functioning docker install:

`ansible-playbook -i local.inventory keycloak_install.yml`

Look inside keycloak_install.yml to see the default password for
"admin"-user.

# Configure keycloak using REST API

First you will need keycloak CLI client available on your local node.
Easiest way to get it is to download the whole "Standalone server
distribution": https://www.keycloak.org/downloads

Then add the path the `bin` directory within the extracted files to
`local_vars.yml`. For example:

`keycloak_bin_path: /usr/local/keycloak-9.0.3/bin`

Then get the necessary tokens for administerin' keycloak:

`/usr/local/keycloak-9.0.3/bin/kcadm.sh config credentials --server http://localhost:9080/auth --realm master --user admin`

Enter the `keycloak_initial_admin_pw` from `keycloak_install.yml`

Thereafter you can setup an example configuration using:

`ansible-playbook -i local.inventory keycloak_config.yml`
