FROM ubuntu:22.04

RUN apt update && apt install -y krb5-kdc krb5-admin-server

COPY krb5.conf /etc/krb5.conf
RUN kdb5_util -r SIGUSR.NET -P kdc create -s
RUN kadmin.local -q "addprinc -randkey host/B.sigusr.net@SIGUSR.NET"
RUN kadmin.local -q "addprinc -pw fred fred@SIGUSR.NET"

