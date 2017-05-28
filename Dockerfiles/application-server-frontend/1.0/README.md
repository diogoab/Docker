# Docker

Image with PHP, Composer, NodeJS, NPM, Gulp, AngularJS, TypeScript, Bower and React installed and extended from marcosoliveirasoares94/ubuntu:17.04.

# Build

To create the image `marcosoliveirasoares94/application-server-frontend:1.0`, execute the following command on the project folder :

    docker build -t marcosoliveirasoares94/application-server-frontend:1.0 .

# Run

Start your image :

    docker run --name <container-name> -d marcosoliveirasoares94/application-server-frontend:1.0

# Accessing the Container
The container can be accessed via SSH, just run `ssh -p <port> root@<host>` and enter the `secret` password.

# Ports
* **22**

# Volumes
You can add any volume to the container: It can be useful to limit access to a particular section of your server.

# Issues

Please report any issues on [GitHub](https://github.com/marcosoliveirasoares94/Docker/issues).
