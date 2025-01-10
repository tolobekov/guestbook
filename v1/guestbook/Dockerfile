FROM golang:1.18 as builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

FROM ubuntu:18.04

# Use COPY with --from= to copy the binary from the builder stage
COPY --from=builder /app/main /app/guestbook

# Use ADD or COPY to include the public assets
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

WORKDIR /app

# CMD to execute the application
CMD ["./guestbook"]

# EXPOSE the application port
EXPOSE 3000
