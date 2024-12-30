FROM alpine:3.21

ARG PROTOC_JS_VERSION=3.21.4
ARG PROTOC_GRPC_WEB_VERSION=1.5.0
ARG TARGETPLATFORM

RUN apk add --no-cache protoc protobuf-dev gcompat

# Install protoc-gen-js
RUN set -ex; \
    PLATFORM=$( \
      case "${TARGETPLATFORM}" in \
        "linux/amd64") echo "x86_64";; \
        "linux/arm64") echo "aarch_64";; \
        *)             echo "x86_64";; \
      esac \
    ); \
    apk add --no-cache --virtual .fetch-deps curl tar; \
    curl -fsL "https://github.com/protocolbuffers/protobuf-javascript/releases/download/v${PROTOC_JS_VERSION}/protobuf-javascript-${PROTOC_JS_VERSION}-linux-${PLATFORM}.tar.gz" -o protobuf-javascript.tar.gz; \
    tar zxf protobuf-javascript.tar.gz --strip-components=1 bin/protoc-gen-js; \
    rm protobuf-javascript.tar.gz; \
    chmod +x protoc-gen-js; \
    mv protoc-gen-js /usr/local/bin/; \
    apk del .fetch-deps

# Install protoc-gen-grpc-web
RUN set -ex; \
    PLATFORM=$( \
      case "${TARGETPLATFORM}" in \
        "linux/amd64") echo "x86_64";; \
        "linux/arm64") echo "aarch64";; \
        *)             echo "x86_64";; \
      esac \
    ); \
    apk add --no-cache --virtual .fetch-deps curl; \
    curl -fsL "https://github.com/grpc/grpc-web/releases/download/${PROTOC_GRPC_WEB_VERSION}/protoc-gen-grpc-web-${PROTOC_GRPC_WEB_VERSION}-linux-${PLATFORM}" -o protoc-gen-grpc-web; \
    chmod +x protoc-gen-grpc-web; \
    mv protoc-gen-grpc-web /usr/local/bin/; \
    apk del .fetch-deps

ENTRYPOINT ["/usr/bin/protoc"]
