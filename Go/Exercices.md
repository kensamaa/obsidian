
## Accessing files
```go 
package main

  

import (

"bufio"

"fmt"

"os"

"strings"

)

  

type Name struct {

Fname [20]byte

Lname [20]byte

}

  

func main() {

var fileName string

  

fmt.Print("Enter the name of the file ")

fmt.Scan(&fileName)

  

file, err := os.Open(fileName)

if err != nil {

fmt.Println("Error opening file:", err)

return

}

defer file.Close()

  

names := make([]Name, 0)

  

scanner := bufio.NewScanner(file)

for scanner.Scan() {

line := scanner.Text()

parts := strings.Split(line, " ")

if len(parts) != 2 {

fmt.Println("Invalid format:", line)

continue

}

  

var fname [20]byte

copy(fname[:], parts[0])

var lname [20]byte

copy(lname[:], parts[1])

  

names = append(names, Name{Fname: fname, Lname: lname})

}

  

if err := scanner.Err(); err != nil {

fmt.Println("Error reading file:", err)

return

}

  

fmt.Println("Names read from the file:")

for _, name := range names {

fmt.Printf("First Name: %s, Last Name: %s\n", strings.TrimRight(string(name.Fname[:]), "\x00"), strings.TrimRight(string(name.Lname[:]), "\x00"))

}

}
```
## Functions 
### bubble sort 
```go 
package main

  

/*

Write a Bubble Sort program in Go. The program

should prompt the user to type in a sequence of up to 10 integers. The program

should print the integers out on one line, in sorted order, from least to

greatest. Use your favorite search tool to find a description of how the bubble

sort algorithm works.

As part of this program, you should write a

function called BubbleSort() which

takes a slice of integers as an argument and returns nothing. The BubbleSort() function should modify the slice so that the elements are in sorted

order.

A recurring operation in the bubble sort algorithm is

the Swap operation which swaps the position of two adjacent elements in the

slice. You should write a Swap() function which performs this operation. Your Swap()

function should take two arguments, a slice of integers and an index value i which

indicates a position in the slice. The Swap() function should return nothing, but it should swap

the contents of the slice in position i with the contents in position i+1.

*/

import (

"fmt"

)

  

func Swap(arr []int, i int) {

arr[i], arr[i+1] = arr[i+1], arr[i]

}

func BubbleSort(arr []int) {

n := len(arr)

for i := 0; i < n-1; i++ {

for j := 0; j < n-i-1; j++ {

if arr[j] > arr[j+1] {

Swap(arr, j)

}

}

}

}

func main() {

fmt.Println("Bubble Sort Program")

fmt.Println("Enter up to 10 integers")

  

var ListInteger []int

for i := 0; i < 10; i++ {

fmt.Println("enter integer number : ", i+1)

integer := 0

fmt.Scan(&integer)

ListInteger = append(ListInteger, integer)

}

fmt.Println("Unsorted integers")

fmt.Println(ListInteger)

BubbleSort(ListInteger)

fmt.Println("sorted integers with bubble sort ")

fmt.Println(ListInteger)

}
```
### function returns functions 

```go
package main

  

import (

"fmt"

"math"

)

  

func GenDisplaceFn(a float64, v float64, s float64) func(float64) float64 {

return func(t float64) float64 {

return 0.5*a*math.Pow(t, 2) + v*t + s

}

}

func main() {

  

var acceleration, InitialVelocity, InitialDisplacement, time float64

  

fmt.Print("enter the valeu of acceleration : ")

fmt.Scan(&acceleration)

  

fmt.Print("enter the valeu of InitialVelocity : ")

fmt.Scan(&InitialVelocity)

  

fmt.Print("enter the valeu of InitialDisplacement : ")

fmt.Scan(&InitialDisplacement)

  

fmt.Print("enter the time : ")

fmt.Scan(&time)

  

fn := GenDisplaceFn(acceleration, InitialVelocity, InitialDisplacement)

displacement := fn(time)

fmt.Printf("Displacement after %.2f seconds: %.2f\n", time, displacement)

  

}
```
## object orientation
```go
package main

  

import (

"fmt"

"strings"

)

  

type Animal struct {

food string

locomotion string

noise string

}

  

func Eat(a Animal) {

fmt.Println(a.food)

}

func Move(a Animal) {

fmt.Println(a.locomotion)

}

func Speak(a Animal) {

fmt.Println(a.noise)

}

func ShowDataAnimal(animalMap map[string]Animal, name string, information string) {

if _, exists := animalMap[name]; exists {

switch strings.ToLower(information) {

case "food":

fmt.Println(animalMap[name].food)

case "locomotion":

fmt.Println(animalMap[name].locomotion)

case "noise":

fmt.Println(animalMap[name].noise)

}

} else {

fmt.Println("error in requested info try food ,locomotion or noise")

}

}

func main() {

var userData = make(map[string]Animal)

userData["cow"] = Animal{"grass", "walk", "moo"}

userData["bird"] = Animal{"worm", "fly", "peep"}

userData["snake"] = Animal{"mice", "slitcher", "hsss"}

for {

request := ""

fmt.Print("write the name of animal and information requested separated by , : ")

fmt.Scan(&request)

parts := strings.Split(request, ",")

if len(parts) == 2 {

ShowDataAnimal(userData, parts[0], parts[1])

} else {

fmt.Println("Input does not contain exactly two parts separated by a space.")

continue

}

  

}

}
```
### using interface 

