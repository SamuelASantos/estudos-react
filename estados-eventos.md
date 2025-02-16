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