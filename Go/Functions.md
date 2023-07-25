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