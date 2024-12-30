FROM golang:1.23-alpine AS builder
RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.36
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.5

FROM alpine:3.21
COPY --from=builder /go/bin/protoc-gen-go /usr/local/bin/
COPY --from=builder /go/bin/protoc-gen-go-grpc /usr/local/bin/
RUN apk add --no-cache protobuf protobuf-dev
ENTRYPOINT ["/usr/bin/protoc"]
