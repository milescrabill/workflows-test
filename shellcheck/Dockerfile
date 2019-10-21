FROM ubuntu:latest

RUN apt update
RUN apt install -y shellcheck

COPY entrypoint.sh /entrypoint.sh
RUN chmod +X /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]