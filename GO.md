## Declaration
 ```go
Var a int =7

Var s string

S="string"
```
## Running the code 
```go
Go run main.go   ;; compiles and run the application

Go build main.go ;; compiles and generate .exe file
```
## array and data types
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
## Functions
```go
//functions
func greatuser(){
    fmt.Println("great user")
}

//function with param
func greatuser2(name string){
    fmt.Println("great user2",name)
}

//fnction return string
func greatuser3(name string,age int) string{
    fmt.Println("great user3",name,age)
    return "great user3"
}

//function return multiple data
func greatuser4(name string,age int) (string,int){
    fmt.Println("great user4",name,age)
    return "great user4",age
}
```