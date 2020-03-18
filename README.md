# hel-keycloak
Repository for setting up Keycloak as helsinki-tunnistus component.

helsinki-tunnistus is planned to be a service enabling two functions of Helsinki Profile:
* identification of users using different services linking users to either social media identities, population registry identity or workplace identity (for city employees)
* generation of tokens that allows applications to access data in different backends of behalf of users

Most of the user data and authorization information for the tokens would be kept in separate services, with keycloak based helsinki-tunnistus serving as a "token machine".

This repository will probably contain automation necessary to install Keycloak and any extensions necessary for implementing helsinki-tunnistus service.
