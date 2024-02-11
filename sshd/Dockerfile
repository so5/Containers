FROM ubuntu:22.04
EXPOSE 22

# install packages
RUN apt update &&\
    DEBIAN_DRONTEND=noninteractive apt install -y\
    bash tcsh zsh rsync openssh-server openssh-client\
    openssh-sftp-server

# add non-root user
RUN ssh-keygen -A&&\
    useradd -m testuser &&\
    echo "testuser:passw0rd" | chpasswd

# generate key pair and change password
USER testuser
RUN mkdir -p /home/testuser/.ssh &&\
    chmod 755 /home/testuser/.ssh &&\
    ssh-keygen -N "" -f ${HOME}/.ssh/id_rsa &&\
    cp ${HOME}/.ssh/id_rsa.pub ${HOME}/.ssh/authorized_keys

USER root
CMD ["/usr/sbin/sshd", "-e", "-D"]
