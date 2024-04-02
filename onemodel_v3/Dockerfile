# Now define the runtime image
FROM python:3.8

ARG AWS_ACCESS_KEY_ID=""
ARG AWS_SECRET_ACCESS_KEY=""
ARG INDEX_FILE_NAME=""
ARG OPENSEARCH_URL=""
ARG OPENSEARCH_PASSWORD=""
ARG BM_CUTOFF=""
ARG NUGU_PROXY_API_KEY=""
ARG API_VERSION=""
ARG STACK_TYPE=""
ARG REDIS_HOST=""

ENV AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
ENV AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
ENV INDEX_FILE_NAME=${INDEX_FILE_NAME}
ENV OPENSEARCH_URL=${OPENSEARCH_URL}
ENV OPENSEARCH_PASSWORD=${OPENSEARCH_PASSWORD}
ENV NUGU_PROXY_API_KEY=${NUGU_PROXY_API_KEY}
ENV BM_CUTOFF=${BM_CUTOFF}
ENV API_VERSION=${API_VERSION}
ENV STACK_TYPE=${STACK_TYPE}
ENV REDIS_HOST=${REDIS_HOST}
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8

RUN apt-get update \
 && apt-get install -yq --no-install-recommends \
    ca-certificates git \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

COPY . .
RUN pip install --upgrade pip && pip install -r requirements.txt --no-cache-dir
RUN chmod +x /docker_entrypoint.sh

EXPOSE 80

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini


# RUN mkdir -p /usr/share/man/man1
# RUN apt-get update && \
#     apt-get install -y --no-install-recommends default-jre default-jdk


# RUN java -version

# RUN apt-get update && apt-get install -y curl git
# RUN curl -s https://raw.githubusercontent.com/konlpy/konlpy/master/scripts/mecab.sh | bash -s
ENTRYPOINT ["./docker_entrypoint.sh"]