# Swift Supabase Auth HTTP Client

A Swift HTTP client for Supabase Auth generated from the official OpenAPI specification using Apple's Swift OpenAPI Generator.

## ⚠️ Warning

**This is a Proof of Concept (POC) and is not meant for production use.**

This project is experimental and should not be used in production environments. It's intended for:
- Learning and experimentation
- Testing Swift OpenAPI Generator capabilities

## Overview

This package provides a type-safe Swift client for the Supabase Auth REST API, automatically generated from the official OpenAPI specification. It includes:

- Complete type definitions for all Supabase Auth API endpoints
- Type-safe request/response handling
- Support for all authentication flows (password, OAuth, Web3, etc.)
- Generated from the latest Supabase Auth OpenAPI spec

## Requirements

- Swift 6.0+
- macOS 10.15+, iOS 13+, tvOS 13+, watchOS 6+, visionOS 1+

## Installation

Add this package to your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/grdsdev/swift-supabase-auth-http", branch: "main")
]
```

## Usage

```swift
import SupabaseAuthHTTP
import OpenAPIURLSession

// Create a client
let client = Client(
    serverURL: URL(string: "https://your-project.supabase.co/auth/v1")!,
    transport: URLSessionTransport()
)

// Example: Sign in with email and password
let response = try await client.postToken(
    .init(
        query: .init(grant_type: .password),
        body: .json(.init(
            email: "user@example.com",
            password: "password123"
        ))
    )
)
```

## Development

### Prerequisites

- Swift 6.0+
- Make

### Updating the OpenAPI Specification

To pull the latest OpenAPI spec from Supabase:

```bash
make pull-spec
```

### Generating Swift Code

To regenerate the Swift client from the OpenAPI spec:

```bash
make generate
```

### Building

```bash
make build
```

### Available Make Targets

- `make help` - Show all available targets
- `make pull-spec` - Download latest OpenAPI spec from Supabase
- `make generate` - Generate Swift client from OpenAPI spec
- `make build` - Build the package
- `make clean` - Clean generated files
- `make clean-all` - Clean everything including dependencies

## Project Structure

```
Sources/SupabaseAuthHTTP/Generated/
├── Client.swift    # Generated HTTP client
└── Types.swift     # Generated type definitions
```

## Dependencies

This package depends on:
- [Swift OpenAPI Runtime](https://github.com/apple/swift-openapi-runtime)
- [Swift OpenAPI URLSession](https://github.com/apple/swift-openapi-urlsession)

## Related Projects

- [Supabase Auth](https://supabase.com/auth) - The official Supabase Auth service
- [Swift OpenAPI Generator](https://github.com/apple/swift-openapi-generator) - Apple's OpenAPI code generator
- [Supabase Swift](https://github.com/supabase/supabase-swift) - Official Supabase Swift client
