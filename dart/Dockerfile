FROM dart:3.1
RUN dart pub global activate protoc_plugin
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends protobuf-compiler; \
    rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["/usr/bin/protoc"]
