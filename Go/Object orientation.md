## classes and encapsulation
collection of datafield and [[function]] that shares a well defined responsability
classes are templates
contain data fields not data
[[Exercices#object orientation]]
## support for classes
### association methods with data
methode has reciever type that it is associated with 
use dot notation to call the method 
![[Pasted image 20230812202323.png]]
### implicit method argument
object v is an implicit argument to the method
call by value
### struct with methods
![[Pasted image 20230812203135.png]]
### controlling access
can define public function to allow access to hidden data
using packages and import the package
### controlling access to struct
need initMe() to assign hidden data 
hide fields of struct by startin field name with lower caser letter
![[Pasted image 20230812204748.png]]
![[Pasted image 20230812204927.png]]
access to hidden fields only through public methods
### point receiver
 all method for a type have pointer receivers or all methods for type have non pointer receivers!
 [[F4IHsGA5EeiEZRKxXgWFpg_17912270603911e8a2ca5752f6e50088_m3_t2_3.pptx]]
## polymorphism
ability for a object to have different forms depending on the context
[[polymorphism]]
## interfaces
set of method signatures
![[Pasted image 20230812220424.png]]
no need to state it explicitly
![[Pasted image 20230812222650.png]]
![[Pasted image 20230812222712.png]]
### empty interface
empty [[interface]] specify no methode 
all types satisfy the empty interface
use it to have a function accept any type as a parameter
```go
func printme(val interface{}){
fmt.print(val)
}
```


