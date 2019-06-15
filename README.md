# flyhttp
### Example
##### GET
`http://example.com?id=1&page=2`
```go
flyhttp.Get("http://example.com?id=1&page=2")

flyhttp.Get("http://example.com", "id=1&page=2")

flyhttp.Get("http://example.com", map[string][string]{
	"id":   "1",
	"page": "2",
})

flyhttp.Get("http://example.com", url.Values{
	"id":   {"1"},
	"page": {"2"},
})
```
##### POST
```go
str         := `{"name":"jhon", "age":11}`
bytes       := []byte(`{"name":"jhon", "age":11}`
reader      := strings.NewReader(`{"name":"jhon", "age":11}`)
contentType := "application/json"
header      := http.Header{"content-type":{"application/json"}}

flyhttp.Post("http://example.com", contentType, str)
flyhttp.Post("http://example.com", contentType, bytes)
flyhttp.Post("http://example.com", contentType, reader)

flyhttp.Post("http://example.com", header,      reader)
```

##### POST Forum
```go
flyhttp.PostForum("http://example.com", url.Values{
	"name": {"tom"},
	"age":  {"11"},
})

flyhttp.PostForum("http://example.com", map[string][string]{
	"name": "tom",
	"age":  "11",
})

```
### Client
```go
client := flyhttp.New(&http.Client{})
//just like above
```


### BaseURLClient
`http://example.com/path/path`
```go
client := flyhttp.NewBase("http://example.com", &http.Client{})
client.Get("/path/path")
```
使用内置的defaultClient，你可以这样做:
```go
client := flyhttp.Base("http://example.com")
```

### 注意
##### xxx.Get
虽然使用了可变长参数，
但`Get(url string, args ...interface())`至多三个实参，至少一个实参。

三个实参按 `(url, query_params, header)` 排列

以下为实参允许的类型

|名称|类型|
|-----|----|
|url|`string`|
|query_params|`string`, `map[string][string]`, `url.Values`|
|header|`http.Header`|
>*query_params 会覆盖掉 url 中的查询参数*

#### xxx.Post

虽然使用了可变长参数，

但`Post(url string, args ...interface())`**必须有三个实参**。

三个实参按 `(url, contentType|header, data)` 排列

以下为实参允许的类型

|名称|类型|
|-----|----|
|url|`string`|
|header|`http.Header`|
|contentType|`string`|
|data|`[]byte`, `string`, `io.Reader`|
-------

更多请见测试文件
