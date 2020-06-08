# Analizando un programa Go

```go
// Esta es la forma de implementar y distribuir codigo reutilizable
package main // Nombre del paquete

import "fmt" // Importar librerias necesarias para ejecutar el programa

// Este es el punto de inicio de la aplicación
func main() {
    // Go permite declarar variables de dos formas

    // de manera explicita
    var mensaje string = "Hola Mundo"

    // de manera implicta 
    mensajeFacil := "Hola mundo 2"
    
    // Imprimir por consola
    fmt.Println(mensaje)
    fmt.Println(mensajeFacil)

    // Tipo numerico de punto flotante implicito
    a := 10.

    // Tipo numerico de punto flotante explicito
    var b float64 = 3
    fmt.Println((a/b))

    // Tipo numerico entero explicito
    var c int = 10

    // Tipo numerico entero implicito
    d := 3
    fmt.Println(c/d)


    // Valor boolean implicito
    x := true
    // Valor boolean explicito
    var y  bool = false

    fmt.Println((x || y))
    fmt.Println(y && x)
    fmt.Println(!x)

    privada()
    Publica()
    imprimirHola()
}

// es privada si empieza con minuscula
func privada() {
    fmt.Println("Ejecutar logica que no necesita ser exportada")
}

// es publica si comienza con mayuscula
func Publica() {
    fmt.Println("Logica que se quiere exportar")
}


func imprimirHola() {
    // defer indica que se debe ejecutar al final de la funcion
    defer fmt.Prinln("Mundo")
    fmt.Println("Hola")
}
```

