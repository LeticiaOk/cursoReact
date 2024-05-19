# `Entendendo o JSX:`

~~~~js
import './App.css';

function App() {
  const name = 'Matheus'

  const newName = name.toUpperCase()

  function sum(a, b){
    return a + b
  }

  const url = 'https://via.placeholder.com/150'

  return (
    <div className="App">
      <h2>Alterando o JSX</h2>
      <p>Olá, {newName}</p>
      <p> Soma: {sum(1, 2)}</p>
      <img src={url} alt="Minha imagem" />
    </div>
  );
}

export default App;
~~~~

# `Criando componentes no React:`

* Criar um 'arquivo.js' que geralmente fica em uma pasta chamada 'components'.

* Fazer a função e a exportação do arquivo.

* Fazer a importação do arquivo onde se quer utilizar.

* Componentes devem ser Inicializados com letra maíuscula.


## Arquivo de exportação (Frase.js):
~~~~js
function Frase(){ //Criando função para o componente
    return(
        <div> {/*Todo componente deve estar dentro de um container pai no caso <div>*/}
            <p>Este é um componente com uma frase!</p>
        </div>
    )
}

export default Frase // Exportando componente
~~~~


## Arquivo de importação (HelloWorld.js):
~~~~js
import Frase from "./Frase" //Importando componente
function HelloWorld(){

    return (
        <div>
            <h1>Meu primeiro componente</h1>
            <Frase/> / {/*Aplicando componente que foi importado*/}
        </div>
    )
}

export default HelloWorld
~~~~

# `Trabalhando com props:`

* Criar um 'arquivo.js' que geralmente fica em uma pasta chamada 'components'.

* Fazer a função e a exportação do arquivo.

* Fazer a importação do arquivo onde se quer utilizar.

* Componentes devem ser Inicializados com letra maíuscula.

## Arquivo de exportação (SaMyName.js):

~~~~js
function SayMyName(props){ // Passando props (propriedades) para a função.
    
    return(
        <div>
            <p> Fala aí {props.nome}, suave?</p> {/*Ultiziando o que foi passado para propriedade 'nome' e escrevendo na tela.*/}
        </div>
    )
}

export default SayMyName // exportando componente
~~~~


## Arquivo de importação (App.js):

~~~~js
import './App.css'
import SayMyName from './components/SayMyName' // Importando componente

function App() {
  const nome = "Maria"

  return (
    <div className="App">
      <SayMyName nome="Matheus"/>
      <SayMyName nome="João"/>
      <SayMyName nome={nome}/> {/*Passando valores para a propriedade 'nome'*/}
    </div>
  );
}

export default App;
~~~~

## Outra maneira de utilizar props:

### Arquivo de exportação (Pessoa.js):
~~~~js
function Pessoa({nome, idade, profissao, foto}){ // Passando propriedades específicas para a função.
    return(
        <div>
            <img src={foto} alt={nome}/> {/*Utilizando os valores passados para as propriedades e escrevendo na tela.*/}
            <h2>Nome: {nome}</h2>
            <p>Idade: {idade}</p>
            <p>Profissão: {profissao}</p>
        </div>
    )
}

export default Pessoa
~~~~

### Arquivo de importação (App.js):

~~~~js
import './App.css'
import Pessoa from './components/Pessoa'

function App() {

  return (
    <div className="App">
      <Pessoa nome="Rodrigo" idade="28" profissao="Programador" foto="https://via.placeholder.com/150" /> {/*Passando valores para as propriedades da função do componente*/}
    </div>
  );
}

export default App;
~~~~

# `Inserindo CSS no React (CSS modules):`

* O arquivo 'index.css' é onde fica os estilos globais

* Criar um 'arquivo.module.css' e adicionar os estilos.

* Importar o CSS no componente onde se quer usar.

* Importar o componente no arquivo onde se quer usar.


## CSS do componente (Frase.module.css):

* Não usar '-' no nome das classes, apenas camelCase e '_'.

~~~~css
.fraseContainer{
    background-color: #333;
    border: 1px solid #111;
}

.fraseContent{
    color: #fff;
    background-color: #333;
    margin: 0;
}
~~~~

## Componente onde vai ser importado o CSS (Frase.js):
~~~~js
import styles from './Frase.module.css'; // Importando CSS

function Frase(){
    return(
        <div className={styles.fraseContainer}> {/*Utilizando o CSS importado*/}
            <p className={styles.fraseContent}>Este é um componente com uma frase!</p>
        </div>
    )
}

export default Frase
~~~~

## Arquivo onde vai ser utilizado o componente estilizado (HelloWorld.js):

