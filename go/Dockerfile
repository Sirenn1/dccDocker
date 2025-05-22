FROM golang:1.24.3 AS builder

WORKDIR /app
COPY . .

RUN go build -o hello

FROM debian:bullseye-slim

WORKDIR /app
COPY --from=builder /app/hello .

CMD ["./hello"]