```go
package main

  

import (

"bufio"

"fmt"

"os"

"strings"

)

  

type Animal interface {

Eat()

Move()

Speak()

}

  

type Cow struct {

name string

}

  

func (c Cow) Eat() {

fmt.Println("grass")

}

  

func (c Cow) Move() {

fmt.Println("walk")

}

  

func (c Cow) Speak() {

fmt.Println("moo")

}

  

type Bird struct {

name string

}

  

func (b Bird) Eat() {

fmt.Println("worms")

}

  

func (b Bird) Move() {

fmt.Println("fly")

}

  

func (b Bird) Speak() {

fmt.Println("peep")

}

  

type Snake struct {

name string

}

  

func (s Snake) Eat() {

fmt.Println("mice")

}

  

func (s Snake) Move() {

fmt.Println("slither")

}

  

func (s Snake) Speak() {

fmt.Println("hsss")

}

func ExecQuery(animal Animal, info string) {

switch info {

case "eat":

animal.Eat()

case "move":

animal.Move()

case "speak":

animal.Speak()

default:

fmt.Println("Invalid info type. Available types: eat, move, speak")

  

}

}

func main() {

animals := make(map[string]Animal)

scanner := bufio.NewScanner(os.Stdin)

  

fmt.Println("Welcome to the Animal Information Program!")

fmt.Println("You can create new animals and get information about them.")

  

for {

fmt.Print("> ")

scanner.Scan()

command := scanner.Text()

parts := strings.Fields(command)

  

if len(parts) == 0 {

continue

}

  

switch strings.ToLower(parts[0]) {

case "newanimal":

if len(parts) != 3 {

fmt.Println("Invalid command. Usage: newanimal <name> <type>")

continue

}

name := parts[1]

animalType := strings.ToLower(parts[2])

var newAnimal Animal

  

switch animalType {

case "cow":

newAnimal = Cow{name: name}

case "bird":

newAnimal = Bird{name: name}

case "snake":

newAnimal = Snake{name: name}

default:

fmt.Println("Invalid animal type. Available types: cow, bird, snake")

continue

}

  

animals[name] = newAnimal

fmt.Println("Created it!")

  

case "query":

if len(parts) != 3 {

fmt.Println("Invalid command query")

continue

}

name := parts[1]

info := parts[2]

  

animal, ok := animals[name]

if !ok {

fmt.Printf("Animal with name %s not found.\n", name)

continue

}

ExecQuery(animal, info)

  

default:

fmt.Println("Invalid command. Available commands: newanimal, query")

}

}

}
```


## concurrency
<p>Ecrivez un programme pour trier un tableau d'entiers. Le programme doit diviser le tableau en 4 parties, chacune d'entre elles étant triée par
une goroutine différente. Chaque partition doit étre de taille approximativement égale. Ensuite, la goroutine principale doit fusionner les 4
sous-réseaux triés en un seul grand tableau trié.

