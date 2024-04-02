# Now define the runtime image
FROM python:3.10.13-slim-bookworm


RUN apt-get update \
 && apt-get install -yq --no-install-recommends \
    ca-certificates git \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

COPY . .
RUN pip install --upgrade pip && pip install -r ./onemodel_v3/requirements.txt --no-cache-dir
RUN chmod +x ./onemodel_v3/docker_entrypoint.sh

EXPOSE 80

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

ENTRYPOINT ["python", "./onemodel_v3/main.py"]