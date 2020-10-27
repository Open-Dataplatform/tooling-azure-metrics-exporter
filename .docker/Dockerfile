FROM golang:1.11 as builder
WORKDIR /go/src/github.com/RobustPerception/azure_metrics_exporter
COPY . .
RUN make build

FROM quay.io/prometheus/busybox:latest AS app

COPY --from=builder /go/src/github.com/RobustPerception/azure_metrics_exporter/azure_metrics_exporter /bin/azure_metrics_exporter

COPY ./azure_config /azure_config

WORKDIR /azure_config
EXPOSE 9276
ENTRYPOINT ["/bin/azure_metrics_exporter"]