Le programme doit inviter l'utilisateur a saisir une série d'entiers. Chaque goroutine qui trie 4 du tableau doit imprimer le sous-réseau qu'elle
va trier. Lorsque le tri est terminé, la goroutine principale doit imprimer toute la liste triée.</p>
```go
package main

  

import (

    "fmt"

    "sort"

    "strconv"

    "strings"

    "sync"

)

  

func main() {

    fmt.Println("Entrez une série d'entiers séparés par des , :")

    var input string

    fmt.Scanln(&input)

    numbers := parseInput(input)

  

    // Création de la WaitGroup pour synchroniser les goroutines

    var wg sync.WaitGroup

  

    // Diviser le tableau en 4 parties égales

    partitionSize := len(numbers) / 4

    partitions := make([][]int, 4)

  

    for i := 0; i < 4; i++ {

        start := i * partitionSize

        end := start + partitionSize

  

        if i == 3 { // La dernière partition inclut les éléments restants

            end = len(numbers)

        }

  

        partitions[i] = numbers[start:end]

  

        // Créer une goroutine pour trier chaque partition

        wg.Add(1)

        go func(partition []int) {

            defer wg.Done()

            sort.Ints(partition)

            fmt.Println("Partition triée :", partition)

        }(partitions[i])

    }

  

    // Attendez que toutes les goroutines de tri aient terminé

    wg.Wait()

  

    // Fusionner les partitions triées en un seul tableau trié

    sorted := merge(partitions)

  

    // Imprimer le tableau trié final

    fmt.Println("Tableau trié final :", sorted)

}

  

func parseInput(input string) []int {

    var numbers []int

    for _, str := range split(input) {

        num, err := strconv.Atoi(str)

        if err == nil {

            numbers = append(numbers, num)

        }

    }

    return numbers

}

  

func split(input string) []string {

    return strings.Split(input, ",")

}

  

func merge(arrays [][]int) []int {

    // Fusionnez les partitions triées en un seul tableau trié

    var merged []int

  

    for _, arr := range arrays {

        merged = mergeSorted(merged, arr)

    }

  

    return merged

}

  

func mergeSorted(arr1, arr2 []int) []int {

    // Fusionnez deux tableaux triés en un seul tableau trié

    merged := make([]int, 0, len(arr1)+len(arr2))

    i, j := 0, 0

  

    for i < len(arr1) && j < len(arr2) {

        if arr1[i] < arr2[j] {

            merged = append(merged, arr1[i])

            i++

        } else {

            merged = append(merged, arr2[j])

            j++

        }

    }

  

    // Ajoutez les éléments restants, s'il y en a

    merged = append(merged, arr1[i:]...)

    merged = append(merged, arr2[j:]...)

  

    return merged

}
```
<p>Mettez en ceuvre le probléme du philosophe au restaurant avec les contraintes/modifications suivantes. 1. Il doit y avoir 5 philosophes partageant des baguettes, avec une baguette entre chaque paire adjacente de philosophes. 2. Chaque philosophe ne doit manger que 3 fois (et non pas dans une boucle infinie comme nous l'avons fait en cours) 3. Les philosophes prennent les baguettes dans n'importe quel ordre, et non pas en commengant par le plus petit (comme nous l'avons fait en cours). 4, Pour manger, un philosophe doit obtenir la permission d'un héte qui s'exécute dans sa propre goroutine. 5. L'héte n'autorise pas plus de deux philosophes a manger en méme temps. 6. Chaque philosophe est numéroté de 14 5. 7. Lorsqu'un philosophe commence a4 manger (aprés avoir obtenu les verrous nécessaires), il imprime “starting to eat number" sur une ligne, ou number est le numéro du philosophe.</p>
```go
package main

import (
    "fmt"
    "sync"
)
const numPhilosophers = 5
const maxEating = 2
const numMeals = 3
var (

    philosophers   [numPhilosophers]int

    philosopherIDs [numPhilosophers]int

    mutexes        [numPhilosophers]sync.Mutex

    host           = make(chan struct{}, maxEating)

)
func main() {

    for i := 0; i < numPhilosophers; i++ {

        philosopherIDs[i] = i + 1

    }

  

    var wg sync.WaitGroup

    wg.Add(numPhilosophers)

  

    for i := 0; i < numPhilosophers; i++ {

        go dine(i, &wg)

    }

  

    wg.Wait()

}
func dine(philosopherID int, wg *sync.WaitGroup) {

    for meal := 1; meal <= numMeals; meal++ {

        think(philosopherID)

        eat(philosopherID)

    }

    wg.Done()

}
func think(philosopherID int) {

    fmt.Printf("Philosopher %d is thinking\n", philosopherID+1)

}
func eat(philosopherID int) {

    fmt.Printf("Philosopher %d is starting to eat\n", philosopherID+1)
    host <- struct{}{}

    mutex1 := &mutexes[philosopherID]

    mutex2 := &mutexes[(philosopherID+1)%numPhilosophers]
    mutex1.Lock()
    mutex2.Lock()
    philosophers[philosopherID]++
    fmt.Printf("Philosopher %d is eating (%d times)\n", philosopherID+1, philosophers[philosopherID])
    mutex1.Unlock()
    mutex2.Unlock()
    <-host
    fmt.Printf("Philosopher %d is done eating\n", philosopherID+1)
}
```