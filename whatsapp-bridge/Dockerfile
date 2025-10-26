# Stage 1: Build the Go binary
FROM golang:1.24 AS builder

WORKDIR /app
COPY . .

# Download dependencies and build the binary
RUN go mod tidy
RUN go build -o server main.go

# Stage 2: Create a lightweight final image
FROM gcr.io/distroless/base-debian12

WORKDIR /app
COPY --from=builder /app/server .

# Cloud Run expects the service to listen on $PORT
ENV PORT=8080

EXPOSE 8080
CMD ["/app/server"]
