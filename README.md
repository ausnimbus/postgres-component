# AusNimbus PostgreSQL *WIP*

[![Build Status](https://travis-ci.org/ausnimbus/postgres-component.svg?branch=master)](https://travis-ci.org/ausnimbus/postgres-component)
[![Docker Repository on Quay](https://quay.io/repository/ausnimbus/postgres-component/status "Docker Repository on Quay")](https://quay.io/repository/ausnimbus/postgres-component)

This repository contains the source for deploying [PostgreSQL](https://www.ausnimbus.com.au/instant-apps/postgresql/)
on [AusNimbus](https://www.ausnimbus.com.au/).

## Environment Variables

The following environment variables are available to configure your postgres instance:

- **POSTGRES_USER, POSTGRES_PASSWORD**
  This user will be granted superuser permissions for the database specified by the `MYSQL_DATABASE` variable. Both variables are required for a user to be created.  If it is not specified, then the default user of `postgres` will be used.

- **POSTGRES_DB**
  This variable is optional and allows you to specify the name of a database to be created on image startup. If it is not specified, then the value of `POSTGRES_USER` will be used.


## Versions

The versions currently supported are:

- 9.6
