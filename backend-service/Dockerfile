FROM golang:1.24.2-alpine3.21 as builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o ./sitter

#FROM scratch AS sitter
FROM curlimages/curl as sitter

COPY --from=builder /app/sitter /sitter

EXPOSE 8080

ENTRYPOINT ["/sitter"]
