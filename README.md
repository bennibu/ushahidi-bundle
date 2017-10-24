# Ushahidi bundle

This is a docker compose folder. It builds and enables a ushahidi installation, using the ushahidi backend (ushahidi platform), the ushahidi frontend (ushahidi client), and a mariadb server. 

To build the platfomr and the client, the official instructions provided by ushahidi were used. 

Build and run ushahidi platform and client. Followed setup instructions on
https://www.ushahidi.com/support/install-ushahidi#installing-on-linux.



## How to Setup ?

First you will need a system with a running docker and docker compose already installed. 

Then you can clone this repo. Go to he cloned repo in your commandline. 
and ...


Build docker containers:

    docker-compose build

Setup database/run migrations:

    docker-compose run platform ./bin/update --no-deps --migrate

Start applications:

    docker-compose up

Now access ushidi on http://localhost:8081. Login with user 'admin' and
password 'admin'.


## NOTES.
Be sure to set the ENV variable of the backend url to a public ip or url, accesible from your web browser.  Most of the rendering of the final web page, is made using JS, and inside your browser. So you need a public url, for this to work ok. You can modify the docker file or modify it, modify it in the docker directly or use another method. 

It is recommended to put and nginx, caddy, or other web server proxy for productions purposes. 


## You can do better

- [ ] Improve client build: Use another node container to build assets and copy them afterwards to tiny nginx alpine container.
