
a pointer is a address to data in memory 

operator & return the address of the variable 
operator  * returns data at a address 
```go

var x int =1
var y int
var ip *int
ip= &x //ip points to x 
y= *ip //y is now 1
```
alternate way to create a variable 
new() [[Functions]] create a variable and returns a pointer to the variable