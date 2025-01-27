FROM docker.io/library/python:3.11-slim-bookworm

LABEL version="3.11"
LABEL maintainer="mrachuta"

ENV PATH="/home/python/.local/bin:${PATH}"

RUN apt update && \
    apt install -y libpq-dev gcc && \
    useradd -ms /bin/bash -u 1001 python && \
    mkdir /app && \
    chown -R python:python /app && \
    apt autoremove -y && \
    apt clean -y
USER python
WORKDIR /app

CMD ["python3"]
