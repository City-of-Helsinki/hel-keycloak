Keycloak-asennus dockeriin
=========

Asentaa keycloakin pyörimään koneelle jossa ompi dockeri odottamassa.

Tarpehet
------------

Ei vielä tiedossa olevia

Roolimuuttujat
--------------

Tämmöset:
    keycloak_initial_admin_name
    keycloak_initial_admin_pw

Dependencies
------------

Docker tarvitsee asentaa sopivalla roolilla.

Pelikirjaesimerkki
----------------

- hosts: dev-korppi
  gather_facts: yes
  become: yes
  vars_files:
  vars:
    keycloak_initial_admin_name: admin
    keycloak_initial_admin_pw: hyvinsalainensalasanataisittenvaansangenpitkäsellainen
  roles:
  - role: geerlingguy.docker
  - role: keycloak-in-docker


License
-------

MIT

Author Information
------------------

Written by Ville Koivunen. Contact us through the role address: dev@hel.fi
