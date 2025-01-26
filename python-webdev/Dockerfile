FROM docker.io/library/python:3.11-slim-bookworm

LABEL version="3.11"
LABEL maintainer="mrachuta"

RUN apt update && \
    apt install -y libpq-dev gcc && \
    useradd -ms /bin/bash -u 1001 python && \
    mkdir /app && \
    chown -R python:python /app
USER python
WORKDIR /app

CMD ["python3"]
