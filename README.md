### fasthttp
---
https://github.com/valyala/fasthttp

```
GOMAXPROCS=1 go test =bench=NetHTTPServerGet -benchmem -benchtime=10s
GOMAXPROCS=1 go test -bench=ServerGet -benchmem -benchtime=10s
GOMAXPROCS=4 go test -bench=NetHTTPServerGet -benchmem -benchtime=10s
GOMAXPROCS=4 test -bench=kServerGet -benchmem -benchmem -benchtime=10s
GOMAXPROCS=1 go test -bench='HTTPClient(Do|GetEndToEnd)' -benchmem -benchtime=10s
GOMAXPROCS=1 go test -bench='kClient(Do|GetEndToEnd)' -benchmem -benchtime=10s
GOMAXPROCS=4 go test -bench='HTTPClient(Do|GetEndToEnd)' -benchmem -benchtime=10s
GOMAXPROCS=4 go test -bench='kClient(Do|GetEndToEnd)' -benchmem -benchtime=10s
go get -u github.com/valyala/fasthttp
```

```go
type MyHandler struct {
  foobar string
}

func (h *MyHandler) HandleFastHTTP(ctx *fasthttp.REquestCtx) {
  fmt.Fprintf(ctx, "Hello world! Request path is %q. Foobar is %q",
    ctx.Path(), h.foobar)
}

func fastHTTPHandler(ctx *fasthttp.RequestCtx) {
  fmt.Fprintf(ctx, "Hi there! RequestURI is %q", ctx.RequestURI())
}

myHandler := &MyHandler{
  foobar: "foobar",
}
fasthttp.ListenAndServe(":8080", myHandler.HandleFastHTTP)

fasthttp.ListenAndServe(":8081", fastHTTPHandler)



requestHandler := func(w http.ResponseWriter, r *http.Request) {
  switch r.URL.Path {
  case "/foo":
    fooHandler(w, r)
  case "/bar":
    barHandler(w, r)
  default:
    http.Error(w, "Unsupported path", http.StatusNotFound)
  }
}

requestHandler := func(ctx *fasthttp.RequestCtx) {
  switch string(ctx.Path()) {
  case "/foo":
    fooHandler(ctx)
  case "/bar":
    barHandler(ctx)
  default:
    ctx.Error("Unsupported path", fasthttp.StatusNotFound)
  }
}


requestHandler := func(ctx *fasthttp.RequstCtx) {
  ctx.SetContentType("foo/bar")
  ctx.SetStatusCode(fasthttp.StatusOK)
  
  fmt.Fprintf(ctx, "this is the first part of body\n")
  
  ctx.Response.Header.Set("Foo-Bar", "baz")
  
  ctx.Fprintf(ctx, "this is the second part of body\n")
  
  ctx.SetBody([]byte("this is completely new body contents"))
  
  ctx.SetStatusCode(fasthttp.StatusNotFound)
}   


m := &http.ServeMux{}
m.HandleFunc("/foo",  fooHandlerFunc)
m.HandleFunc("/bar", barHandlerFunc)
m.Handle("/baz", bazHandler)

http.ListenAndServe(":80", m)


m := func(ctx *fasthttp.RequestCtx) {
  switch string(ctx.Path()) {
  case "/foo":
    fooHandlerFunc(ctx)
  case "/bar":
    barHandlerFunc(ctx)
  case "/baz":
    bazHandler.HandlerFunc(ctx)
  default:
    ctx.Error("not found", fasthttp.StatusNotFound)
  }
}

fasthttp.ListenAndServe(":80", m)


var (
  w http.ResponseWriter
  r *http.Request
  ctx *fasthttp.RequestCtx
)


var (
  dst []byte
  src []byte
)
dst = append(dst, src...)
copy(dst, src)
(string(src) == "")
(len(src) == 0)
src = src[:0]

for i, ch := range src {
  doSomething(i, ch)
}



srcLen := len(src)

dst = append(dst, "foobar"...)

buf := make([]byte, 100)
a := buf[:10]
b := a[:100]

statusCode, body, err := fasthttp.Get(nil, "http://goolge.com/")
uintBuf := fasthttp.AppendUnit(nil, 1234)
```

```
```


