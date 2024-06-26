# syntax=docker/dockerfile:1

FROM golang:1.19

# Set destination for COPY
WORKDIR /app

# Download Go modules
COPY go.mod go.sum ./

# Update packages
RUN go mod tidy
RUN GO111MODULE=on go get github.com/labstack/echo/v4 github.com/labstack/echo/v4/middleware

# Copy the source code. Note the slash at the end, as explained in
# https://docs.docker.com/reference/dockerfile/#copy
COPY *.go ./

# Test
RUN CGO_ENABLED=0 GOOS=linux go test

# Build
RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping
RUN chmod a+x /docker-gs-ping

# Optional:
# To bind to a TCP port, runtime parameters must be supplied to the docker command.
# But we can document in the Dockerfile what ports
# the application is going to listen on by default.
# https://docs.docker.com/reference/dockerfile/#expose
EXPOSE 8080

# Run
CMD ["/docker-gs-ping"]
