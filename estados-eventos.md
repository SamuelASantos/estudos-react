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