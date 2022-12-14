# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM debian:bullseye-slim

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y apache2 \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN a2enmod proxy proxy_http ssl md

COPY 000-default.conf 001-ssl.conf /etc/apache2/sites-enabled/
COPY *.html *.css *.css.map /var/www/html/
RUN rm /etc/apache2/sites-available/*

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE $APACHE_RUN_DIR/apache2.pid

RUN mkdir -p ${APACHE_RUN_DIR} ${APACHE_LOG_DIR}

EXPOSE 80

CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
