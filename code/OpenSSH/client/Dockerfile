FROM ubuntu:22.04

RUN apt update && apt install nano iputils-ping openssh-client krb5-user -y
COPY krb5.conf /etc/krb5.conf

RUN useradd -mg users fred
USER fred

ENTRYPOINT ["tail", "-f", "/dev/null"]
