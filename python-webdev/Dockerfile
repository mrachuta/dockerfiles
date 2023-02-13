FROM docker.io/library/python:3.9.10-slim-bullseye

ENV PATH="/home/python/.local/bin:${PATH}" 
RUN apt update && \
    apt install -y libpq-dev gcc && \
    useradd -ms /bin/bash -u 1001 python && \
    mkdir /app && \
    chown -R python:python /app
USER python
WORKDIR /app

CMD ["python3"]
