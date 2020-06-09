# Punteros

ref: https://ed.team/blog/que-son-los-punteros-en-go

Un puntero en Go es una variable que nos permite acceder a la dirección en memoria de otra variable.

## Para que sirven los punteros ?

Los punteros son muy útiles en los casos en los que queremos pasar una variable como argumento a una función para que su valor sea modificado, lo que se conoce como pasar valores por referencia a una función.

Cuando creamos una función y le pasamos una variable como argumento, lo que hace la función es hacer una copia del valor de la variable y trabajar con ese valor, por lo que la variable que pasamos como argumento no se modifica.


Veamos un ejemplo para entender esta situación.

```go
package main

import (
	"fmt"
)

func Increase(v int) {
	v++
}

func main() {
	var v int = 19
	Increase(v)
	fmt.Println("El valor de v es:", v)	
}
```

Este código produce el siguiente resultado.

        El valor de v es: 19


Podemos ver entonces que el valor de la variable v no se incrementa y sigue siendo 19, ya que la función Increase hace una copia de la variable v y realiza el incremento sobre la copia y no sobre la variable.

A continuación veremos algunos conceptos que debemos entender para trabajar con punteros, y al finalizar refactorizaremos el código anterior para lograr incrementar el valor de la variable "v".


## ¿Cómo creamos un puntero?

Como Go es un lenguaje estáticamente tipado las variables puntero tienen que ser de un tipo de dato especifico.

Para crear un puntero utilizamos el operador \* antes del tipo de dato que necesitamos almacenar en esa dirección de memoria.

```go
    var p *int
```


Adicionalmente, Go nos proporciona dos formas más para crear punteros:

- Mediante la función new() que recibe como argumento un tipo de dato.
- Y a través del del short hand de declaración de variables :=.

A continuación veremos un ejemplo de su uso:

```go
package main

import (
	"fmt"
)

func main() {
	v := 19
	
	var p1 *int
	var p2 = new(int)
	p3 := &v 
	
	// %T nos permite imprimir el tipo de dato de la variable
	fmt.Printf("p1: %T \n", p1)
	fmt.Printf("p2: %T \n", p2)
	fmt.Printf("p3: %T \n", p3)	
}
```

Este código produce el siguiente resultado.

    p1: *int 
    p2: *int 
    p3: *int

Podemos ver entonces que el tipo de dato de las variables p1, p2 y p3 es un puntero de tipo entero \*int.

## El operador de dirección &

Para obtener la referencia o dirección de memoria de una variable, debemos anteponer a la variable el operador de dirección &.

Veamos un ejemplo:

```go
package main

import (
	"fmt"
)

func main() {
	var v int = 19
	fmt.Println("La dirección de memoria de v es: ", &v)	
}
```

Este código produce el siguiente resultado.

        La dirección de memoria de v es:  0x10414020


En este ejemplo, podemos ver que la variable "v" de tipo entero tiene el valor 19 y se almacena en la dirección de memoria 0x10414020.


## El operador de desreferenciación *

Desreferenciar un puntero es obtener el valor que esta almacenado en la dirección de memoria a donde hace referencia el puntero, para hacerlo debemos anteponer el operador \* a la variable puntero.

Veamos un ejemplo:

```go
package main

import (
	"fmt"
)

func main() {
	var v int = 19
	var p *int
	
	// Hacemos que el puntero p, referencie la dirección
	// de memoria de la variable v.
	p = &v
	
	fmt.Printf("La variable v es: %d \n", v)
	fmt.Printf("La dirección de memoria de v es: %v \n", &v)
	fmt.Printf("El puntero p referencia a la dirección de memoria: %v \n", p)
	fmt.Printf("Al desrefenciar el puntero p obtengo el valor: %d \n", *p) 
}
```

Este código produce el siguiente resultado.

        La variable v es: 19 
        La dirección de memoria de v es: 0x10414020 
        El puntero p referencia a la dirección de memoria: 0x10414020 
        Al desrefenciar el puntero p obtengo el valor: 19


Podemos ver que el puntero p referencia a la dirección de memoria 0x10414020 , y para obtener el valor 19 almacenado en esta dirección, hacemos uso del operador de desreferenciación \*p.


## Incrementemos la variable "v"

Refactoricemos la función Increase con el uso de punteros:

```go
package main

import (
	"fmt"
)

// Increase recibe un puntero de tipo entero
func Increase(v *int) {
	// Desreferenciamos la variable v para obtener
	// su valor e incrementarlo en 1
	*v++
}

func main() {
	var v int = 19
	
	// La función Increase recibe un puntero
	// utilizamos el operador de dirección &
	// para pasar la dirección de memoria de v
	Increase(&v)
	
	fmt.Println("El valor de v ahora vale:", v)
}
```

Este código produce el siguiente resultado.

    El valor de v ahora vale: 20 


## Y, ¿Cómo utilizo punteros en estructuras?

El uso de punteros en estructuras maneja los mismos conceptos que hemos aprendido, veamos su aplicación a través del siguiente ejemplo:

Crearemos una estructura llamada User y utilizaremos una función llamada UpdateStatus para actualizar el estado del usuario, así que esta función recibirá un puntero de tipo User y actualizará el campo IsActive.

Veamos el código:

```go
package main

import (
	"fmt"
)

type User struct {
	FirstName string
	LastName  string
	Email     string
	IsActive  bool
}

func UpdateStatus(u *User) {
	(*u).IsActive = !(*u).IsActive
}

func main() {

	u := User{
		FirstName: "Alejandro",
		LastName:  "Rodríguez",
		Email:     "aj@ed.team",
		IsActive:  false,
	}
	
	fmt.Println("User antes de actualización: ", u)
	
	UpdateStatus(&u)
	
	fmt.Println("User después de actualización: ", u)	
}
```

Este código produce el siguiente resultado.

        User antes de actualización:  {Alejandro Rodríguez aj@ed.team false}
        User después de actualización:  {Alejandro Rodríguez aj@ed.team true}


La función UpdateStatus recibe un puntero de tipo User, lo que nos permite acceder a la dirección de memoria en donde se encuentra almacenada la estructura, para modificar el valor del campo IsActive desreferenciamos el puntero con (\*u).IsActive y le asignamos el mismo valor con el operador de negación !, así invertimos el estado del usuario.

Cuando estamos trabajando con punteros de estructura, Go nos permite trabajar sin el operador de desreferenciación \*, con esto logramos una sintaxis más limpia, así que la función anterior podríamos refactorizarla como:

```go
func UpdateStatus(u *User) {
	u.IsActive = !u.IsActive
}
```

