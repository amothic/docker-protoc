FROM dart:3.6
RUN dart pub global activate protoc_plugin
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        libprotoc-dev \
        protobuf-compiler \
    ; \
    rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["/usr/bin/protoc"]
