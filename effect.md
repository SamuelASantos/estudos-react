O `useEffect` é um dos hooks mais importantes do React, usado para lidar com efeitos colaterais em componentes funcionais. Ele substitui os métodos de ciclo de vida dos componentes de classe, como `componentDidMount`, `componentDidUpdate` e `componentWillUnmount`.

---

## 📌 **O que é o useEffect?**
Ele permite que você execute código sempre que o componente:
1. **For montado** (executado uma única vez ao carregar).
2. **For atualizado** (quando certas variáveis mudam).
3. **For desmontado** (limpeza de efeitos).

### **Sintaxe Básica**
```jsx
import { useEffect } from "react";

useEffect(() => {
  // Código que será executado
}, [dependências]); 
```
- Se as **dependências** estiverem vazias (`[]`), o efeito ocorre **apenas uma vez** quando o componente é montado.
- Se houver dependências, o efeito ocorre **sempre que a variável dentro do array mudar**.
- Se **não houver array de dependências**, o efeito ocorre **toda vez que o componente renderiza**.

---

## 🚀 **Exemplos Práticos**

### **1️⃣ Executar apenas na montagem**
Se precisar buscar dados de uma API apenas quando o componente for renderizado, use um array de dependências vazio (`[]`).
```jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Componente montado!");
  }, []); 

  return <h1>Olá, mundo!</h1>;
}
```
📌 O `console.log` será executado **apenas uma vez**.

---

### **2️⃣ Executar quando uma variável mudar**
Se precisar reagir a mudanças em uma variável, adicione-a ao array de dependências.
```jsx
import { useState, useEffect } from "react";

function Contador() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(`O contador mudou para: ${count}`);
  }, [count]); 

  return (
    <div>
      <p>Contador: {count}</p>
      <button onClick={() => setCount(count + 1)}>Incrementar</button>
    </div>
  );
}
```
📌 Sempre que `count` mudar, o `console.log` será executado.

---

### **3️⃣ Executar código quando o componente for desmontado**
Se precisar limpar um efeito antes do componente ser removido (exemplo: remover um **event listener** ou **parar um timer**), retorne uma função dentro do `useEffect`.
```jsx
import { useEffect } from "react";

function Temporizador() {
  useEffect(() => {
    const timer = setInterval(() => {
      console.log("Executando a cada 1 segundo");
    }, 1000);

    return () => {
      clearInterval(timer); // Limpa o timer quando o componente for desmontado
      console.log("Temporizador removido");
    };
  }, []);

  return <h1>Temporizador ativo</h1>;
}
```
📌 O `clearInterval(timer)` impede que o timer continue rodando quando o componente for desmontado.

---

## 🎯 **Resumo**
| Caso | Código | Quando executa? |
|------|--------|----------------|
| Apenas na montagem | `useEffect(() => { ... }, [])` | Uma vez quando o componente renderiza. |
| Quando uma variável muda | `useEffect(() => { ... }, [state])` | Sempre que `state` mudar. |
| Quando o componente desmonta | `useEffect(() => { return () => { ... } }, [])` | Ao desmontar o componente. |