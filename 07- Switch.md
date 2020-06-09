# Switch

```go 
scanner:= bufio.NewScanner(os.Stdin)
	scanner.Scan()
	operation := scanner.Text()
	//fmt.Println(operator)
	re := regexp.MustCompile("[^0-9]+")
	operatorr:= re.FindAllString(operation, -1)
	fmt.Println(operatorr)
	var operator string = strings.Join(operatorr,"")
	valores := strings.Split(operation,operator)
	num1,_ := strconv.Atoi(valores[0])
    num2,_ := strconv.Atoi(valores[1])
    
	switch operator{
        case "+": fmt.Println(num1+num2)
        case "-": fmt.Println(num1-num2)
        case "*": fmt.Println(num1*num2)
        case "/": fmt.Println(num1/num2)
        default: fmt.Println("operacion no valida")
	}

```