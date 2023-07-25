```go
var books = [50]string{} //size of the array
books[0]="amine"
books[1]="imane"
fmt.Printf("array len  %v",len(books))

//slice
var bookslice []string
bookslice=append(bookslice,"amine")

//map
var userData=make(map[string]string)
userData["books1"]="bokees"
userData["books2"]="bokees"
userData["books3"]="bokees"

//struct
type Book struct {
    title string
    author string
}
```