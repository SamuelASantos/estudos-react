## 📝 **Estados e Eventos**:
  

### **#1: Adicionando evento de clique**
📌 **Descrição**:  
Nesta aula, aprendemos como adicionar eventos de clique (`onClick`) em elementos do React. A abordagem principal foi usar a sintaxe JSX para associar uma função ao evento.

🚀 **Exemplo**:
```jsx
function Botao() {
  function handleClick() {
    alert("Botão clicado!");
  }

  return <button onClick={handleClick}>Clique aqui</button>;
}
```
🔎 **Pontos Importantes**:
- Os eventos em React são baseados em SyntheticEvent, uma camada sobre os eventos nativos do JavaScript.
- O manipulador de eventos deve ser passado como uma função (sem parênteses).

---

### **#2: Forma errada de passar eventos**
📌 **Descrição**:  
Aqui identificamos formas incorretas de passar eventos em React, que podem levar a reexecução indesejada da função ou a problemas de performance.

❌ **Exemplo errado**:
```jsx
<button onClick={handleClick()}>Clique aqui</button>
```
🚨 **Por que está errado?**  
- `handleClick()` está sendo chamado **imediatamente**, ao invés de ser passado como referência para ser executado no clique.

✅ **Forma correta**:
```jsx
<button onClick={handleClick}>Clique aqui</button>
```

---

### **#3: Passando eventos via props**
📌 **Descrição**:  
Esta aula aborda como **passar eventos via props** para tornar componentes mais reutilizáveis.

🚀 **Exemplo**:
```jsx
function Botao({ aoClicar }) {
  return <button onClick={aoClicar}>Clique aqui</button>;
}

function App() {
  function handleBotaoClick() {
    alert("Botão no App foi clicado!");
  }

  return <Botao aoClicar={handleBotaoClick} />;
}
```
🔎 **Pontos Importantes**:
- Permite que componentes filhos disparem eventos que são tratados pelos pais.
- Melhora a reusabilidade e desacopla componentes.

---

### **#4: Usando o preventDefault**
📌 **Descrição**:  
Aprendemos a utilizar o método `preventDefault()` para impedir comportamentos padrão de eventos, como o recarregamento da página ao submeter um formulário.

🚀 **Exemplo**:
```jsx
function Formulario() {
  function handleSubmit(event) {
    event.preventDefault();
    alert("Formulário enviado!");
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Enviar</button>
    </form>
  );
}
```
🔎 **Pontos Importantes**:
- `preventDefault()` evita ações padrão do navegador em eventos.
- Útil em formulários, links e outras interações.

---

### **#5: O que é um State?**
📌 **Descrição**:  
O **State** no React é uma estrutura que permite armazenar e manipular dados dentro de um componente, tornando a interface dinâmica.

🚀 **Exemplo**:
```jsx
import { useState } from "react";

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>
    </div>
  );
}
```
🔎 **Pontos Importantes**:
- `useState` cria e gerencia estados dentro de componentes funcionais.
- Atualizar o **State** causa re-renderização do componente.

---

### **#6: Trabalhando com States**
📌 **Descrição**:  
Exploramos como modificar **States** corretamente e entender como as mudanças impactam a renderização do React.

🚀 **Exemplo**:
```jsx
function Toggle() {
  const [ligado, setLigado] = useState(false);

  return (
    <button onClick={() => setLigado(!ligado)}>
      {ligado ? "Desligar" : "Ligar"}
    </button>
  );
}
```
🔎 **Pontos Importantes**:
- **States** nunca devem ser modificados diretamente (`state = novoValor` ❌).
- Devemos sempre usar a função `setState` para garantir a reatividade do React.

---

### **#7: Usando states para auxiliar UI**
📌 **Descrição**:  
Os **States** são essenciais para criar **interfaces dinâmicas**, como modais, notificações e animações baseadas no estado.

🚀 **Exemplo**:
```jsx
function Modal() {
  const [visivel, setVisivel] = useState(false);

  return (
    <div>
      <button onClick={() => setVisivel(!visivel)}>
        {visivel ? "Fechar" : "Abrir"} Modal
      </button>
      {visivel && <p>Este é um modal</p>}
    </div>
  );
}
```
🔎 **Pontos Importantes**:
- Estados podem **exibir ou ocultar elementos** na interface.
- Evitam manipulação direta do DOM, tornando o código mais limpo.

---

### **#8: Usando states em campos**
📌 **Descrição**:  
Aprendemos a usar o **State** para gerenciar campos de entrada (`input`), tornando-os controlados.

🚀 **Exemplo**:
```jsx
function Formulario() {
  const [nome, setNome] = useState("");

  return (
    <input 
      type="text" 
      value={nome} 
      onChange={(e) => setNome(e.target.value)} 
    />
  );
}
```
🔎 **Pontos Importantes**:
- **Campos controlados** garantem que os valores sempre estejam sincronizados com o **State**.
- `onChange` atualiza o **State** conforme o usuário digita.

---

### **#9: States mudando no tempo**
📌 **Descrição**:  
Exploramos como os **States** podem mudar ao longo do tempo com **efeitos assíncronos**.

🚀 **Exemplo**:
```jsx
function Relogio() {
  const [hora, setHora] = useState(new Date().toLocaleTimeString());

  useEffect(() => {
    const intervalo = setInterval(() => {
      setHora(new Date().toLocaleTimeString());
    }, 1000);

    return () => clearInterval(intervalo);
  }, []);

  return <p>Hora atual: {hora}</p>;
}
```
🔎 **Pontos Importantes**:
- `setInterval` é usado para atualizar o **State** a cada segundo.
- **Necessário limpar efeitos colaterais** usando `clearInterval`.

---

