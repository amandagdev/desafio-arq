# Testes e Qualidade de Código

Para garantir que a qualidade do código seja uma prioridade, implementaremos uma pipeline de CI/CD e testes completos. O objetivo é automatizar a verificação da qualidade a cada alteração, fornecendo feedback rápido para os desenvolvedores e prevenindo a introdução de bugs.

### 1. Estrutura da Pipeline CI/CD

A pipeline será configurada em ferramentas como GitHub Actions e será acionada a cada `push` em uma branch ou na abertura de um Pull Request. Ela consistirá nos seguintes passos sequenciais:

1.  **Instalação (Install):**
    * A pipeline inicia instalando todas as dependências do projeto (`npm install`).

2.  **Qualidade do Código:**
    * Executa o **ESLint** para verificar se o código segue as regras de estilo e boas práticas definidas para o projeto.
    * Executa o **Prettier** em modo de verificação (`--check`) para garantir a consistência na formatação do código.


3.  **Testes Unitários e de Integração:**
    * Executa todo o teste com **Jest**.
    * Gera um relatório de **cobertura de testes** e falha se a cobertura estiver abaixo de uma meta definida (ex: 70%). Isso garante que novo código seja sempre testado.

4.  **Build da Aplicação:**
    * Executa o script de build de produção (`npm run build`). Este passo é muito IMPORTANTE para capturar erros que só aparecem durante o processo de compilação e otimização da aplicação.

5.  **Testes End-to-End:**
    * Após o build, a aplicação roda os testes **End-to-End** (com Cypress). Estes testes simulam jornadas completas do usuário (login, adicionar ao carrinho, etc.) no navegador real.

Se todos os passos passarem, o Pull Request é marcado como "aprovado". 

### 2. Estratégia e Tipos de Testes

Adotaremos a metodologia da **Pirâmide de Testes** para garantir uma cobertura eficiente e de rápida execução.

* **Base da Pirâmide: Testes Unitários (Jest + Testing Library)**
    * **1:** Testam a menor unidade de código isoladamente (um componente, uma função).
    * **2:** Muito rápidos para executar, fáceis de escrever e identificar a causa da falha.


* **Topo da Pirâmide: Testes End-to-End (Cypress)**
    * **1:** Testam um fluxo completo do usuário na aplicação rodando em um navegador.
    * **2:** Simular um usuário que entra no site, e faz todo fluxo de compra por exemplo.
    * **3:** Fornecem a maior confiança de que o sistema funciona pro usuário. 


Para criarmos um fluxo de ci/cd nesse estilo, fariamos algo assim: [exemplo simples](https://github.com/amandagdev/fintri/blob/main/.github/workflows/quality-check.yml)