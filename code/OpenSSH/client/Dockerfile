FROM ubuntu:22.04

RUN apt update && apt install iputils-ping openssh-client krb5-user -y
COPY krb5.conf /etc/krb5.conf

RUN useradd -mg users fred
RUN echo "fred:fred" | chpasswd
USER fred

ENTRYPOINT ["tail", "-f", "/dev/null"]
