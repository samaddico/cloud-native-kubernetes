FROM golang:1.9-alpine as builder
ADD https://github.com/golang/dep/releases/download/v0.4.1/dep-linux-amd64 /usr/bin/dep
RUN apk update && apk upgrade && apk add --no-cache bash git openssh
RUN chmod +x /usr/bin/dep

WORKDIR ${TRAVIS_HOME}/gopath/src/github.com/malike/cloud-native-kubernetes/go-service
COPY . ./
RUN go build -o /go/bin/goservice ./main.go

FROM alpine
COPY --from=builder /go/bin/goservice ./
EXPOSE 8079
ENTRYPOINT ["./goservice"]