# Go App — Quick Guide

## Prerequisites

* Install **Go** (recommended 1.20+):

  ```bash
  go version
  ```

---

## Start a New Project

### 1) Initialize a module (`go mod init`)

> Creates a `go.mod` file to define your project and track dependencies.

```bash
go mod init goapp
# If you plan to publish on GitHub:
# go mod init github.com/<username>/goapp
```
---

## Dependency Management

### `go mod tidy`

> Adds any missing dependencies and removes unused ones.
> Updates `go.mod` and `go.sum`.

```bash
go mod tidy
```

### `go mod download`

> Downloads all dependencies listed in `go.mod`/`go.sum` to the local cache **without modifying** the files.

```bash
go mod download
```

> **When to use which?**
>
> * Use **`tidy`** during development to auto-fix dependencies.
> * Use **`download`** in CI/CD to pre-fetch existing dependencies only.

---

## Running and Building

### `go run` — Run directly (no output file)

```bash
go run .
# Or for a specific folder:
# go run ./cmd/api
```

### `go build` — Build an executable

```bash
go build -o app .
# Run the binary:
./app        # Linux/macOS
# .\app.exe  # Windows
```

---

## Useful Commands

* Install/update a specific library version:

  ```bash
  go get github.com/gin-gonic/gin@v1.9.1
  go mod tidy
  ```

* Build a smaller binary:

  ```bash
  go build -ldflags="-s -w" -o app .
  ```

* Embed a version number into the binary:

  ```go
  // in main.go
  package main
  var Version = "dev"
  ```

  ```bash
  go build -ldflags="-X 'main.Version=1.0.0'" -o app .
  ```

* Cross-compile for another OS:

  ```bash
  GOOS=linux GOARCH=amd64 go build -o app .
  GOOS=windows GOARCH=amd64 go build -o app.exe .
  ```

---

## Recommended Project Structure

```
goapp/
  cmd/api/main.go   # Entry point
  internal/...      # Private code
  pkg/...           # Reusable code (optional)
  go.mod
  go.sum
  README.md
```

---

## Common Issues

* **`no go.mod file found`**
  Run `go mod init ...` in the project root.

* **`no Go files` or build failed**
  Make sure you are in the right folder, with `.go` files and a `package main` containing `func main()`.

* **Missing dependencies**

  ```bash
  go mod tidy
  ```

---

## Quick Start

```bash
mkdir goapp && cd goapp
go mod init goapp   
echo 'package main; import "fmt"; func main(){ fmt.Println("Hello!") }' > main.go
go mod tidy
go run .
go build -o app .
./app
```

