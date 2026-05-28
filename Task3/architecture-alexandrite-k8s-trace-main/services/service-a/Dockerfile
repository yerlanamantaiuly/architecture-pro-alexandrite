FROM golang:1.22-alpine AS builder
WORKDIR /src
COPY go.mod ./
COPY main.go ./
RUN go mod tidy && CGO_ENABLED=0 GOOS=linux go build -trimpath -ldflags="-s -w" -o /out/app .

FROM alpine:3.20
RUN adduser -D -u 10001 app
USER app
COPY --from=builder /out/app /app
EXPOSE 8080
ENTRYPOINT ["/app"]
