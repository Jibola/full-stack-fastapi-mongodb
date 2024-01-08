# Full Stack FastAPI, React, MongoDB (FARM) Base Project Generator

Accelerate your next web development project with this FastAPI/React/MongoDB base project generator.

This project is for developers looking to build and maintain full-feature progressive web applications using Python on the backend / Typescript on the frontend, and want the complex-but-routine aspects of auth 'n auth, and component and deployment configuration, taken care of, including interactive API documentation. 

This is an **experimental** fork of [Sebastián Ramírez's](https://github.com/tiangolo) [Full Stack FastAPI and PostgreSQL Base Project Generator](https://github.com/tiangolo/full-stack-fastapi-postgresql) and [Whythawk's](https://github.com/whythawk) [Full Stack FastAPI and PostgreSQL Base Project Generator](https://github.com/whythawk/full-stack-fastapi-postgresql). FastAPI is updated to version 0.103.2, MongoDB Motor 3.4, ODMantic ODM 1.0.0, and the frontend to React.

## Index

- [Requirements](#requirements)
- [QuickStart](#quickstart)
- [Screenshots](#screenshots)
- [Key features](#key-features)
- [How to use it](#how-to-use-it)
  - [Building a Generated App](./docs/getting-started.md)
  - [Development and installation](./docs/development-guide.md)
  - [Deployment for production](./docs/deployment-guide.md)
  - [Authentication and magic tokens](./docs/authentication-guide.md)
  - [Websockets for interactive communication](./docs/websocket-guide.md)
- [More details](#more-details)
- [Help needed](#help-needed)
- [Release notes](#release-notes)
- [License](#license)


## Requirements

Please make sure you have these installed before proceeding!
* [Docker Desktop](https://www.docker.com/products/docker-desktop/)
* [Python 3.11+](https://www.python.org/downloads/)
* [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/) -- The Python Cookiecutter library.
* [Hatch](https://hatch.pypa.io/latest/)
* [Node.js](https://nodejs.org/en)
* [MongoDB Compass](https://www.mongodb.com/products/tools/compass) -- To help visualize local/remote database easily.

## QuickStart

For those that what to dive in and play around with the generated code, here's quick start guide on how to do it. It is advised, though, once you have run through generating this app the first time, that you circle back and check out to more fleshed out [Building a Generated App](./docs/getting-started.md) section.

```
// Make sure cookiecutter and python are installed on the device
// This will generate a full-stack app in the directory ./example
cookiecutter https://github.com/mongodb-labs/full-stack-fastapi-mongodb --no-input project_name="example"

// change into that directory
cd example

// Make sure that you've opened Docker before this step
// build
docker compose build --no-cache

// start the container in the background
docker compose up -d 
```

Now, you can view the site by going to `localhost:3000`. You can also see all the logs of the running containers in your Docker Desktop app.

The will only be one user on the site, `admin@example.com`. If you choose a different project name, then the email domain changes. i.e. `project_name=fullstackexample` the user email will be `admin@fullstackexample.com`. The default password will be set to `changethis` but that can be changed. Please check out the [Building a Generated App](./docs/getting-started.md) to understand the configuration details better.

Here are all the local development URLS:

- Frontend -- http://localhost:3000
- Backend -- http://localhost/api/v1/
- Automatic Documentation via Swagger UI -- http://localhost/docs
- Alternative Documentation via ReDoc -- http://localhost/redoc
- Flower: Admin tool of Celery Tasks -- http://localhost:5555
- Traefik UI to see how routes are being handled by the proxy: http://localhost:8090

See [Screenshot](#screenshots) section for images of what some of these pages will look like.



## Screenshots

### App landing page

![Landing page](img/landing.png)

### Dashboard Login

![Magic-link login](img/login.png)

### Dashboard User Management

![Moderator user management](img/dashboard.png)

### Interactive API documentation

![Interactive API docs](img/redoc.png)

### Enabling two-factor security (TOTP)

![Enabling TOTP](img/totp.png)

## Key features

This FastAPI, React, MongoDB repo will generate a complete web application stack as a foundation for your project development.

- **Docker Compose** integration and optimization for local development.
- **Authentication** user management schemas, models, crud and apis already built, with OAuth2 JWT token support & default hashing. Offers _magic link_ authentication, with password fallback, with cookie management, including `access` and `refresh` tokens.
- [**FastAPI**](https://github.com/tiangolo/fastapi) backend with [Inboard](https://inboard.bws.bio/) one-repo Docker images:
  - **MongoDB Motor** https://motor.readthedocs.io/en/stable/
  - **MongoDB ODMantic** for handling ODM creation https://art049.github.io/odmantic/
  - **Common CRUD** support via generic inheritance.
  - **Standards-based**: Based on (and fully compatible with) the open standards for APIs: [OpenAPI](https://github.com/OAI/OpenAPI-Specification) and [JSON Schema](http://json-schema.org/).
  - [**Many other features**]("https://fastapi.tiangolo.com/features/"): including automatic validation, serialization, interactive documentation, etc.
- [**Nextjs/React**](https://nextjs.org/) frontend:
  - **Authorization** route-based authentication, including logged in or superuser.
  - **Form validation** with [React useForm](https://react-hook-form.com/docs/useform)
  - **State management** with [Redux](https://redux.js.org/)
  - **CSS and templates** with [TailwindCSS](https://tailwindcss.com/), [HeroIcons](https://heroicons.com/), and [HeadlessUI](https://headlessui.com/).
- **Celery** worker that can import and use models and code from the rest of the backend selectively.
- **Flower** for Celery jobs monitoring.
- Load balancing between frontend and backend with **Traefik**, so you can have both under the same domain, separated by path, but served by different containers.
- Traefik integration, including Let's Encrypt **HTTPS** certificates automatic generation.
- GitLab **CI** (continuous integration), including frontend and backend testing.

## How to use the Template

- [Building a Generated App](./docs/getting-started.md)
- [Development and installation](./docs/development-guide.md)
- [Deployment for production](./docs/deployment-guide.md)
- [Authentication and magic tokens](./docs/authentication-guide.md)
- [Websockets for interactive communication](./docs/websocket-guide.md)

## More details

After using this generator, your new project (the directory created) will contain an extensive `README.md` with instructions for development, deployment, etc. You can pre-read [the project `README.md` template here too](./{{cookiecutter.project_slug}}/README.md).

This current release (October 2023) is for FastAPI version 0.103 and introduces support for Pydantic 2. Since this is intended as a base stack on which you will build complex applications, there is no intention of backwards compatability between releases, and the objective is to ensure that each release has the latest long-term-support versions of the core libraries so that you can rely on your application core for as long as possible.

To align with [Inboard](https://inboard.bws.bio/), Poetry has been deprecated in favour of [Hatch](https://hatch.pypa.io/latest/). This will also, hopefully, sort out some Poetry-related Docker build errors.

## Help needed

This stack is in an experimental state, so there is no guarantee for to not find bugs or issues. Please open an issue ticket against this repository to make us aware of issues and we will do our best to respond to them in a timely manner. Please leave feedback on features that would be very beneficial for developers who often leverage mongodb in their FastAPI stack.


## Release Notes

For each release of the generated apps, please assume any changed introduced as the potential to be a backwards-breaking change.

See notes: 

## CalVer 2024.01.XX
- **TODO**

## CalVer 2023.12.XX
- Replaced Beanie usage with ODMantic

## CalVer 2023.11.10

- Replaced Next/Vue.js frontend framework with entirely React/Redux
- Replaced Backend native connection of PostgreSQL/SQLAlchemy with MongoDB Motor/Beanie ODM
- Removed Neo4j plugin
- Removed Alembic Usage
- Introduced new cookiecutter environment variables `mongodb_uri`, and `mongo_database`
- Introduced support for Pydantic 2

[Historic changes from whythawk](https://github.com/whythawk/full-stack-fastapi-postgresql/releases)
[Historic changes from original](https://github.com/tiangolo/full-stack-fastapi-postgresql#release-notes)

## License

This project is licensed under the terms of the MIT license.
