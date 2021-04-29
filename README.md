# Calculadora com React

<h1 align="center">
    <img src="/desafio4/public/calc.png" alt="Calculadora">
</h1>

Calculadora desenvolvida com React


### Selecionar Operação

Função para selecionar e executar a operação matemática:

```js
setOperation(operation) {
        if (this.state.current === 0) {
            this.setState({ operation, current: 1, clearDisplay: true })
        } else {
            const equals = operation === '='
            const currentOperation = this.state.operation
            const values = [...this.state.values]

            // try catch to decrease errors when calculating
            try {
                values[0] = eval(`${values[0]} ${currentOperation} ${values[1]}`)
            } catch (e) {
                values[0] = this.state.values[0]
            }

            values[1] = 0

            this.setState({
                displayValue: values[0],
                operation: equals ? null : operation,
                current: equals ? 0 : 1,
                clearDisplay: !equals,
                values
            })
        }
    }
```

### Enviar valores para o display

```js
addDigit(n) {
    if (n === '.' && this.state.displayValue.includes('.')) {
        return
    }

    const clearDisplay = this.state.displayValue === '0'
        || this.state.clearDisplay
    const currentValue = clearDisplay ? '' : this.state.displayValue
    const displayValue = currentValue + n
    this.setState({ displayValue, clearDisplay: false })

    if (n !== '.') {
        const i = this.state.current
        const newValue = parseFloat(displayValue)
        const values = [...this.state.values]
        values[i] = newValue
        this.setState({ values })
        console.log(values)
    }
}
```
