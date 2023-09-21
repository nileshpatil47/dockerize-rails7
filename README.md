# Read Me

Start here: https://github.com/nileshpatil47/dockerize-rails7

# Rails 7 on Docker demo application

This app demonstrates Rails 7 with Sqlite3, CRUD, all running in Docker.

## Features

* Rails 7
* Ruby 3
* Dockerfile and Docker Compose configuration
* Sqlite3 database
* Redis
* GitHub Actions for 
  * tests
  * Rubocop for linting
  * Building and testing of a production Docker image
* Dependabot for automated updates

## Requirements

Please ensure you are using Docker Compose V2. This project relies on the `docker compose` command, not the previous `docker-compose` standalone program.

https://docs.docker.com/compose/#compose-v2-and-the-new-docker-compose-command

Check your docker compose version with:
```
% docker compose version
Docker Compose version v2.10.2
```

## Initial setup
```
cp .env.example .env
docker compose build
docker compose run --rm web bin/rails db:setup
```

## Running the Rails app
```
docker compose up
```

## Running the Rails console
When the app is already running with `docker-compose` up, attach to the container:
```
docker compose exec web bin/rails c
```

When no container running yet, start up a new one:
```
docker compose run --rm web bin/rails c
```

## Running tests
```
docker compose run --rm web bin/rspec
```

## Updating gems
```
docker compose run --rm web bundle update
docker compose up --build
```

## Production build

(adjust tags as needed)

### with [BuildKit](https://docs.docker.com/build/buildkit/)
```
DOCKER_BUILDKIT=1 docker build --tag dockerize-rails7 --file Dockerfile . --load
```

### With legacy builder (no BuildKit)
```
docker build --tag dockerize-rails7 --file Dockerfile .
```

## Deployment

This app can be hosted wherever Ruby is supported and Sqlite3 databases can be provisioned.

#### Render

NOTE: You will need to generate a production secret with `bin/rails secret` and set it as the `SECRET_KEY_BASE` environment variable.

## Author

**Nilesh Patil**

- <https://twitter.com/nileshpatilIN>
- <https://www.linkedin.com/in/nilesh-r-patil-5b486385/>
- <https://github.com/nileshpatil47>
