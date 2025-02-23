# Effect, Reducers e Context

Os **Effects** são um conceito fundamental no **React**, especialmente no **React Hooks**, representados pelo **useEffect**. Eles permitem executar efeitos colaterais em componentes funcionais, como chamadas a APIs, manipulação do DOM, assinaturas de eventos e muito mais.

---

### 📌 **O que são Effects?**
Os **Effects** são usados para lidar com efeitos colaterais em componentes React, ou seja, operações que afetam algo fora do escopo do componente, como:
- Buscar dados de uma API.
- Assinar e limpar eventos.
- Manipular o DOM diretamente.

No React **antes dos hooks**, esses efeitos colaterais eram gerenciados nos métodos de ciclo de vida de componentes de classe, como `componentDidMount`, `componentDidUpdate` e `componentWillUnmount`.

Agora, com **useEffect**, é possível gerenciar efeitos em **componentes funcionais**.

---

### 📌 **Definindo um Effect**
Um **Effect** é definido usando o **hook useEffect**, que aceita dois argumentos:
1. **Uma função de efeito** – O código que será executado.
2. **Um array de dependências (opcional)** – Define quando o efeito deve ser reexecutado.

```jsx
import { useEffect } from "react";

function MeuComponente() {
  useEffect(() => {
    console.log("O componente foi montado!");

    return () => {
      console.log("O componente foi desmontado!");
    };
  }, []);

  return <h1>Olá, mundo!</h1>;
}
```

🔹 **Explicação**:
- O `useEffect` executa a função quando o componente é montado.
- O retorno da função (`return () => {}`) é executado quando o componente é desmontado.

---

### 📌 **Usando o Effect da forma correta**
Para usar `useEffect` corretamente, siga estas boas práticas:

1. **Use dependências corretamente**:  
   - Se o array de dependências estiver **vazio (`[]`)**, o efeito será executado **apenas uma vez** (semelhante ao `componentDidMount`).
   - Se não for passado nenhum array de dependências, ele será executado **a cada renderização**.
   - Se houver **dependências no array**, o efeito será reexecutado **sempre que uma delas mudar**.

```jsx
useEffect(() => {
  console.log("Efeito executado sempre que `count` mudar!");
}, [count]);
```

2. **Evite dependências desnecessárias**:  
   - Dependências excessivas podem fazer o efeito ser executado mais vezes do que o necessário.
   - Omitir dependências pode causar bugs (efeitos rodando com valores antigos).

3. **Sempre limpe assinaturas/eventos**:  
   - Se o efeito criar um **listener**, **intervalo** ou **timer**, remova-os ao desmontar.

```jsx
useEffect(() => {
  const interval = setInterval(() => {
    console.log("Intervalo rodando...");
  }, 1000);

  return () => clearInterval(interval);
}, []);
```

---

### 📌 **Exemplo real do Effect**
Vamos criar um componente que busca dados de uma API usando `fetch` e exibe uma lista:

```jsx
import { useEffect, useState } from "react";

function ListaUsuarios() {
  const [usuarios, setUsuarios] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => setUsuarios(data))
      .catch((error) => console.error("Erro ao buscar usuários:", error));
  }, []);

  return (
    <div>
      <h2>Lista de Usuários</h2>
      <ul>
        {usuarios.map((usuario) => (
          <li key={usuario.id}>{usuario.name}</li>
        ))}
      </ul>
    </div>
  );
}

export default ListaUsuarios;
```

🔹 **O que acontece nesse código?**  
- O `useEffect` faz uma requisição **apenas uma vez** ao montar o componente.
- Os dados são armazenados no estado `usuarios` e renderizados em uma lista.
- Como o array de dependências está **vazio (`[]`)**, o efeito não roda novamente.

---

### 📌 **Resumo**
✅ `useEffect` permite lidar com efeitos colaterais em componentes funcionais.  
✅ Ele pode ser disparado **uma única vez**, **a cada renderização**, ou **sempre que uma dependência mudar**.  
✅ Sempre limpe efeitos que envolvam assinaturas de eventos ou timers para evitar vazamento de memória.  
✅ É ideal para **requisições assíncronas**, **manipulação do DOM** e **integrações externas**.

---

## 📌 Usando o **CleanUp** no `useEffect`
O **clean-up** em um `useEffect` serve para evitar vazamentos de memória ao desmontar o componente. Ele é especialmente útil para:
- Cancelar **timers**
- Remover **event listeners**
- Cancelar **requisições** pendentes

**Exemplo prático com `setInterval` e limpeza:**
```javascript
import { useEffect, useState } from "react";

function Contador() {
  const [contador, setContador] = useState(0);

  useEffect(() => {
    const intervalo = setInterval(() => {
      setContador((prev) => prev + 1);
    }, 1000);

    return () => clearInterval(intervalo); // Cleanup ao desmontar o componente
  }, []);

  return <h1>Contador: {contador}</h1>;
}
```
✅ O **`clearInterval(intervalo)`** impede que o timer continue rodando depois que o componente for desmontado.

