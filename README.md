# Calculadora com React

<h1 align="center">
    <img src="./calc.png" alt="Calculadora">
</h1>

Componentes permitem você dividir a UI em partes independentes, reutilizáveis e pensar em cada parte isoladamente. São como métodos em JavaScript que retornam elementos React e podem receber parâmetros chamados de `props` que descrevem o que deve aparecer na tela.

Existem dois principais tipos:

### Componentes de função

É a maneira mais simples de definir um componente:

```js
import React from 'react'

const FATECLab = props => {
    return <h1>Hello, {props.name}</h1>
}

export default FATECLab
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
