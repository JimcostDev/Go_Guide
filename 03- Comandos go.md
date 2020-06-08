# Comandos basicos de Go

1. Crea un archivo main.go con el siguiente contenido

```go
package main

import "fmt"

func main()  {
	fmt.Println("Hello !!")
}
```

2. para ejecutar dicha funcion primero se debe compilar el archivo , para ello se ejecuta el comando:

        go build main.go

este creara un ejecutable del archivo.


3. para ejecutar el archivo y que inmeditamente lo ejecute , se utiliza el comando :

        go run main.go


Este crea el ejecutable y luego que se ejecuta lo elimina.