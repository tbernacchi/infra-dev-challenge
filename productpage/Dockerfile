# Copyright 2017 Istio Authors
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.
FROM python:3.7.4-slim

RUN mkdir -p /opt/microservices && mkdir -p /opt/microservices/tests/unit
COPY ./productpage/requirements.txt /opt/microservices/
RUN pip install --no-cache-dir -r /opt/microservices/requirements.txt && apt update -y && apt install -y curl

ARG flood_factor
ENV FLOOD_FACTOR ${flood_factor:-0}

COPY ./productpage/test-requirements.txt /opt/microservices
RUN pip install --no-cache-dir -r /opt/microservices/test-requirements.txt 

COPY ./productpage/productpage.py /opt/microservices/
COPY ./productpage/tests/unit/* /opt/microservices/tests/unit/
COPY ./productpage/templates/* /opt/microservices/templates/
COPY ./productpage/static/* /opt/microservices/static/
COPY ./productpage/requirements.txt /opt/microservices/

EXPOSE 9080
WORKDIR /opt/microservices

USER 1

CMD ["python", "productpage.py", "9080"]
