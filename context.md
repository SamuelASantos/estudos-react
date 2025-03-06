```markdown
## 🔹 O que é o Context no React?

O **Context** é um recurso poderoso do React que permite compartilhar estados ou dados entre múltiplos componentes, sem precisar passar essas informações através de várias camadas de componentes usando props.

Em outras palavras, o Context ajuda você a evitar o problema conhecido como **"prop drilling"**, tornando o compartilhamento de estados mais fácil, limpo e eficiente.

---

## 🔹 Quando usar Context?

Utilize Context quando:

- ✅ Um estado precisa estar disponível em múltiplos componentes distantes entre si.
- ✅ Você deseja evitar o prop drilling (props passadas por muitos níveis de componentes).
- ✅ Você precisa de um gerenciamento centralizado simples de estados globais.

---

## 🔹 Como usar Context na prática?

Existem **três passos essenciais** para usar Context no React:

### 1. Criar o Context

```jsx
import { createContext } from "react";

const MeuContexto = createContext();

export default MeuContexto;
```

---

### 2. Prover o Context (**Provider**)

O **Provider** fornece os dados aos componentes filhos que precisarem acessar o estado compartilhado:

```jsx
import { useState } from "react";
import MeuContexto from "./MeuContexto";

function MeuProvider({ children }) {
  const [usuario, setUsuario] = useState({ nome: "Samuel", logado: true });

  return (
    <MeuContexto.Provider value={{ usuario, setUsuario }}>
      {children}
    </MeuContexto.Provider>
  );
}

export default MeuProvider;
```

- Aqui, `usuario` e `setUsuario` são os valores que você quer compartilhar entre vários componentes.

---

### 3. Consumir o Context (**useContext**)

Agora, qualquer componente dentro do Provider pode facilmente acessar esses dados usando o hook `useContext`:

```jsx
import { useContext } from "react";
import MeuContexto from "./MeuContexto";

function ComponentePerfil() {
  const { usuario } = useContext(MeuContexto);

  return (
    <div>
      <h2>Olá, {usuario.nome}!</h2>
      <p>Status: {usuario.logado ? "Online ✅" : "Offline ❌"}</p>
    </div>
  );
}

export default ComponentePerfil;
```

---

## 🚩 Resumo (quando usar Context)

- ✅ **Excelente** para estados globais ou que precisam ser compartilhados amplamente.
- ✅ Simplifica o compartilhamento de estado e evita complexidade desnecessária.
- ❌ **Não utilize** em estados locais simples que não serão compartilhados, pois gera uma complexidade desnecessária.

---

## 💡 Dicas Extras (para avançar)

- Em aplicações maiores, é comum combinar **Context** com o **useReducer** para gerenciar estados complexos.
- Context pode ser uma alternativa mais simples e eficiente ao uso de bibliotecas externas como Redux, principalmente em projetos médios ou menores.

---
```