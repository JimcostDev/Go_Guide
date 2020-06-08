# Leer inputs desde la consola

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
)

func main() {
	// Crea una instancia de Scan de la terminal
	scanner := bufio.NewScanner(os.Stdin)

	// Iniciar scaner
	scanner.Scan()

	// Solicitar un input en la terminal
	// para este ejemplo sera 2+2
	operacion := scanner.Text()
	fmt.Println(operacion)
	valores := strings.Split(operacion, "+")
	fmt.Println(valores)
	// en este caso se concatena ya que los valores devueltos por el Split son de tipo String
	fmt.Println(valores[0] + valores[1])

	/* el simbolo de _ permite compilar el programa aun que la variable no este en uso ,
	ya que se debe compilar , exige que las variables si sean utilizadas */
	operador1, _ := strconv.Atoi(valores[0])
	operador2, _ := strconv.Atoi(valores[1])

	// mostrar resultado
	fmt.Println(operador1 + operador2)
}
```