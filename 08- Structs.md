# Structs

Los structs en go son colecciones de campos con tipos específicos. Son útiles para agrupar datos y formar registros.

Es muy parecido a las clases de otros lenguajes

```go
package main

import "fmt"

// El struct `persona` tiene los campos `nombre` y edad.
type persona struct {
    nombre string
    edad   int
}

func main() {

    // Esta sintaxis crea una instancia de un struct.
    fmt.Println(persona{"Bob", 20})

    // Puedes nombrear los campos cuando inicializas un struct.
    fmt.Println(persona{name: "Alice", age: 30})

    // Los campos omitidos serán de valor cero.
    fmt.Println(persona{name: "Fred"})

    // El prefijo `&` devuelve el apuntador a un struct.
    fmt.Println(&persona{name: "Ann", age: 40})

    // Puedes acceder a los campos del struct con un punto.
    s := person{name: "Sean", age: 50}
    fmt.Println(s.name)

    // También puedes usar puntos con apuntadores a struct -
    // los apuntadores son automáticamente dereferenciados.
    sp := &s
    fmt.Println(sp.age)

    // los Structs son inmutables.
    sp.age = 51
    fmt.Println(sp.age)
}
```


Otra funcionalidad que permiten los structs, es poder asignarle funciones
que haran parte de ese struct

```go
package main

import (
	"bufio"
	"fmt"
	"log"
	"os"
	"strconv"
	"strings"
)

type calc struct{}

// Asigna esta funcion al struct
func (calc) parseString(operator string) (int, error) {
	result, err := strconv.Atoi(operator)
	return result, err
}

func (c calc) operate(input string, operation string) (int, error) {
	cleanInput := strings.Split(input, operation)
	first, err := c.parseString(cleanInput[0])
	if err != nil {
		return 0, err
	}
	second, err := c.parseString(cleanInput[1])
	if err != nil {
		return 0, err
	}

	switch operation {
	case "+":
		return first + second, nil
	case "-":
		return first - second, nil
	case "*":
		return first * second, nil
	case "/":
		return first / second, nil
	default:
		log.Println(operation, "operation is not supported!")
		return 0, nil

	}

}

func main() {
	fmt.Println("Enter your input")
	input := readInput()
	fmt.Println("Enter your operation")
	operator := readInput()
	processResult(input, operator)

}

func readInput() string {
	scanner := bufio.NewScanner(os.Stdin)
	scanner.Scan()
	return scanner.Text()
}

func processResult(input string, operator string) {
	c := calc{}
	value, err := c.operate(input, operator)
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("Result of", input, "equals to", value)
	}
}

```