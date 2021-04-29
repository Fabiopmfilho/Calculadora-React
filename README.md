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

### Componentes de classe

Desta maneira você também pode renderizar uma [Classe ES6](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Classes). Classes tem alguns recursos adicionais que nós discutiremos nas próximas seções. Até lá, nós usaremos componentes de função por serem mais sucintos.


```js
import React from 'react'

class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>
    }
}

export default Welcome
```
