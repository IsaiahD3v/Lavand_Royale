# Lavand Royale 🌸

Bem-vindo ao repositório do **Lavand Royale**, um protótipo de e-commerce moderno, elegante e focado em estética premium de "Liquid Glass" (Vidro Líquido da Apple). Desenvolvido com **Svelte**, **Vite** e **TypeScript**, este projeto foi criado para oferecer uma experiência visual imersiva com animações suaves e interfaces translúcidas.

## ✨ Características Principais

* **Estética Premium (Liquid Glass)**: Painéis com alto desfoque de fundo (blur) e bordas luminosas (rim lighting), proporcionando uma aparência cristalina.
* **Fundo Animado (Mesh Gradient)**: Um gradiente de malha animado em CSS puro que refrata através dos componentes de vidro do site.
* **Transição Cinemática de Tema**: Suporte completo ao modo claro e escuro utilizando a moderna `View Transitions API`, criando um "crossfade" cinematográfico perfeito ao alternar os temas.
* **Cursor Personalizado**: Um cursor de flor de lavanda em SVG nativo que se transforma suavemente em uma seta após o usuário passar o mouse sobre itens clicáveis por 0,3 segundos.
* **Roteamento SPA**: Navegação limpa e sem recarregamentos utilizando a `History API` (`/` para Home e `/our-values` para Nossos Valores).
* **Interações e Carrossel**: Carrossel infinito para exibição das assinaturas aromáticas e modals premium para detalhes dos produtos com redirecionamento para o WhatsApp.

## 🚀 Como Rodar o Projeto Localmente

1. **Pré-requisitos**: Certifique-se de ter o [Node.js](https://nodejs.org/) instalado.
2. **Instalar Dependências**:
   Abra o terminal na pasta `app` e rode o comando:
   ```bash
   npm install
   ```
3. **Iniciar o Servidor de Desenvolvimento**:
   ```bash
   npm run dev
   ```
4. **Acessar**: Abra o seu navegador e acesse [http://localhost:5173](http://localhost:5173).

## 📁 Estrutura do Projeto

- `/src/App.svelte`: O componente principal da aplicação, responsável pelo roteamento SPA, gerenciamento do tema e pelo cursor customizado.
- `/src/app.css`: Onde toda a mágica do CSS acontece! Contém a animação de fundo (`bg-mesh`) e a redefinição global da classe `.glass-panel`.
- `/src/lib/Home.svelte`: A página inicial, contendo o Hero section e o carrossel infinito.
- `/src/lib/Values.svelte`: A página "Nossos Valores", contendo detalhes sobre a Filosofia, Depoimentos e Fornecedores.

## 🛠 Tecnologias Utilizadas
- **Svelte**: Framework de interface de usuário.
- **Vite**: Ferramenta de build extremamente rápida.
- **TypeScript**: Superset de JavaScript com tipagem estática.
- **CSS3 Puro**: Para todas as animações e efeitos de "Liquid Glass".

---
*Criado com dedicação para a Lavand Royale.*
