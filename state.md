## 🔹 O que é o `state` no React?
O `state` (ou "estado") é um objeto que permite armazenar e gerenciar informações dentro de um **componente funcional** ou **classe** no React. Ele representa os **dados internos** do componente e pode mudar ao longo do tempo, causando uma **re-renderização** do componente quando alterado.

No React moderno, o `state` é geralmente gerenciado usando o **React Hooks**, especificamente o `useState`.

---

## 🔹 Como usar o `useState`?
O `useState` é um Hook que permite adicionar **estado** a um componente funcional. Ele retorna um **array com dois valores**:
1. O valor atual do estado.
2. Uma função para atualizar esse estado.

### **📌 Exemplo básico: Contador**
Aqui está um exemplo de um contador simples usando `useState`:

```jsx
import { useState } from "react";

function Contador() {
  // Criando o state inicial com valor 0
  const [contador, setContador] = useState(0);

  return (
    <div>
      <h2>Contador: {contador}</h2>
      <button onClick={() => setContador(contador + 1)}>Aumentar</button>
      <button onClick={() => setContador(contador - 1)}>Diminuir</button>
      <button onClick={() => setContador(0)}>Resetar</button>
    </div>
  );
}

export default Contador;
```

### **🔍 Explicação**
1. **`const [contador, setContador] = useState(0);`**
   - Inicializamos o state `contador` com o valor `0`.
   - `setContador` é a função que atualiza esse estado.

2. **Os botões alteram o estado ao clicar**
   - `setContador(contador + 1)` → Aumenta o contador.
   - `setContador(contador - 1)` → Diminui o contador.
   - `setContador(0)` → Reseta o contador.

3. **Toda vez que o estado muda, o componente é re-renderizado** automaticamente.

---

## 🔹 Atualizando o `state` corretamente
O React pode agrupar múltiplas atualizações de estado para otimizar a performance. Se precisar usar o estado anterior ao atualizar, utilize a **função de callback**:

```jsx
setContador(prevContador => prevContador + 1);
```

Isso garante que a atualização seja feita corretamente, mesmo se houver múltiplas chamadas da função.

---

## 🔹 Exemplo prático: Lista de Tarefas ✅
Vamos criar um componente onde o usuário pode adicionar e remover tarefas dinamicamente.

```jsx
import { useState } from "react";

function ListaTarefas() {
  const [tarefas, setTarefas] = useState([]);
  const [novaTarefa, setNovaTarefa] = useState("");

  const adicionarTarefa = () => {
    if (novaTarefa.trim() === "") return;
    setTarefas([...tarefas, novaTarefa]);
    setNovaTarefa(""); // Limpa o input após adicionar
  };

  const removerTarefa = (index) => {
    setTarefas(tarefas.filter((_, i) => i !== index));
  };

  return (
    <div>
      <h2>Lista de Tarefas</h2>
      <input
        type="text"
        value={novaTarefa}
        onChange={(e) => setNovaTarefa(e.target.value)}
        placeholder="Digite uma tarefa..."
      />
      <button onClick={adicionarTarefa}>Adicionar</button>
      
      <ul>
        {tarefas.map((tarefa, index) => (
          <li key={index}>
            {tarefa} <button onClick={() => removerTarefa(index)}>❌</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ListaTarefas;
```

### **🔍 O que acontece aqui?**
1. **`tarefas`** é um array armazenado no `state`, que começa vazio.
2. **`novaTarefa`** guarda o valor do campo de entrada (`input`).
3. **Função `adicionarTarefa`** adiciona uma nova tarefa à lista.
4. **Função `removerTarefa`** remove uma tarefa específica.
5. **Cada item da lista** recebe um botão ❌ para remoção.

---

## 🔹 Resumo 📌
- O **`state`** é um objeto que permite armazenar informações dentro de um componente e muda ao longo do tempo.
- O Hook **`useState`** permite adicionar estado a componentes funcionais.
- **Sempre use a função de atualização (`setState`)** para modificar o estado.
- Quando o `state` muda, o **React re-renderiza** o componente automaticamente.
