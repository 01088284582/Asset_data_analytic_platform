# Copyright 2021 Acryl Data, Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Use eclipse-temurin as base image as it is the successor of AdoptOpenJDK and is TCK-certified.
FROM eclipse-temurin:8-jre-focal

# Arguments for the script
ARG DATAHUB_VERSION=latest
ARG ELASTIC_SETUP_TIMEOUT_SECONDS=60
ARG WAIT_FOR_GMS=false
# GMS endpoint for healthcheck
ARG DATAHUB_GMS_HOST=datahub-gms
ARG DATAHUB_GMS_PORT=8080

RUN groupadd --system datahub && \
    useradd --system --gid datahub datahub

WORKDIR /app
COPY build/distributions/datahub-frontend-${DATAHUB_VERSION}.zip /app/datahub-frontend.zip
RUN unzip datahub-frontend.zip && \
    rm datahub-frontend.zip

WORKDIR /app/datahub-frontend-${DATAHUB_VERSION}

COPY ../../docker/datahub-frontend/check-gms.sh /app/
COPY ../../docker/datahub-frontend/check-es.sh /app/
RUN chmod +x /app/check-gms.sh
RUN chmod +x /app/check-es.sh
RUN chown -R datahub:datahub /app

USER datahub

EXPOSE 9002 4318

ENTRYPOINT ["./bin/datahub-frontend"]
