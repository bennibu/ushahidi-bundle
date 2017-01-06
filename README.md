# Ushahidi bundle

Build and run ushahidi platform and client. Followed setup instructions on
https://www.ushahidi.com/support/install-ushahidi#installing-on-linux.

## Setup

Build docker containers:

    docker-compose build

Setup database/run migrations:

    docker-compose run platform ./bin/update --no-deps --migrate

Start applications:

    docker-compose up

Now access ushidi on http://localhost:8081. Login with user 'admin' and
password 'admin'.

## You can do better

- [ ] Improve client build: Use another node container to build assets and copy them afterwards to tiny nginx alpine container.
