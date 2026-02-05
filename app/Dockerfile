# -------- Build stage --------
FROM golang:1.22-alpine AS builder

WORKDIR /app
COPY app/go.mod app/go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o http-echo

# -------- Runtime stage --------
FROM gcr.io/distroless/base-debian12

WORKDIR /app
COPY --from=builder /app/http-echo .

USER nonroot:nonroot
EXPOSE 5678

ENTRYPOINT ["/app/http-echo"]
