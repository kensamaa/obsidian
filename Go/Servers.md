
##  GOROUTINES IN SERVERS

_goroutines_ are used to serve responses to multiple requests at the same time.

Go's goroutines are a great fit for web servers because they're lighter weight than operating system threads, but still take advantage of multiple cores.

- Go servers are great for performance whether the workload is I/O _or_ CPU-bound
- Node.js and Express work well for I/O-bound tasks, but struggle with CPU-bound tasks
- Python and Django/Flask do just fine with I/O bound tasks, but frankly, no one picks Python for its performance
### steps creating server
1. Create a [new http.ServeMux](https://pkg.go.dev/net/http#NewServeMux)
2. Wrap that `mux` in a custom [middleware](https://developer.mozilla.org/en-US/docs/Glossary/Middleware) function that adds CORS headers to the response (see the tip below on how to do that).
3. Create a new [http.Server](https://pkg.go.dev/net/http#Server) and use the `corsMux` as the handler
4. Use the server's [ListenAndServe](https://pkg.go.dev/net/http#Server.ListenAndServe) method to start the server
5. Build and run your server (e.g. `go build -o out && ./out`)
```go
package main

import (
	"log"
	"net/http"
)

func main() {
	const port = "8080"

	mux := http.NewServeMux()
	corsMux := middlewareCors(mux)

	srv := &http.Server{
		Addr:    ":" + port,
		Handler: corsMux,
	}

	log.Printf("Serving on port: %s\n", port)
	log.Fatal(srv.ListenAndServe())
}

func middlewareCors(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Access-Control-Allow-Origin", "*")
		w.Header().Set("Access-Control-Allow-Methods", "GET, POST, OPTIONS, PUT, DELETE")
		w.Header().Set("Access-Control-Allow-Headers", "*")
		if r.Method == "OPTIONS" {
			w.WriteHeader(http.StatusOK)
			return
		}
		next.ServeHTTP(w, r)
	})
}
```

## MIDDLEWARE

Middleware is a way to wrap a handler with additional functionality. It is a common pattern in web applications that allows us to write DRY code. For example, we can write a middleware that logs every request to the server. We can then wrap our handler with this middleware and every request will be logged without us having to write the logging code in every handler.
## ADDING CORS HEADERS AND HANDLING OPTIONS REQUESTS

For simple applications, this middleware is enough to handle CORS requirements. That said, these headers open our server up to all domains, all headers, and all HTTP methods. In a production system, we might want to be more selective about which domains we allow, which headers we allow, and which methods we allow.

```go
func middlewareCors(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Access-Control-Allow-Origin", "*")
		w.Header().Set("Access-Control-Allow-Methods", "GET, POST, OPTIONS, PUT, DELETE")
		w.Header().Set("Access-Control-Allow-Headers", "*")
		if r.Method == "OPTIONS" {
			w.WriteHeader(http.StatusOK)
			return
		}
		next.ServeHTTP(w, r)
	})
}```
### LOGGING EVERY REQUEST

```go
func middlewareLog(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		log.Printf("%s %s", r.Method, r.URL.Path)
		next.ServeHTTP(w, r)
	})
}```