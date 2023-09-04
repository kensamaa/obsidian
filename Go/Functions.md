[[Exercices#Functions]]
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
//passing a array 
func foo(x *int[3])int {
	(*x)[0]=(*x)[0]+1
}
a:=[3]int {1,2,3}
foo(&a)
// passing a slice 
func foo(sli int)int {
	sli[0]=sli[0]+1
}
```
## dynamic functions
### variable as function 
```go
var funcVar func(int)int
func incFn(x int) int{
	return x+1
	}
func main(){
	funcVar =incFn
	fmt.print(funcvar(1))
}
```
### functions as arguments
functions can be passed to another function as an argument
```go
func applyIt(afunct func (int) int,var int) int{
return afunct(val)
}
```
![[Pasted image 20230812182818.png]]
### anonymous functions
dont need to name a function 
```go
fn:=funct (x int) int{return x+1}
```
### function returns a function
![[Pasted image 20230812183347.png]]
## variadic and deferred
### variable argument number
functions can take a variables number of arguments
use ellipsis ... to specify
treated as slice inside the function
![[Pasted image 20230812184306.png]]
### deferred function call
call can be deffered untill the surronding function completes
typicaly used for cleanup activities like close file or close connection to db 
```go
defer fmt.print("by")
fmt.print("hy")
```
arguments of a deferred call are evaluated immediately