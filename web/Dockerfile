FROM alpine:3.18

ENV GRPC_WEB_VERSION 1.4.2
ARG TARGETPLATFORM

RUN apk add --no-cache protoc protobuf-dev
RUN set -ex; \
    PLATFORM=$( \
      case "${TARGETPLATFORM}" in \
        "linux/amd64") echo "x86_64";; \
        "linux/arm64") echo "aarch64";; \
        *)             echo "x86_64";; \
      esac \
    ); \
    apk add --no-cache --virtual .fetch-deps curl; \
    curl -fsL "https://github.com/grpc/grpc-web/releases/download/${GRPC_WEB_VERSION}/protoc-gen-grpc-web-${GRPC_WEB_VERSION}-linux-${PLATFORM}" -o protoc-gen-grpc-web; \
    chmod +x protoc-gen-grpc-web; \
    mv protoc-gen-grpc-web /usr/local/bin/; \
    apk del .fetch-deps
ENTRYPOINT ["/usr/bin/protoc"]
