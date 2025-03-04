## 🔹 O que é o `useReducer`?
O `useReducer` é um **gerenciador de estado baseado em "redução"**, um conceito popular em programação funcional. Ele é particularmente útil quando o estado do componente:
- Tem múltiplos valores (objetos, listas, etc.).
- É atualizado por diferentes ações.
- Precisa de **mais controle** sobre as atualizações.

### **📌 Sintaxe básica**
O `useReducer` recebe **dois parâmetros**:
1. Uma **função "reducer"**, que decide como o estado deve ser atualizado.
2. Um **estado inicial**.

E retorna um **array** com:
- O **estado atual**.
- A **função `dispatch`**, que envia ações para atualizar o estado.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

---

## 🔹 Exemplo 1: Contador com `useReducer`
Aqui está um exemplo básico de um **contador**, mas agora usando `useReducer`:

```jsx
import { useReducer } from "react";

// Função reducer para definir como o estado muda
const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return { count: 0 };
    default:
      return state;
  }
};

function Contador() {
  // Estado inicial
  const initialState = { count: 0 };

  // useReducer recebe o reducer e o estado inicial
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h2>Contador: {state.count}</h2>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </div>
  );
}

export default Contador;
```

---

### 🔍 **Explicação**
1. **`reducer`** → Define como o estado deve mudar com base na ação recebida.
2. **`initialState`** → O estado começa com `{ count: 0 }`.
3. **`useReducer(reducer, initialState)`** → Retorna o estado atual (`state`) e a função `dispatch`.
4. **`dispatch({ type: "increment" })`** → Dispara uma ação para modificar o estado.
5. O **estado é atualizado de forma previsível** com base na ação recebida.

---

## 🔹 Exemplo 2: Gerenciando uma Lista de Tarefas ✅
Agora, vamos usar `useReducer` para criar um sistema de **lista de tarefas** onde podemos adicionar, remover e marcar tarefas como concluídas.

### **📌 Código**
```jsx
import { useReducer, useState } from "react";

// Definição do reducer
const reducer = (state, action) => {
  switch (action.type) {
    case "add":
      return [...state, { id: Date.now(), text: action.payload, completed: false }];
    case "remove":
      return state.filter((task) => task.id !== action.payload);
    case "toggle":
      return state.map((task) =>
        task.id === action.payload ? { ...task, completed: !task.completed } : task
      );
    default:
      return state;
  }
};

function ListaTarefas() {
  const [tasks, dispatch] = useReducer(reducer, []);
  const [newTask, setNewTask] = useState("");

  const addTask = () => {
    if (newTask.trim() === "") return;
    dispatch({ type: "add", payload: newTask });
    setNewTask("");
  };

  return (
    <div>
      <h2>Lista de Tarefas</h2>
      <input
        type="text"
        value={newTask}
        onChange={(e) => setNewTask(e.target.value)}
        placeholder="Digite uma tarefa..."
      />
      <button onClick={addTask}>Adicionar</button>

      <ul>
        {tasks.map((task) => (
          <li key={task.id} style={{ textDecoration: task.completed ? "line-through" : "none" }}>
            {task.text}
            <button onClick={() => dispatch({ type: "toggle", payload: task.id })}>
              {task.completed ? "✅" : "❌"}
            </button>
            <button onClick={() => dispatch({ type: "remove", payload: task.id })}>🗑️</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ListaTarefas;
```

---

### **🔍 Explicação**
1. **O estado (`tasks`) é um array de objetos**:
   ```js
   { id: 1, text: "Estudar React", completed: false }
   ```
2. **O `reducer` gerencia três tipos de ação**:
   - `"add"` → Adiciona uma nova tarefa.
   - `"remove"` → Remove uma tarefa pelo `id`.
   - `"toggle"` → Alterna entre concluído/não concluído.
3. **O input captura a nova tarefa**, e ao clicar em "Adicionar", chamamos `dispatch({ type: "add", payload: newTask })`.
4. **Cada tarefa tem dois botões**:
   - ✅/❌ → Marca como concluída ou não.
   - 🗑️ → Remove a tarefa.

---

## 🔹 Quando usar `useReducer` em vez de `useState`?
Use **`useReducer`** quando:
✅ O estado for **complexo** ou envolver múltiplas ações.  
✅ Você precisar de **lógica clara e previsível** para modificar o estado.  
✅ O estado for baseado no estado anterior (como um carrinho de compras).  

Use **`useState`** quando:
🔹 O estado for **simples** (exemplo: um contador).  
🔹 Não houver múltiplas ações para modificar o estado.  

---

## 🔹 Resumo 📌
- **`useReducer`** é um Hook que gerencia estados mais complexos.
- Ele usa um **reducer**, que recebe o estado atual e uma ação para decidir a nova versão do estado.
- O **`dispatch`** é chamado para modificar o estado, enviando uma **ação** com um `type` e, às vezes, um `payload`.
- `useReducer` ajuda a organizar melhor o código quando há múltiplas mudanças no estado.  