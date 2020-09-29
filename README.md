# 04 - Básico dos Componentes

## Componentes e `props`

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

### Renderizando um Componente

Quando o React vê um elemento representando um componente definido pelo usuário, ele passa atributos [JSX](https://pt-br.reactjs.org/docs/introducing-jsx.html) para esse componente como um único objeto. Nós chamamos esse objeto de `props`.

```js
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>
}

const element = <Welcome name="ACCT" />

ReactDOM.render(
  element,
  document.getElementById('root')
)
```

#### [*Props são somente para leitura*](https://pt-br.reactjs.org/docs/components-and-props.html#props-are-read-only)

### Documentação e Exemplos

- [Componentes e Props](https://pt-br.reactjs.org/docs/components-and-props.html)
- [Compondo Componentes](https://pt-br.reactjs.org/docs/components-and-props.html#composing-components)
- [Extraindo Componentes](https://pt-br.reactjs.org/docs/components-and-props.html#extracting-components)

## Ciclo de Vida do Componente

Em aplicações com muitos componentes, é muito importante limpar os recursos utilizados pelos componentes quando eles são destruídos, para isso - e vários outros motivos - o ciclo de vida do componente existe.

Há um método que irá executar sempre que um componente é renderizado pela primeira vez, chamado de `mounting` no React - `componentDidMount`. E também um método que executa sempre que o componente é destruído, o HTML da página deixa de ter o conteúdo do componente, isso é chamado de `unmounting` no React - `componentWillUnmount`.

Além desses métodos, o [`constructor`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Classes#Construtor) também participa do ciclo de vida do componente, não explicitamente por causa do React, mas por causa das Classes em JavaScript.

```js
class Exemplo extends React.Component {
    constructor(props) {  
        super(props) // note que os "props" são passados para que o "constructor" envie-os para a classe que está a extendendo
        // ...
    }

    componentDidMount() {
        // ...
    }

    componentWillUnmount() {
        // ...
    }

    render() {
        // ...
    }
}
```

### Documentação e Exemplos

- [Métodos do Ciclo de Vida do componente](https://pt-br.reactjs.org/docs/react-component.html)
- [Convertendo uma Função para uma Classe](https://pt-br.reactjs.org/docs/state-and-lifecycle.html)
- [Herança em JavaScript](https://developer.mozilla.org/pt-BR/docs/Aprender/JavaScript/Objetos/Heran%C3%A7a)

## Estados do Componentes - `state`

Para você que estava se perguntando "como eu faço uma variável mudar quando uma ação acontecer na tela?", chegou a hora.

Estados ou `states` são variáveis, diferentes do `props` que **não pode ser alterado**, mutáveis do componente que vão definir literalmente o estado de algo. A exibição ou não de um elemento, o conteúdo de um elemento, um próprio elemento e etc.

Para criarmos um `state` é **obrigatório** que o componente seja uma classe ES6, pois a definição dele fica no `constructor`. 

```js
class Exemplo extends React.Component {
    constructor(props) {  
        super(props)
        
        this.state = {
            showButton: false,          // Boolean
            category: 'Smartphones',    // String
            price: 1499.99,             // Float
            product: {                  // Object
                name: 'Samsung S10'
            }
        }
    }

    // ...
}
```

Para alterar o `state` não basta fazer apenas:

```js
this.state.showButton = true
```

Pois para o estado mudar de verdade é necessário que o método `render()` rode de novo, assim o novo estado seria interpretado. Para alterar o valor de `showButton` é necessário:

```js
this.setState({ showButton: true })
```

O método `setState` irá realizar toda a rotina do componente, pois *há métodos do ciclo de vida do componente que são executados ao utilizar o esse método*.

Caso o componente que voce for criar **NÃO** utilize algum dos métodos de ciclo de vida do componente ou não faça uso do `state`, crie ele como função. Isso irá melhorar performaticamente a página e seus componentes.

### Documentação e Exemplos

- [Estado e Ciclo de Vida](https://pt-br.reactjs.org/docs/state-and-lifecycle.html)
- [States Components](https://reactjs.org/docs/faq-state.html)
- [Ententendo os Fundamentos do State em React](https://medium.com/the-andela-way/understanding-the-fundamentals-of-state-in-react-79c711be677f)

## Manipulando Eventos

Manipular eventos em elementos React é muito semelhante a manipular eventos em elementos HTML. Existem algumas diferenças sintáticas:

- Eventos em React são nomeados usando camelCase ao invés de letras minúsculas. - `onClick`
- Com o JSX você passa uma função como manipulador de eventos ao invés de um texto. - `<button onClick={() => alert('Clicado!')}`

Outra diferença é que você não pode retornar `false` para evitar o comportamento padrão no React (mais afetado em `<form>`). Você deve chamar `preventDefault` explícitamente. Por exemplo, com HTML simples, para evitar que um link abra uma nova página, você pode escrever:

``` html
<a href="#" onclick="console.log('O link foi clicado.'); return false">
    Clique Aqui
</a>
```

No React, isso poderia ser:

```js
function ActionLink() {
    function handleClick(event) {
        event.preventDefault();
        console.log('O link foi clicado.');
    }

    return (
        <a href="#" onClick={handleClick}>
            Clique Aqui
        </a>
    );
}
```

Aqui `event` é um "synthetic event". O React define esses eventos sintéticos de acordo com a especificação W3C. Então, não precisamos nos preocupar com a compatibilidade entre navegadores. Veja a página [`SyntheticEvent`](https://pt-br.reactjs.org/docs/events.html) para saber mais.

Ao usar o React você *geralmente* não precisa chamar `addEventListener` para adicionar manipuladores de eventos a um elemento no DOM depois que ele é criado. Ao invés disso você pode apenas definir um ouvinte quando o elemento é inicialmente renderizado.

### Passando Argumentos para Manipuladores de Eventos

É comum querermos passar parâmetros para métodos, o ID de algum registro, um texto que foi digitado em um input. Para isso temos esses dois exemplos:

```js
<button onClick={(e) => this.deleteRow(id, e)}>Deletar linha</button>
<button onClick={this.deleteRow.bind(this, id)}>Deletar linha</button>
```

**Importante:** Em ambos os casos, o argumento e representando o evento do React será passado como segundo argumento após o ID. Com uma arrow function, nós temos que passá-lo explicitamente. Mas com o bind outros argumentos adicionais serão automaticamente encaminhados.

## Renderização condicional

Em React, você pode criar componentes distintos que possuem o comportamento que você precisa. Então, você pode renderizar apenas alguns dos elementos, dependendo do estado da sua aplicação.

Renderização condicional em React funciona da mesma forma que condições funcionam em JavaScript. Use `if` ou um operador lógico (`||` ou `&&`) para criar elementos representando o estado atual, e deixe o React atualizar interface para corresponde-los.

```js
function ToggleOn(props) {
  return <p>ON</p>
}

function ToggleOff(props) {
  return <p>OFF</p>
}

class Toggle extends React.Component {
    constructor(props) {
        super(props)

        this.state = {
            isOn: false
        }
    }

    handleClick() {
        this.setState({
            isOn: !this.state.isOn
        })
    }

    render() {
        return (
            <div>
                <h1 onClick={this.handleClick.bind(this)}>Toggle</h1>
                {this.state.isOn ? (
                    <ToggleOn />
                ) : (
                    <ToggleOff />
                )}
            </div>
        )
    }
}

```

Esse exemplo faz uso do [Operador Condicional Ternário](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Operador_Condicional), entenda mais na documentação.

# Desafio
Neste desafio vocês deverão criar uma calculadora, contendo:

- Um componente de função chamado `<Button>`, este deve receber via props o valor do botão.
- **Se achar necessário** crie um componente `<ButtonOperator>` para diferenciar dos botões comuns.
- Um componente de classe chamado `<Input>`, que:
  - Recebe via `props` o valor digitado.
  - Trata o valor digitado para fazer o cálculo (guarde os valores no `state`).
- A calculadora deve pelo menos fazer uma soma e subtração.

Se sentir necessidade de modificar essa estrutura pode fazer, mas os componentes descritos acima DEVEM existir.

#### Inicialização:
- De um [Fork](https://docs.gitlab.com/ee/gitlab-basics/fork-project.html) no repositório: https://gitlab.com/acct.fateclab/turma-1-sem-2020/04-basico-dos-componentes;
- Agora você deve clonar o repositório localmente, há um botão azul "Clone" no seu repositório do GitLab, clique nele e use a URL com **HTTPS**. 
- Agora localmente abra uma pasta e use o botão direito do Mouse para abrir o "Git Bash", com esse atalho você chegará na pasta que quer mais rapidamente pelo terminal.
- Use o comando `git clone url-copiada-do-gitlab` para que a estrutura de pastas do repositório seja clonada na sua pasta
- Utilize o comando `create-react-app` para criar o projeto.

#### Entrega:
- Assim que terminar dê `git push origin seu-nome/basico-dos-componentes`
- Acesse o menu "Merge Requests", configure o "Target Branch" para o [repositório original](https://gitlab.com/acct.fateclab/dev-turma-2-sem-2020/04-basico-dos-componentes) para que seu App seja avaliado e revisado e para que possamos te dar um feedback.
- O nome do Merge Request deve ser o seu nome completo.
- Crie o Merge Request.

#### Para se destacar:
- Faça também as operações de multiplicação e divisão
- Faça com que possa ser feito vários cálculos na mesma digitação, ex. Digitado: `1 + 2 * 2`, Resultado: `5`
- Crie uma branch `seu-nome/basico-dos-componentes` no seu repositório.
- Personalize o app com CSS.
- Se preocupe com a visualização no celular.
- Organize melhor suas pastas e arquivos:
  - Utilize os nomes dos componentes que criar como o nome dos arquivos.
  - Crie uma pasta `components` dentro do `src` para colocar todos os componentes secundarios como o Button.