#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
FROM golang:1.23-alpine AS builder
COPY ./ /src/
WORKDIR /src/
ENV CGO_ENABLED="0"
RUN go build -o /go/bin/app

FROM alpine
EXPOSE 8080
COPY --from=builder /go/bin/app /go/bin/app
COPY --from=builder /src/config/ /go/bin/config/
COPY --from=builder /usr/local/go/lib/time/zoneinfo.zip /
ENV TZ=Asia/Shanghai
ENV ZONEINFO=/zoneinfo.zip

WORKDIR /go/bin/
ENTRYPOINT ["/go/bin/app"]
