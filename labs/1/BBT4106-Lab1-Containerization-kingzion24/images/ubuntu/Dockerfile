FROM ubuntu:20.04

# Update package list
RUN apt-get update

# Install necessary packages
RUN apt-get install -y \
    wget \
    curl \
    ssh \
    rsync \
    openssh-server \
    nano \
    sudo \
    iputils-ping \
    ufw \
    iproute2 \
    lsb-release \
    vim

# Clean up APT when done
RUN apt-get clean

EXPOSE 3306

CMD ["bash"]