FROM docker.io/library/3.11-slim-bookworm

RUN apt update && \
    apt install -y libpq-dev gcc && \
    useradd -ms /bin/bash -u 1001 python && \
    mkdir /app && \
    chown -R python:python /app
USER python
WORKDIR /app

CMD ["python3"]
