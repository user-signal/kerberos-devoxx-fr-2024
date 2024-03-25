FROM ubuntu:22.04

RUN apt update && apt install -y openssh-server

RUN sed -i 's/#GSSAPIAuthentication no/GSSAPIAuthentication yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#GSSAPICleanupCredentials yes/GSSAPICleanupCredentials yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#GSSAPIStrictAcceptorCheck yes/GSSAPIStrictAcceptorCheck no/g' /etc/ssh/sshd_config
RUN sed -i 's/#GSSAPIKeyExchange no/GSSAPIKeyExchange no/g' /etc/ssh/sshd_config
RUN mkdir /run/sshd
RUN useradd -g users fred

CMD ["/usr/sbin/sshd", "-D", "-e"]