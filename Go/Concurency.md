## Parrallel Execution

two programs execute in parallel
* task my complete more quickly
## concurrent Execution

concurrent exec is not nessesary the same time as parralel 
* concurrent start and end time overlap
* parralel execute at exact same time 
mapping task to hardwar
* operating system
* go runtime scheduler
## hiding latency

concurrency improve  performance even without parallelism
tasks must periodically wait for something
other concurrent tasks can operate while one task is waiting 
## thread vs processes
threads share some context
many threads can exist in one process
## goroutines 
a [[thread]] in go 
many goroutines execute within a single os thread
## go runtimes scheduler 
* scheduler goroutine inside an os thread
* like a little os inside a single os [[thread]]
* logical processor is mapped to a thread
## communication between tasks 
tasks are largely independent but not completely independent
web server one thread per client 
image processing 1 thread per pixel
##  [[goroutine]] 
### Creating 
one goroutine is created automatically to execute the main ()
other goroutines are created using the GO keyword:
### Exiting
a goroutine exists when its code is complete 
when the main goroutine is complete all other goroutines exit
a goroutine may not exit because main completes early
### Delayed exit
go fmt.print()
time.sleep(100* time.milisecond())
fmt.print()
adding a delay in the main routine to give the new routine a chance to complete 
### timing with goroutine
adding a delay to wait a goroutine is bad 
timing assumption may be wrong
## synchronization
using a global events whose execution is viewed by all threads simultaneously
### sync waitGroup
sync package contains function synchronize between goroutines
waitGroup forces a goroutine to wait to other goroutines
contains an internal counter
## goroutine communication
goroutines usually work together to perform a bigger task 
often need to send data to collaborate
### channels
transfer data between goroutines
channel are typed 
use MAKE() to create a channel
c:=make(chan int)
send and receive data using the <-
* send data on channel 
	c <- 3
* receive data from a channel
	x:= <- c

```go
func prof(v1,v2 int,c chan int){
c<- v1* v2
}
func main(){
c:=make(chan int)
go prod(1,2,c)
go prod(3,4,c)
a:=<-c
b:= <-c
fmt.print(a*b)
}
```
### unbuffered channel 
unbuffered channels cannot hold data in transit
sending blocks until data is received 
receiving blocks until data is sent
### channel capacity
channel can contain a limited number of objects
capacity is the number of objects it can hold in transit
optional argument to make() defines channel capacity
c:= make(chan int,3)
sending only blocks if buffer is full 
