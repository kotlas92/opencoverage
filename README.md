# Open Coverage

[![opencoverage](https://open-coverage.org/api/vangheem/repos/opencoverage/badge.svg?branch=master&project=api)](https://open-coverage.org/vangheem/repos/opencoverage)
[![build](https://img.shields.io/github/checks-status/vangheem/opencoverage/master?label=Build)](https://github.com/vangheem/opencoverage/actions)
[![license](https://img.shields.io/github/license/vangheem/opencoverage)](https://github.com/vangheem/opencoverage/blob/master/LICENSE)
[![dockerapi](https://img.shields.io/docker/v/opencoverage/api?label=Docker%28API%29)](https://hub.docker.com/r/opencoverage/api)
[![dockerfront](https://img.shields.io/docker/v/opencoverage/frontend?label=Docker%28Frontend%29)](https://hub.docker.com/r/opencoverage/frontend)
[![apihealth](https://img.shields.io/website?label=API&url=https%3A%2F%2Fopen-coverage.org%2Fapi%2Fping)](https://open-coverage.org/)

Free and open source alternative providing coverage reporting and diff coverage reporting.

The project can be a simple replacement for codecov or coveralls for teams working
on private repos.

(some of the enterprise option pricing seemed a little unreasonable)

Features:

- coverage reporting
- diff coverage reporting
- github integration: PRs, comments
- codecov cli compatible

Requirements:

- sqlalchemy compatible backend(pg, sqlite, mysql, et)
- opencoverage backend
- opencoverage frontend

SCM integrations:

- [x] github
- [ ] bitbucket
- [ ] gitlab

## Configuration

To run the server yourself, you need to create a github application and install
it for your organization.

All configuration is done with env variables.

- host
- port
- public_url
- root_path: root path api is served from
- dsn: connection string for backend database
- cors: hosts frontend runs on
- scm: enum(`github`)
- github_app_id: id of app
- github_app_pem_file: pem file for application you created
- github_default_installation_id: id of org this app is installed on

## Backend development

Develop:

```
make install-dev
```

Tests:

Run docker compose first:

```
docker-compose up postgres
```

```
make test
```

Run:

```
make run
```

## Frontend development

This project uses nextjs. See the `app` directory for details.

## Send report from CI

The backend is compatible with the codecov CLI.

You need to provide the installation id of your org as the `--token` value
or `dummy` if you are using the `github_default_installation_id` setting
and only using the server for a single org.

```
codecov --url="http://<installed-host>:8000" --token=<github installation id> --slug=vangheem/opencoverage
```
