# Chembience Docker Postgres RDKit Module 

2021-03-06, markus.sitzmann@gmail.com

This repository is a fork of the [Docker "Official Image"](https://github.com/docker-library/official-images#what-are-official-images) for [`postgres`](https://hub.docker.com/_/postgres/).
It adds builds of the Postgres [RDKit](https:/github.com/rdkit/rdkit) extension module. The project has been created as 
component of the [Chembience](https://github/chembience/chembience), however, can be used for local Docker image builds 
independently of the Chembience setup . Additionally, the following ready-to-use Docker image
builds are made available at [Dockerhub](https://hub.docker.com/r/chembience/postgres-rdkit/tags?page=1&ordering=last_updated):

|  Postgres | RDKit extension  | Docker Image                                                     | Build Status
|-----------|------------------|------------------------------------------------------------------|--------------
|  13       | 2020.9           |  docker pull chembience/postgres-rdkit:postgres-13.rdkit-2020.09 | [![Docker](https://github.com/chembience/docker-postgres-rdkit-compile/actions/workflows/docker-build-postgres13-rdkit-2020-09.yml/badge.svg)](https://github.com/chembience/docker-postgres-rdkit-compile/actions/workflows/docker-build-postgres13-rdkit-2020-09.yml)
|  12       | 2020.3           |  docker pull chembience/postgres-rdkit:postgres-12.rdkit-2020.03 | [![Docker](https://github.com/chembience/docker-postgres-rdkit-compile/actions/workflows/docker-build-postgres12-rdkit-2020-03.yml/badge.svg)](https://github.com/chembience/docker-postgres-rdkit-compile/actions/workflows/docker-build-postgres12-rdkit-2020-03.yml)
|  11       | 2019.9           |  docker pull chembience/postgres-rdkit:postgres-11.rdkit-2019.09 | [![Docker](https://github.com/chembience/docker-postgres-rdkit-compile/actions/workflows/docker-build-postgres11-rdkit-2019-09.yml/badge.svg)](https://github.com/chembience/docker-postgres-rdkit-compile/actions/workflows/docker-build-postgres11-rdkit-2019-09.yml)

Currently, only RDKit extension for Postgres 11 and newer are supported and only Debian builds are available.

## How to build to image locally

Clone the repository, use the Postgres update.sh script and run build script:

```shell script
git clone https://github.com/chembience/docker-postgres-rdkit-compile
cd docker-postgres-rdkit-compile
./update.sh
./build
```
This would build all available Docker images in the table above. In order to build a specific one, add a specific 
target, e.g. postgres-rdkit-13:
 ```shell script
./build postgres-rdkit-13
```

## How to configure the database

There are no particular changes made with regard to Postgres in comparison to the parent version of this GitHub repository. 
Hence, it can be configured the way it is described at [the official-images repository](https://hub.docker.com/_/postgres/).

## How to start a database instance and use the RDKit extension

In each of the version directories in the repository root (11/, 12/, or 13/), there is a docker-compose.yml file
which demonstrates how to include the database to your own docker-compose-based project. The 
terms "postgres_rdkit_db_volume_xx" and "sphere" in the yml file can be changed according to your own needs, they
are just presets in order do start a demonstration system. To do this, e.g. with Postgres 13, go there and
start the database with docker-compose:
```shell script
cd 13
docker-compose up 
```
You can access the database with the psql script there for testing (the password for this test project is set 
to "Postgres0"):
```
./psql
Password for user postgres: 
psql (13.2 (Debian 13.2-1.pgdg100+1))
Type "help" for help.

postgres=# create extension rdkit;
CREATE EXTENSION
postgres=# 
```
For the configuration of Postgres user and password add the variables
```
POSTGRES_PASSWORD=Postgres0
POSTGRES_USER=postgres
```

to the .env file of your docker-compose.yml project file. For further configuration details read the section above
or read the README of the original project.


## Original README as provided by the source project of this fork:


# https://github.com/docker-library/postgres

## Maintained by: [the PostgreSQL Docker Community](https://github.com/docker-library/postgres)

This is the Git repo of the [Docker "Official Image"](https://github.com/docker-library/official-images#what-are-official-images) for [`postgres`](https://hub.docker.com/_/postgres/) (not to be confused with any official `postgres` image provided by `postgres` upstream). See [the Docker Hub page](https://hub.docker.com/_/postgres/) for the full readme on how to use this Docker image and for information regarding contributing and issues.

The [full image description on Docker Hub](https://hub.docker.com/_/postgres/) is generated/maintained over in [the docker-library/docs repository](https://github.com/docker-library/docs), specifically in [the `postgres` directory](https://github.com/docker-library/docs/tree/master/postgres).

## See a change merged here that doesn't show up on Docker Hub yet?

For more information about the full official images change lifecycle, see [the "An image's source changed in Git, now what?" FAQ entry](https://github.com/docker-library/faq#an-images-source-changed-in-git-now-what).

For outstanding `postgres` image PRs, check [PRs with the "library/postgres" label on the official-images repository](https://github.com/docker-library/official-images/labels/library%2Fpostgres). For the current "source of truth" for [`postgres`](https://hub.docker.com/_/postgres/), see [the `library/postgres` file in the official-images repository](https://github.com/docker-library/official-images/blob/master/library/postgres).

---

-	[![build status badge](https://img.shields.io/github/workflow/status/docker-library/postgres/GitHub%20CI/master?label=GitHub%20CI)](https://github.com/docker-library/postgres/actions?query=workflow%3A%22GitHub+CI%22+branch%3Amaster)
-	[![build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/update.sh/job/postgres.svg?label=Automated%20update.sh)](https://doi-janky.infosiftr.net/job/update.sh/job/postgres/)

| Build | Status | Badges | (per-arch) |
|:-:|:-:|:-:|:-:|
| [![amd64 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/amd64/job/postgres.svg?label=amd64)](https://doi-janky.infosiftr.net/job/multiarch/job/amd64/job/postgres/) | [![arm32v5 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v5/job/postgres.svg?label=arm32v5)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v5/job/postgres/) | [![arm32v6 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v6/job/postgres.svg?label=arm32v6)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v6/job/postgres/) | [![arm32v7 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v7/job/postgres.svg?label=arm32v7)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v7/job/postgres/) |
| [![arm64v8 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/postgres.svg?label=arm64v8)](https://doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/postgres/) | [![i386 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/i386/job/postgres.svg?label=i386)](https://doi-janky.infosiftr.net/job/multiarch/job/i386/job/postgres/) | [![mips64le build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/mips64le/job/postgres.svg?label=mips64le)](https://doi-janky.infosiftr.net/job/multiarch/job/mips64le/job/postgres/) | [![ppc64le build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/ppc64le/job/postgres.svg?label=ppc64le)](https://doi-janky.infosiftr.net/job/multiarch/job/ppc64le/job/postgres/) |
| [![s390x build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/s390x/job/postgres.svg?label=s390x)](https://doi-janky.infosiftr.net/job/multiarch/job/s390x/job/postgres/) | [![put-shared build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/put-shared/job/light/job/postgres.svg?label=put-shared)](https://doi-janky.infosiftr.net/job/put-shared/job/light/job/postgres/) |

<!-- THIS FILE IS GENERATED BY https://github.com/docker-library/docs/blob/master/generate-repo-stub-readme.sh -->
