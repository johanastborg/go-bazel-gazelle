# Go Bazel Gazelle Project

A simple REST API built with Go using only native libraries, managed by Bazel's Bzlmod system with `rules_go` and Gazelle.

## Project Structure

- `main.go`: The Go source code for the REST API.
- `MODULE.bazel`: Bazel module definitions (Bzlmod).
- `BUILD.bazel`: Bazel build instructions.
- `.bazelrc`: Global Bazel configuration flags (optimized for macOS/pure Go).
- `go.mod`: Go module definition.

## Prerequisites

- [Bazel](https://bazel.build/install) (v7.0.0 or later recommended).
- [Go](https://go.dev/doc/install) (v1.23.0 or later recommended).
- macOS users: XCode Command Line Tools.

## Getting Started

### 1. Build the Project

To build the Go binary:
```bash
bazel build //:go-bazel-gazelle
```

### 2. Run the Server

To run the REST API server:
```bash
bazel run //:go-bazel-gazelle
```

Once running, the server listens on port `8080`. You can test it with `curl`:
```bash
curl http://localhost:8080/api/hello
```

### 4. Build and Run with Docker

To build the OCI container image and run it locally with Docker:
```bash
./run_docker.sh
```

This script will:
1.  Build the OCI loadable tarball using Bazel.
2.  Load the image into your local Docker daemon.
3.  Start a container on port `8080`.

Alternatively, you can build the image directly:

To build the OCI image:
```bash
bazel build //:image
```

To load the image into Docker manually:
```bash
bazel run //:load
```

Once running, the containerized API is available at:
```bash
curl http://localhost:8080/api/hello
```

This project is configured to work around common macOS Xcode detection issues in `rules_go` by:
1.  Using `apple_support` in `MODULE.bazel`.
2.  Forcing a `pure` Go build (disabling CGO) via `.bazelrc`.

This ensures the project builds "out of the box" even if your local Xcode configuration is not standard.
