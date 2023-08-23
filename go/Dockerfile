FROM golang:1.21-alpine AS builder
RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.31
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.3

FROM alpine:3.18
COPY --from=builder /go/bin/protoc-gen-go /usr/local/bin/
COPY --from=builder /go/bin/protoc-gen-go-grpc /usr/local/bin/
RUN apk add --no-cache protobuf protobuf-dev
ENTRYPOINT ["/usr/bin/protoc"]
