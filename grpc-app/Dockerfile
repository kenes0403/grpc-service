FROM --platform=$BUILDPLATFORM golang:alpine AS builder
ARG TARGETOS
ARG TARGETARCH
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN GOOS=${TARGETOS} GOARCH=${TARGETARCH} go build -o grpc-app ./helloworld/greeter_server

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/grpc-app .
RUN chmod +x ./grpc-app
EXPOSE 50051
CMD ["./grpc-app"]