# Use the official Golang image to build the application
FROM golang:1.20-alpine as builder

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy the Go Modules manifests
COPY go.mod go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum are not changed
RUN go mod tidy

# Copy the source code into the container
COPY . .

# Build the Go app
RUN go build -o main .

# Start a new stage to build a minimal image for running the app
FROM alpine:latest  

# Set the Current Working Directory inside the container
WORKDIR /root/

# Copy the pre-built binary file from the previous stage
COPY --from=builder /app/main .

# Expose the port the app runs on
EXPOSE 8080

# Command to run the application
CMD ["./main"]
