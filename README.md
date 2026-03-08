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

### 3. Update Build Files (Gazelle)

If you add new Go files or dependencies, update the Bazel build files using Gazelle:
```bash
bazel run //:gazelle
```

## macOS Compatibility Notes

This project is configured to work around common macOS Xcode detection issues in `rules_go` by:
1.  Using `apple_support` in `MODULE.bazel`.
2.  Forcing a `pure` Go build (disabling CGO) via `.bazelrc`.

This ensures the project builds "out of the box" even if your local Xcode configuration is not standard.
