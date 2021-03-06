# Protocol Buffers + Docker
All inclusive protoc suite, powered by Docker and Alpine Linux.

## This fork
I made this fork to add multiple extentions. Maybe later I will try and PR them back to the original. For now this is experimental.

## What's included:
- protobuf 3.6.0.1
- gRPC 1.13.0
- gRPC-Web 1.0.0
- Google Well Known Types are automatically included (via `google/`)
- Go related tools compiled with 1.8.1, gRPC support is built-in:
  - github.com/golang/protobuf/protoc-gen-go
  - github.com/gogo/protobuf/protoc-gen-gofast
  - github.com/gogo/protobuf/protoc-gen-gogo
  - github.com/gogo/protobuf/protoc-gen-gogofast
  - github.com/gogo/protobuf/protoc-gen-gogofaster
  - github.com/gogo/protobuf/protoc-gen-gogoslick
  - github.com/twitchtv/twirp/protoc-gen-twirp
  - github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger
  - github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway
  - github.com/mwitkow/go-proto-validators
  - github.com/moul/protoc-gen-gotemplate
  - github.com/micro/protoc-gen-micro
  - github.com/infobloxopen/protoc-gen-gorm

## Supported languages
- C
- C++
- C#
- Java / JavaNano (Android)
- JavaScript
- Objective-C
- Python
- Ruby
- Go
- Swift 4
- Rust

## Usage
```
$ docker run --rm mvmaasakkers/protoc --help
Usage: /usr/bin/protoc [OPTION] PROTO_FILES
```

Don't forget you need to bind mount your files:
```
$ docker run --rm -v $(pwd):$(pwd) -w $(pwd) mvmaasakkers/protoc --python_out=. -I. myfile.proto
```

## Google Well Known Types
They are embedded in the image and are included by `protoc` automatically.
They accessible via `google/protobuf/`:
```protobuf
syntax = "proto3";

import "google/protobuf/timestamp.proto";
import "google/protobuf/duration.proto";
```

## Gogo
`gogo.proto` is embedded in the image and can be included with:
```protobuf
syntax = "proto3";

import "github.com/gogo/protobuf/gogoproto/gogo.proto";
```

## Image Size
The current image is about ~189mb and one layer. Most the space is spent on Go tools.
All the binaries are UPX'ed. Including the Swift stdlib.
