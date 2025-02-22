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