~~~~js
import Frase from "./Frase" // importando componente

function HelloWorld(){

    return (
        <div>
            <Frase/> {/*Utilizando componente*/}
            <h1>Meu primeiro componente</h1>
            <Frase/>
            <Frase/>
        </div>
    )
}

export default HelloWorld
~~~~

# `Utilizando React Fragments:`

* Fragments são utilizados para simplificar o código.

* São usados para armazenar os elementos filhos dentro de um container ao invés da tag 'div'.

## Componente (Item.js):

~~~~js
function Item(props){
    return(
        <> {/*Fragment*/}
            <li>{props.marca}</li>
        </>
    )
}

export default Item
~~~~

## Componente (List.js):
~~~~js
import Item from './Item'

function List(){
    return(
        <> {/*Fragment*/}
            <h1>Minha Lista</h1>
            <ul>
                <Item marca="Ferrai" />
                <Item marca="Fiat" />
                <Item marca="Renault" />
            </ul>
        </>
    )
}

export default List
~~~~

# `Avançando em props:`

* Importar a bibilioteca PropTypes.

## Compoennte (Item.js):
~~~~js
import PropTypes from 'prop-types' // importando biblioteca

function Item({marca, ano_lancamento}){
    return(
        <>
            <li>{marca} - {ano_lancamento}</li>
        </>
    )
}

Item.propTypes = { /*Utilizando bibilioteca*/
    marca: PropTypes.string.isRequired, /*A propriedade 'marca' deve ter o valor string e ser obrigatório*/
    ano_lancamento: PropTypes.number, /*A propriedade 'ano_lancamento' deve ser numérico*/
}

Item.defaultProps ={ /*Definindo valores padrão*/
    marca: 'Faltou a marca', /*O valor padrão apra a propriedade 'marca' será 'Faltou marca' caso não seja preenchida*/
    ano_lancamento: 0, /*Valor padrão '0' para a propriedade 'ano_lancamento'*/
}
export default Item
~~~~

## Componente (List.js):

* Atribuindo valores a propriedade 'item'.
~~~~js 
import Item from './Item' /*Exportando propriedade Item.js*/

function List(){
    return(
        <>
            <h1>Minha Lista</h1>
            <ul>
                <Item marca="Ferrai" ano_lancamento={1985} />
                <Item marca="Fiat" ano_lancamento={1964} />
                <Item marca="Renault" />
                <Item marca="Chevrolet" ano_lancamento={1999} />
                <Item />
            </ul>
        </>
    )
}

export default List
~~~~

# `Eventos no React (onClick, onChange e onSubmit):`

## Componente (Form.js)
~~~~js
function Form(){

    function cadastrarUsuario(e){ /*Função que ocorrerá quando o usuário clicar em 'Cadastrar'*/
        e.preventDefault() /*Para a execução do submit para que a página não recarregue e o evento ocorra*/
        console.log("Cadastrou o usuário!") /*Imprime a frase no console*/
    }

    return(
        <div>
            <h1>Meu cadastro:</h1>
            <form onSubmit={cadastrarUsuario}> {/*Chamando função pelo evento onSubmit quando o usuário clicar em 'Cadastrar no formulário'*/}
                <div>
                    <input type="text" placeholder="Digite o seu nome" />
                </div>
                <div>
                    <input type="submit" value="Cadastrar"></input>
                </div>
            </form>
        </div>
    )
}

export default Form
~~~~

## Componente (App.js)

~~~~js
import './App.css'
import Evento from './components/Evento'
import Form from './components/Form'; /*Importando o componente Form.js*/

function App() {

  return (
    <div className="App">
      <h1>Testando Eventos</h1>
      <Evento numero="1"/>
      <Evento numero="2"/>
      <Form /> {/*Chamando componente Form.js*/}
    </div>
  );
}

export default App;
~~~~

# `useState na prática:`

* O useState é um hook do React.
* Com ele conseguimos manuesear o estado de um componente de forma simples.
* Este hook funciona muito bem com evento.
* Podemos atrelar um evento a mudança do state.

## Componente (Form.js):

~~~~js
import {useState} from 'react' // importar a bibilioteca useState do React.

