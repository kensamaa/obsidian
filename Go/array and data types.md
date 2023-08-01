# Summary
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
## Arrays
predefined array 
```go
var books = [5]int =[5]{1,2,3,4,5}
```
### Iterate on the array
```go
x:=[3]int={1,2,3}
for i ,v in range x {
fmt.Printf("ind %d,val %d",i,v)
}
```
range returns two values 
index and element at index

## Slices
a window on a underlying array
variables size up to the size of array
* Pointer  : indicate the start of the slice
* Length : number of elts in the slice
* Capacity : maximum  number of elts
```go
arr:=[...]string {"a","b","c","d"}
s1:= arr[1:3]
s2:=arr[2,5]
```
![[Pasted image 20230801215957.png]]
### Length and capacity
* len() returns the lenght
* cap() returns the capacity
### Slice literals 
 can be used to initialise slice 
 create the underlying array and create a slice to reference it
 ```go
slice:=[]int {1,2,3}
```
### variable slices
#### make
create a slice using make()
2 arg specify length/capacity
3 arg specify length and capacity separatly
 ```go
slice=make([]int,10)
sli=make([]int,10,15)
```
#### append
add element to the end of the slice
```go
sli=make([]int,10,15)
sli=append(sli,100)
```
## hash table
contains key/value pair 
each value is associated with a unique key
hash function is used to compute the slot for a key
#### advantages
* faster lookup than lists
* arbitrary keys
#### disadvatanges
* may have collisions

## Maps
implementation of hashtable
use make to create a map
![[Pasted image 20230801225818.png]]
```go
idmap:=map[string]int{"joe":123}
```
### access map
reference a value with key
returns zero if key is not present
```go
fmt.print(idmap["joe"])
```
#### adding key value pair
```go
idmap["joe"]=456
```
#### delete a key value
```go
delete(idmap,"joe")
```
### map functions
two value assignment tests for existence of the key
```go
id,p:=idmap["joe"]
```
id is value , p is presence of key
* len() returns number of values
#### iterate throw the map
use for loop
```go
for key,val :=range idmap{
	fmt.print(key,val)
}
```
## Struct
aggregate data type
groupe toghether other objects
![[Pasted image 20230801230749.png]]
### initialisation
```go
p:=new(Person)
p2:=Person(name:"joe",addr:"a dasd",phone:1231)
```



