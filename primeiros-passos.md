# 🚀 Primeiros Passos no React

## 🏗️ Primeiro Componente

### 📌 export default
O `export default` permite exportar um único valor ou função por arquivo, tornando mais simples a importação.

### 📌 Criando como uma função normal
```jsx
function MeuComponente() {
    return <h1>Meu Primeiro Componente!</h1>;
}
export default MeuComponente;
```

### 📌 Criando como uma arrow function
```jsx
const MeuComponente = () => {
    return <h1>Meu Primeiro Componente!</h1>;
};
export default MeuComponente;
```

## 📦 Exportando e Importando um Componente

### 🔄 export default X export normal
- `export default`: Importação sem chaves `{}`.
- `export`: Importação com chaves `{}`.

Exemplo de export normal:
```jsx
export function MeuComponente() {
    return <h1>Olá, Mundo!</h1>;
}
```

Importação:
```jsx
import { MeuComponente } from './MeuComponente';
```

## 🏗️ Usando vários componentes

### 🎯 Vantagens de usar componentes separados
- Reutilização de código
- Melhor organização
- Manutenção facilitada

### 📂 Organizando os componentes em arquivos separados dentro de uma pasta Components
Os componentes podem ser organizados dentro de uma pasta `components` para melhor estruturação.
```bash
src/
  components/
    Header.js
    Footer.js
  App.js
```

## 📜 Regras gerais do JSX

### 🔍 Diferenças entre JSX e HTML
- JSX é mais próximo de JavaScript que de HTML.
- Algumas palavras-chave do HTML mudam (ex: `class` → `className`).

### ✅ Regra 1 - Retorno único
#### Uso de fragmentos `<> </>`
```jsx
return (
    <>
        <h1>Olá</h1>
        <p>Bem-vindo ao React!</p>
    </>
);
```

### ✅ Regra 2 - Todas as tags precisam fechar
```jsx
<img src="imagem.jpg" alt="Imagem" />
```

### ✅ Regra 3 - Uso do camelCase
```jsx
const estilo = {
    backgroundColor: 'blue',
};
```

## 🎭 JSX e variáveis, funções e objetos

### 💡 Usando variáveis
```jsx
const nome = "React";
<p>Bem-vindo ao {nome}!</p>
```

### ⚡ Criando funções
```jsx
const saudacao = () => "Olá, React!";
<p>{saudacao()}</p>
```

### 🎨 Uso de objetos
#### Exemplo style inline
```jsx
const estilo = {
    color: "red",
    fontSize: "20px"
};
<p style={estilo}>Texto estilizado!</p>
```

## 📩 Passando props para um componente
```jsx
function Saudacao({ nome }) {
    return <h1>Olá, {nome}!</h1>;
}
```

## 📌 Definindo um padrão em props
### 📌 Uso do TypeScript
```tsx
interface Props {
    nome: string;
}
const Saudacao: React.FC<Props> = ({ nome }) => <h1>Olá, {nome}!</h1>;
```

## 🧒 Children do componente
### 📌 ReactNode
```tsx
import { ReactNode } from "react";
interface Props {
    children: ReactNode;
}
const Container: React.FC<Props> = ({ children }) => <div>{children}</div>;
```

### 📌 Exemplo prático
```jsx
<Container>
    <h1>Texto dentro do Container</h1>
</Container>
```

## 🔄 Renderização Condicional

### ✅ Uso padrão
```jsx
if (usuarioLogado) {
    return <p>Bem-vindo!</p>;
} else {
    return <p>Faça login</p>;
}
```

### 🔄 Uso de condição ternária
```jsx
<p>{usuarioLogado ? "Bem-vindo!" : "Faça login"}</p>
```

### 🏆 Uso de condição ternária avançado (`??`)
```jsx
const nome = usuario?.nome ?? "Visitante";
<p>Olá, {nome}!</p>
```

## 🛠️ Operador lógico &&
```jsx
{usuarioLogado && <p>Bem-vindo!</p>}
```

## 📜 Renderizando Listas
```jsx
const lista = ["React", "Vue", "Angular"];
lista.map((item, index) => <p key={index}>{item}</p>);
```

## 🔍 Filtrando Listas
```jsx
const filtrados = lista.filter((item) => item.includes("React"));
```

### 📌 Agrupando componentes
```jsx
const ListaDeItens = ({ itens }) => (
    <ul>
        {itens.map((item) => (
            <li key={item}>{item}</li>
        ))}
    </ul>
);
```

