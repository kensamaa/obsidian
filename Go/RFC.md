request for comments
definitions of onternet protocol and formats
Example : 
* html
* URI
* http

## Protocol Packages 

functions that encode and decode protocol format
Example :
	"net/http"
	* web communication protocol
	* http.get()
	"net"
	* tcp/ip and socket programming
	* net.Dial("tcp","uci.edu:80")

## Json

javascript object notation
Attribute value pairs 
* struct or map
### json properties
all unicode
human readable
types can be combined recursively
* arrays of structs, struct in [[struct]]
### json marshalling
generating json representation from object 
![[Pasted image 20230810182627.png]]
### json unmarshall
![[Pasted image 20230810182826.png]]
pointer to go object is passed to unmarshal()
object must fit json []byte
## Files
### basic operation
open() get handle for access
Read() read bytes
Write() write bytes into file
close() release handle
Seek() move read/write head
### Ioutil file 
![[Pasted image 20230810183447.png]]
![[Pasted image 20230810183621.png]]
### os package
os.open() open a file
os.close()
os.read()
* fills the byte
* control the amount read
os.write()