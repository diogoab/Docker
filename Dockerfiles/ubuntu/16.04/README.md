# Docker

Image default/official Ubuntu 16.04 with OpenSSH-Server installed among other basic software existing in an operating system. Service initialization process management. The list of installed software can be checked in the image file Dockerfile.

# Build

To create the image `marcosoliveirasoares94/ubuntu:16.04`, execute the following command on the project folder :

    docker build -t marcosoliveirasoares94/ubuntu:16.04 .

# Run

Start your image :

    docker run --name <container-name> -d marcosoliveirasoares94/ubuntu:16.04

# Accessing the Container
The container can be accessed via SSH, just run `ssh -p <port> root@<host>` and enter the `secret` password.

# Ports
* **22**

# Volumes
You can add any volume to the container: It can be useful to limit access to a particular section of your server.

# Issues

Please report any issues on [GitHub](https://github.com/marcosoliveirasoares94/Docker/issues).
