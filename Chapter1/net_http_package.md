# net/http Package

[net/http](https://pkg.go.dev/net/http)

## Hello World 예제

```go
package main

import (
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("Hello World!!"))
	})

	http.ListenAndServe(":8080", nil)
}
```

결과
```bash
$ curl localhost:8080
Hello World!!
```

## Handler 사용

```go
package main

import (
	"io"
	"net/http"
)

func main() {
	h1 := func(w http.ResponseWriter, r *http.Request) {
		io.WriteString(w, "Hello from a HandleFunc #1!\n")
	}
	h2 := func(w http.ResponseWriter, r *http.Request) {
		io.WriteString(w, "Hello from a HandleFunc #2!\n")
	}

	http.HandleFunc("/", h1)
	http.HandleFunc("/endpoint", h2)
	
	http.ListenAndServe(":8080", nil)
}
```

결과
```bash
$ curl localhost:8080
Hello from a HandleFunc #1!

$ curl localhost:8080/endpoint
Hello from a HandleFunc #2!
```