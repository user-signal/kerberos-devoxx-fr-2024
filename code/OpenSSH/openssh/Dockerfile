FROM ubuntu:22.04

RUN apt update && apt install -y nano openssh-server krb5-user

RUN sed -i 's/#GSSAPIAuthentication no/GSSAPIAuthentication yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#GSSAPICleanupCredentials yes/GSSAPICleanupCredentials yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#GSSAPIStrictAcceptorCheck yes/GSSAPIStrictAcceptorCheck no/g' /etc/ssh/sshd_config
RUN sed -i 's/#GSSAPIKeyExchange no/GSSAPIKeyExchange yes/g' /etc/ssh/sshd_config
RUN mkdir /run/sshd
RUN useradd -mg users fred
RUN echo fred@SIGUSR.NET > /home/fred/.k5login

CMD ["bash", "-c", "cp /etc/keytabs/openssh.keytab /etc/krb5.keytab && /usr/sbin/sshd -D -e"]