function Form(){

    function cadastrarUsuario(e){ // Chamando a função
        e.preventDefault()
        console.log(`Usuario ${name} foi cadastrado com a senha: ${password}`)
        console.log("Cadastrou o usuário!")
    }
    /*name: atribui o valor 'name' do formulario*/
    /*SetName: Resgata o valor */
    const[name, setName] = useState() // Atribuindo e passando os dados do formulário para o useState.
    // const[name, setName] = useState('Matheus') /*Atribui o valor 'Matheus diretamente no formulário'*/
    const[password, setpassword] = useState()

    return(
        <div>
            <h1>Meu cadastro:</h1>
            <form onSubmit={cadastrarUsuario}> {/*Chamando a função pelo evento 'onSubmit' quando o usuário clicar para enviar o formulário*/}
                <div>
                    <label htmlFor="name">Nome:</label>
                    <input type="text"
                        id="name"
                        name="name"
                        placeholder="Digite o seu nome" 
                        // value={name} /*Já atribui o valor name diretamente */
                        onChange={(e) => setName(e.target.value)}/> {/*Passando valor do formulario para o useState().*/}
                </div>
                <div>
                    <label htmlFor="password">Senha:</label>
                    <input
                     type="password" 
                     id="password" 
                     name="password" 
                     placeholder="Digite a sua senha" 
                     onChange={(e) => setpassword(e.target.value)}/>
                </div>
                <div>
                    <input type="submit" value="Cadastrar"></input>
                </div>
            </form>
        </div>
    )
}

export default Form
~~~~

## Componente (App.js):

~~~~js
import './App.css'
import Evento from './components/Evento'
import Form from './components/Form'; /*Importando componente For..js */

function App() {
  const nome = "Maria"

  return (
    <div className="App">
      <h1>Testando Eventos</h1>
      <Evento numero="1"/>
      <Evento numero="2"/>
      <Form /> {/*Chamando componente   */}
    </div>
  );
}

export default App;
~~~~

# `Métodos pro Props:`

* os métodos também podem ser passados por props.
* Ou seja, um componente filho pode ativar o método do seu ancestral
* Vamos acessar o método por meio de um evento.
* A sintaxe é a mesma de uma props de dados: props. meuEvento.

## Componente (Button.js):

~~~~js
function Button(props){ /*Passando props (propriedadas para a função)*/ 
    return <button onClick={props.event}>{props.text}</button> /*Retornando valores passados ao clicar no botão.*/
}

export default Button
~~~~

## Componente (Evento.js):

~~~~js
import Button from './evento/Button' /*Importando o componente Button.js*/

function Evento({numero}){
    function meuEvento(){ /*Função passada na propriedade 'event'*/
        console.log(`Ativando primeiro evento!`)
    }

    function segundoEvento(){ /*Função passada na propriedade 'event'*/
        console.log('Ativando o segundo evento!')
    }

    return(
        <div>
            <p>Clique para disparar um vento:</p>
            <Button event={meuEvento} text="Primeiro Evento"/> {/*Passando valores para as propriedas do componente Button.js*/}
            <Button event={segundoEvento} text="Segundo Evento"/>
        </div>
    )
}

export default Evento
~~~~

# `Renderização condicional (if):`

* Podemos atrelar a exeibição de algum elemento a um if.
* Esta ação é chamada de **Renderização condicional.**
* Envolvemos as tags em chaves {}.
* Como as chaves executam o JavaScript, criamos nossa condição
* É possível usar state para criar as condições

~~~~js
import {useState} from 'react' // Importando biblioteca

function Condicional(){
    const [email, setEmail] = useState() // Enviando dados do formulário para o useState
    const [userEmail, setUserEmail] = useState() // Enviando dados do formulário para o useState

    function enviarEmail(e){
        e.preventDefault()
        setUserEmail(email) // Atribuindo o 'email' ao 'setUserEmail'
    }
    function limparEmail(){
        setUserEmail('') // Limpa a mensagem
    }

    return(
        <div>
            <h2>Cadastre o seu e-mail:</h2>
            <form>
                <input type="email" placeholder="Digite o seu e-mail..." onChange={(e) => setEmail(e.target.value)}/>
                <button type='submit' onClick={enviarEmail}>Enviar-email</button>
                {userEmail &&( // Se a condição for verdadeira faz algo
                    <div>
                        <p>O e-mail do usuário é: {userEmail}</p> {/*Imprime na tela o parágrafo*/}
                        <button onClick={limparEmail}>Limpar e-mail</button> {/*Limpa o setUserEmail fazendo a condição ser falsa*/}
                    </div>
                )}
            </form>
        </div>
    )
}

export default Condicional
~~~~

# `Renderização de listas:`

* Para renderizar uma lista vamos primeiramente precisar de um array.
* Depois utilizamos a função map, para percorrer um dos itens.
* Podendo assim renderizar algo na tela.
* É possível unir operadores condicionais com a renderização de listas.