---

## 🚀 O que são **Reducers**?
No React, um **reducer** é uma função pura que gerencia o estado de um componente de maneira previsível. Ele recebe:
1. **O estado atual**
2. **Uma ação** que define qual mudança deve ser feita

E retorna:
- **O novo estado atualizado** 🎯

É uma alternativa ao `useState`, útil para **lógica complexa** e **múltiplas atualizações de estado**.

### 🛠 Criando um **Reducer 1** - Contador simples
```javascript
import { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return initialState;
    default:
      throw new Error("Ação desconhecida");
  }
}

function Contador() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Contador: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "reset" })}>Resetar</button>
    </div>
  );
}

export default Contador;
```
✅ O `dispatch({ type: "increment" })` aciona a ação dentro do reducer.

---

### 🛠 Criando um **Reducer 2** - Gerenciando uma lista de tarefas
```javascript
import { useReducer } from "react";

const initialState = [];

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return [...state, { id: Date.now(), text: action.payload, done: false }];
    case "remove":
      return state.filter((task) => task.id !== action.payload);
    case "toggle":
      return state.map((task) =>
        task.id === action.payload ? { ...task, done: !task.done } : task
      );
    default:
      return state;
  }
}

function ListaDeTarefas() {
  const [tasks, dispatch] = useReducer(reducer, initialState);
  const addTask = () => {
    const text = prompt("Nova tarefa:");
    if (text) dispatch({ type: "add", payload: text });
  };

  return (
    <div>
      <button onClick={addTask}>Adicionar Tarefa</button>
      <ul>
        {tasks.map((task) => (
          <li
            key={task.id}
            onClick={() => dispatch({ type: "toggle", payload: task.id })}
            style={{ textDecoration: task.done ? "line-through" : "none" }}
          >
            {task.text}
            <button onClick={() => dispatch({ type: "remove", payload: task.id })}>
              ❌
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ListaDeTarefas;
```
✅ O reducer agora gerencia uma **lista de tarefas** com ações de adicionar, remover e alternar status.

---

## 🎯 Usando o **Reducer 1** - Estado com múltiplas mudanças
Se tivermos vários `useState`, podemos simplificá-los com `useReducer` para maior clareza.

```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```
O `dispatch` permite disparar diferentes ações sem necessidade de vários `useState`.

---

## 🎯 Usando o **Reducer 2** - Formulários complexos
Para um formulário, podemos armazenar múltiplos campos com um único `useReducer`.

```javascript
import { useReducer } from "react";

const initialState = { nome: "", email: "", senha: "" };

function reducer(state, action) {
  return { ...state, [action.field]: action.value };
}

function Formulario() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <form>
      <input
        type="text"
        placeholder="Nome"
        value={state.nome}
        onChange={(e) => dispatch({ field: "nome", value: e.target.value })}
      />
      <input
        type="email"
        placeholder="Email"
        value={state.email}
        onChange={(e) => dispatch({ field: "email", value: e.target.value })}
      />
      <input
        type="password"
        placeholder="Senha"
        value={state.senha}
        onChange={(e) => dispatch({ field: "senha", value: e.target.value })}
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```
✅ Aqui, **qualquer campo modificado** dispara o `dispatch` e atualiza o estado correto.

---

## 🎯 Usando o **Reducer 3** - Comunicação entre componentes
Podemos compartilhar um estado global com `useReducer` e `Context API`.

1️⃣ **Criando o contexto do estado global**
```javascript
import { createContext, useReducer } from "react";

const AppContext = createContext();

const initialState = { theme: "light" };

function reducer(state, action) {
  switch (action.type) {
    case "toggleTheme":
      return { theme: state.theme === "light" ? "dark" : "light" };
    default:
      return state;
  }
}

export function AppProvider({ children }) {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <AppContext.Provider value={{ state, dispatch }}>
      {children}
    </AppContext.Provider>
  );
}

export default AppContext;
```

2️⃣ **Usando o contexto em componentes**
```javascript
import { useContext } from "react";
import AppContext from "./AppContext";

function ThemeButton() {
  const { state, dispatch } = useContext(AppContext);

  return (
    <button onClick={() => dispatch({ type: "toggleTheme" })}>
      Mudar para {state.theme === "light" ? "dark" : "light"}
    </button>
  );
}

export default ThemeButton;
```
✅ Aqui, `useReducer` trabalha junto com **Context API**, tornando o estado **compartilhado entre componentes**.

---

### 🚀 Conclusão
- `useEffect` → Executa efeitos colaterais e usa `clean-up` para evitar vazamentos.
- `useReducer` → Ótimo para gerenciar **estados complexos** com **múltiplas ações**.
- `dispatch` → Permite disparar ações para modificar o estado.
- `useReducer + Context` → Ajuda a **compartilhar estado global**.
