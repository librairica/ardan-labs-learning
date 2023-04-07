# Build the Go Binary
FROM golang:1.17 as build_service-api
ENV CGO_ENABLED 0
ARG VCS_REF
ARG BUILD_REF

# Copy the source code into the container
COPY . /service

# Build the service binary
WORKDIR /service
RUN go build -ldflags "-X main.build=${BUILD_REF}"

# Run the Go Binary in Alpine
FROM alpine:3.14
ARG BUILD_DATE
ARG BUILD_REF
COPY --from=build_service-api /service/ardan-labs-learning /service/service
WORKDIR /service
CMD ["./service"]

LABEL org.opencontainers.image.created="${BUILD_DATE}" \
      org.opencontainers.image.title="service-api" \
      org.opencontainers.image.authors="Librairica <bill@ardanlabs.com>" \
      org.opencontainers.image.source="https://github.com/librairica/ardan-labs-learning/app/service-api" \
      org.opencontainers.image.revision="${BUILD_REF}" \
      org.opencontainers.image.vendor="Ardan Labs" 