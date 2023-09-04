
[[Declaration]]
[[Pointers]]
[[array and data types]]
[[Functions]]
[[Dependency Injection]]
[[RFC]]
[[Object orientation]]
[[Concurency]]
[[Exercices]]

## blocks
a sequence of declaration and statement within matching brackets {}
## printing 

```go
fmt.printf()
fmt.println()
s:="hi"
fmt.printf("hi %s",s)
fmt.printf("hi"+s)
```
## Scan
scan reads user input
```go
var applenum int
fmt.Println("numbeer of apples?")
num,err :=fmt.Scan( )
```
## Type conversion
```go
var x int32 =1
var t int16 =2
x=int32(t)
```
## ascii and Unicode

Unicode : is 32 bit character
utf-8 : is a variable length
* 8bit utf codes are same as ascii
code points : Unicode characters
Rune : a code point in Go
### Unicode package 
Provide a set of functions to test categories of runes
```go
//return bool
IsDigit()
IsSpace()
IsLetter()
IsLower()
//conversion
ToUpper()
ToLower()
TrimSpace(s)
// string searche functions 
Compare(a,b)//return an integer comparing two strings
Contains(s,substr)
HasPrefix(s,prefix)
Index(s,substr)
```
### Strconv Package
conversion to and from string represantation of basic data types
```go
Atoi(s)//convert string to int
Itoa(s)//convert int to string
ParseFloat(s,bitSize)//convert string to a floating point number

```
## constants
```go
const x =1.3
const(
y=2
z="d"
)
```
iota : generate a set of related but distinct constant
Constant must be different but actual values is not important
```go
type Grade int
const(
A Grades=iota
B
c
d
)
```

## Control structure
```go
if x>5 {
fmt.println('hy')
}
else {
fmt.println('by')
}

switch x {
case 1:
	fmt.println('hy')
case 2:
	fmt.println('by')
default :
	fmt.println('hy')
}
//taglesss switch

switch  {
case x=1:
	fmt.println('hy')
case x= 2:
	fmt.println('by')
default :
	fmt.println('hy')
}

```
### Loop
```go
for i:=0;i<10;i++{
	fmt.println('hy')
}
//
i=1
for i<10{
	fmt.println('hy')
	i++
}
for{
	fmt.println('hy')
}
```