### **#10: State Updater**
📌 **Descrição**:  
O **State Updater** é uma técnica que usa funções dentro do `setState` para garantir atualizações seguras.

🚀 **Exemplo**:
```jsx
function ContadorSeguro() {
  const [contador, setContador] = useState(0);

  function incrementar() {
    setContador((prevContador) => prevContador + 1);
  }

  return <button onClick={incrementar}>Contador: {contador}</button>;
}
```
🔎 **Pontos Importantes**:
- O **State Updater** recebe o valor anterior (`prevState`) e retorna o novo valor.
- Evita problemas de concorrência em múltiplas atualizações.

---

### **#11: Atualizando Objetos em States**  
📌 **Descrição**:  
Aprendemos a atualizar objetos dentro de um **State** no React, garantindo que a modificação ocorra corretamente sem mutar o estado diretamente.  

🚀 **Exemplo**:  
```jsx
function Usuario() {
  const [usuario, setUsuario] = useState({ nome: "Alice", idade: 25 });

  function atualizarIdade() {
    setUsuario((prevUsuario) => ({ ...prevUsuario, idade: prevUsuario.idade + 1 }));
  }

  return (
    <div>
      <p>Nome: {usuario.nome}</p>
      <p>Idade: {usuario.idade}</p>
      <button onClick={atualizarIdade}>Aumentar Idade</button>
    </div>
  );
}
```
🔎 **Pontos Importantes**:  
- **Nunca modificar o objeto diretamente** (`usuario.idade += 1` ❌).  
- Sempre usar **spread operator (`...`)** para manter os outros valores do objeto.  

---

### **Projeto ToDo**  
📌 **Descrição**:  
Criamos um **Projeto ToDo** para gerenciar tarefas utilizando um **array no State**.  

🚀 **Estrutura do Projeto**:  
```bash
📁 projeto-todo/
├── 📄 index.js
├── 📁 src/
│   ├── 📄 App.js
│   ├── 📄 TodoList.js
│   ├── 📄 TodoItem.js
│   ├── 📄 styles.css
└── 📄 README.md
```
🔎 **Pontos Importantes**:  
- Cada **tarefa é um objeto** com `id` e `texto`.  
- Manipulação do **State** para exibir, adicionar, excluir e alterar tarefas.  

---

### **Arrays em States: Exibir**  
📌 **Descrição**:  
Renderizamos um **array no State** utilizando `map()`.  

🚀 **Exemplo**:  
```jsx
function Lista() {
  const [itens, setItens] = useState(["Item 1", "Item 2", "Item 3"]);

  return (
    <ul>
      {itens.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}
```
🔎 **Pontos Importantes**:  
- **Cada item deve ter uma `key` única**.  
- `map()` percorre o **array do State** e gera elementos JSX.  

---

### **Arrays em States: Adicionar**  
📌 **Descrição**:  
Adicionamos novos itens ao **array do State** utilizando `setState`.  

🚀 **Exemplo**:  
```jsx
function Lista() {
  const [itens, setItens] = useState(["Item 1", "Item 2"]);

  function adicionarItem() {
    setItens((prevItens) => [...prevItens, `Item ${prevItens.length + 1}`]);
  }

  return (
    <div>
      <ul>
        {itens.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
      <button onClick={adicionarItem}>Adicionar Item</button>
    </div>
  );
}
```
🔎 **Pontos Importantes**:  
- **Não modificar o array diretamente** (`push() ❌`).  
- Criar um **novo array** com os itens antigos + novo item.  

---

### **Arrays em States: Excluir**  
📌 **Descrição**:  
Removemos um **item do array** utilizando `filter()`.  

🚀 **Exemplo**:  
```jsx
function Lista() {
  const [itens, setItens] = useState(["Item 1", "Item 2", "Item 3"]);

  function removerItem(index) {
    setItens((prevItens) => prevItens.filter((_, i) => i !== index));
  }

  return (
    <ul>
      {itens.map((item, index) => (
        <li key={index}>
          {item} <button onClick={() => removerItem(index)}>Remover</button>
        </li>
      ))}
    </ul>
  );
}
```
🔎 **Pontos Importantes**:  
- `filter()` cria um **novo array** excluindo o item desejado.  

---

### **Arrays em States: Alterar**  
📌 **Descrição**:  
Editamos um item dentro do **array do State** utilizando `map()`.  

🚀 **Exemplo**:  
```jsx
function Lista() {
  const [itens, setItens] = useState(["Item 1", "Item 2", "Item 3"]);

  function editarItem(index) {
    setItens((prevItens) =>
      prevItens.map((item, i) => (i === index ? `Item ${i + 1} (editado)` : item))
    );
  }

  return (
    <ul>
      {itens.map((item, index) => (
        <li key={index}>
          {item} <button onClick={() => editarItem(index)}>Editar</button>
        </li>
      ))}
    </ul>
  );
}
```
🔎 **Pontos Importantes**:  
- `map()` percorre o array e altera apenas o item desejado.  

---

### **Arrays em States: Usando ID**  
📌 **Descrição**:  
Usamos **IDs únicos** para gerenciar corretamente os itens da lista.  

🚀 **Exemplo**:  
```jsx
function Lista() {
  const [itens, setItens] = useState([
    { id: 1, nome: "Item 1" },
    { id: 2, nome: "Item 2" },
  ]);

  function removerItem(id) {
    setItens((prevItens) => prevItens.filter((item) => item.id !== id));
  }

  return (
    <ul>
      {itens.map((item) => (
        <li key={item.id}>
          {item.nome} <button onClick={() => removerItem(item.id)}>Remover</button>
        </li>
      ))}
    </ul>
  );
}
```
🔎 **Pontos Importantes**:  
- **Evita problemas ao excluir ou alterar itens no array**.  

---