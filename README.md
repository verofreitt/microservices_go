# Microservices Go Project

This project is a microservices architecture implemented in Go, featuring at least two main services: `account` and `catalog`. Each service uses gRPC for communication and Protocol Buffers for data serialization.

## Features

- **Account Service**: Manages user accounts (create, list, retrieve).
- **Catalog Service**: Manages product catalog (add, list, retrieve products).
- **gRPC**: All inter-service communication is done via gRPC.
- **Protobuf**: Data contracts are defined using Protocol Buffers (`.proto` files).
- **Docker**: Each service can be containerized for easy deployment.
- **Modern Go Practices**: Uses the latest Go modules, Protobuf plugins, and gRPC APIs.

## Project Structure

```
├── account/
│   ├── account.proto
│   ├── pb/
│   │   ├── account.pb.go
│   │   └── account_grpc.pb.go
│   ├── client.go
│   ├── server.go
│   ├── service.go
│   ├── repository.go
│   └── ...
├── catalog/
│   ├── catalog.proto
│   ├── pb/
│   │   ├── catalog.pb.go
│   │   └── catalog_grpc.pb.go
│   ├── client.go
│   ├── server.go
│   ├── service.go
│   ├── repository.go
│   └── ...
├── docker-compose.yaml
├── go.mod
├── go.sum
└── README.md
```

## Getting Started

### Prerequisites
- Go 1.18+
- Protocol Buffers compiler (`protoc`)
- Protobuf Go plugins:
  ```bash
  go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
  go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
  export PATH="$(go env GOPATH)/bin:$PATH"
  ```
- Docker (optional, for containerization)

### Generating Protobuf Files

From each service directory (e.g., `account/`, `catalog/`):
```bash
protoc --go_out=pb --go-grpc_out=pb *.proto --proto_path=. --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative
```

### Running Services

Each service can be run individually:
```bash
cd account
# or cd catalog
# Then run:
go run ./cmd/account/main.go
```
Or use Docker Compose:
```bash
docker-compose up --build
```

## Usage
- Use a gRPC client (e.g., [grpcurl](https://github.com/fullstorydev/grpcurl), Postman, or your own Go client) to interact with the services.
- See the `.proto` files for available RPCs and message formats.

## Development
- All generated files (`*.pb.go`) are ignored in `.gitignore` and should be generated locally.
- Use modern Go and gRPC APIs (no deprecated methods).
- Update the README as you add new features or services.

## License
MIT
