FROM golang:1.15-alpine as builder

ARG DOCK_PKG_DIR=/go/src/github.com/kyma-project/kyma/components/event-publisher-nats

WORKDIR $DOCK_PKG_DIR
COPY . $DOCK_PKG_DIR

RUN GOOS=linux GO111MODULE=on go mod vendor && \
    CGO_ENABLED=0 GOOS=linux GO111MODULE=on go build -o event-publisher-nats ./cmd/event-publisher-nats

FROM gcr.io/distroless/static:nonroot
LABEL source = git@github.com:kyma-project/kyma.git
USER nonroot:nonroot

WORKDIR /
COPY --from=builder /go/src/github.com/kyma-project/kyma/components/event-publisher-nats/event-publisher-nats .

COPY licenses/ /licenses/

ENTRYPOINT ["/event-publisher-nats"]
