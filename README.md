docker-shadowsocks
==================

This Dockerfile builds an image with the Python implementation of [shadowsocks](https://github.com/shadowsocks/shadowsocks). Based on Ubuntu 16.04 image.

Quick Start
-----------

This image uses ENTRYPOINT to run the containers as an executable. 

    docker run -d -p 1984:1984 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 1984 -k $SSPASSWORD -m aes-256-cfb

You can configure the service to run on a port of your choice. Just make sure the port number given to Docker is the same as the one given to shadowsocks. Also, it is  highly recommended that you store the shadowsocks password in an environment variable as shown above. This way the password will not show in plain text when you run `docker ps`.

For more command line options, refer to the [shadowsocks documentation](https://github.com/shadowsocks/shadowsocks/tree/master)

Install On Ubuntu 18.04
-----------


    export SSPORT=[your shadowsocks port]
    export SSPASSWORD=[your shadowsocks password]

    # Install docker prerequisites
    sudo apt update
    sudo apt install apt-transport-https ca-certificates
    sudo apt install linux-image-extra-$(uname -r) linux-image-extra-virtual

    # Add docker GPG key
    sudo apt-key adv \
        --keyserver hkp://ha.pool.sks-keyservers.net:80 \
        --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

    # Add docker apt repository
    echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list

    # Install the docker engine
    sudo apt update
    sudo apt install docker-engine

    # Make sure docker service is running
    sudo service docker status
    sudo service docker start

    # Test docker installation
    sudo docker run hello-world

    # Install the shadowsocks docker image
    sudo docker pull oddrationale/docker-shadowsocks

    sudo docker run -d \
        --name shadowsocks \
        --restart=always \
        -p $SSPORT:$SSPORT \
        oddrationale/docker-shadowsocks \
        -qq \
        -m aes-256-cfb \
        -s 0.0.0.0 \
        -p $SSPORT \
        -k $SSPASSWORD
        
  ## Shadowsocks Windows Client
  
    https://github.com/shadowsocks/shadowsocks-windows/releases
