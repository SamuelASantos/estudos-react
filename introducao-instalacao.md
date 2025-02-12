# 📌 Introdução e Instalação

## 🚀 O que é React?

React é uma biblioteca JavaScript para a construção de interfaces de usuário. Desenvolvido pelo Facebook, ele permite criar interfaces dinâmicas e reativas de forma eficiente. O foco principal do React é a construção de componentes reutilizáveis e a atualização eficiente do DOM.

## ⚡ O que é DOM Virtual?

O DOM Virtual é uma representação leve do DOM real na memória. O React usa essa técnica para otimizar atualizações na interface, tornando as mudanças mais rápidas e eficientes. Em vez de modificar diretamente o DOM real, o React compara a versão virtual com a atual e faz apenas as alterações necessárias.

## 🎨 Como usar o React

O React pode ser usado de diferentes formas, seja via CDN ou instalando localmente em um projeto. Ele permite a criação de componentes reutilizáveis, facilitando o desenvolvimento de aplicações escaláveis.

## 🧠 Como pensar em reactês?

Pensar em "reactês" significa estruturar sua aplicação baseada em componentes reutilizáveis e na gestão de estado. É importante entender como os componentes se comunicam entre si e como o fluxo de dados funciona dentro da aplicação.

## 🔥 O que é Next, Remix e Gatsby?

Esses são frameworks baseados em React que trazem diferentes abordagens para o desenvolvimento web:

- **Next.js**: Focado em renderização no servidor (SSR) e geração estática (SSG).
- **Remix**: Prioriza experiências otimizadas para o usuário, com foco em carregamento de dados eficiente.
- **Gatsby**: Especializado em sites estáticos e otimizados para SEO.

## 🌎 Usando React via CDN

Para testar o React sem necessidade de instalação, é possível incluí-lo diretamente via CDN:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React via CDN</title>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
<body>
    <div id="root"></div>
    <script type="text/babel">
        function App() {
            return <h1> Olá, React! </h1>;
        }
        ReactDOM.render(<App />, document.getElementById('root'));
    </script>
</body>
</html>
```

## 📦 Instalando o Node.js

O Node.js é necessário para gerenciar pacotes e executar scripts de desenvolvimento do React. Para instalar:

1. Acesse [Node.js](https://nodejs.org/)
2. Baixe a versão recomendada (LTS)
3. Verifique a instalação:
   ```sh
   node -v
   npm -v
   ```

## 🏗️ Iniciando um projeto com Next.js

Next.js permite criar aplicações React otimizadas com facilidade. Para criar um projeto:

```sh
npx create-next-app@latest meu-projeto
cd meu-projeto
npm run dev
```

Isso inicia um servidor de desenvolvimento local em `http://localhost:3000/`.

## ⚡ Iniciando um projeto com Vite

Vite é uma ferramenta leve para inicialização rápida de projetos React. Para criar um projeto com Vite:

```sh
npm create vite@latest meu-projeto --template react
cd meu-projeto
npm install
npm run dev
```

O Vite inicia um servidor rápido e eficiente para desenvolvimento.

---
