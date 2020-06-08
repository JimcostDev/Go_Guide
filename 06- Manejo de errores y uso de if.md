# Manejo de errores y uso de if


Para ver un error como el de un parseo de un string a un tipo de dato entero, se puede ver de la 
siguiente manera

```go
operador1, err1 := strconv.Atoi(valores[0])

fmt.Println(err1)
```


para el manejo de una condicional se puede utilizar el if :

```go
if err1 != nil && err2 != nil {
		// mostrar resultado
		fmt.Println(operador1 + operador2)	
	} else {
		fmt.Println("Op1 error : ",  err1)
		fmt.Println("Op2 error : ",  err2)
	}
```