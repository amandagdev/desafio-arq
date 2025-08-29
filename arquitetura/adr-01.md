# ADR-01: Arquitetura com Micro-frontends

## Contexto

A empresa precisa desenvolver uma nova aplicação web de varejo. A arquitetura deve permitir alta escalabilidade, flexibilidade e fácil manutenção.

## Decisão

Sugiro uma **arquitetura de micro-frontends**. A aplicação será criada em partes menores, correspondentes aos contextos de negócio, que serão desenvolvidas e implementadas de forma independente. Cada time será dono de um ou mais micro-frontends assim tornando o sistema modular.

A orquestração e o carregamento serão realizados utilizando **Module Federation**.


## Consequências

* **Positivas:**
    * **Autonomia de Times:** As equipes podem desenvolver, testar e fazer o deploy de suas funcionalidades de forma independente, reduzindo gargalos e aumentando a velocidade de entrega.
    * **Escalabilidade:** A arquitetura suporta o crescimento da equipe e da aplicação. Novos times e funcionalidades podem ser adicionados como novos MFES sem grande impacto no sistema atual.
    * **Resiliência:** Uma falha em um micro-frontend tem menor probabilidade de impactar funcionalidades importantes da aplicação.
    * **Flexibilidade:** Permite que diferentes equipes, utilizem tecnologias diferentes para seus respectivos micro-frontends se preciso.

    * **Negativas:**
    * **Complexidade de Compartilhamento:** Compartilhar código (ex: Design System) e gerenciar versões entre dezenas de repositórios é o principal desafio.
        * **Solução:** O código compartilhado será gerenciado em seus próprios repositórios e publicado como **pacotes versionados em um registro NPM** (ex: GitHub Packages).
    * **Risco de Inconsistência:** A experiência do usuário e as configurações de desenvolvimento podem divergir entre os diferentes repositórios.
        * **Solução:** O **Design System** (publicado como pacote) vai garantir total consistencia.
    * **Complexidade:** Atualizar uma dependência compartilhada (ex: o Design System) pode exigir a atualização e o deploy de múltiplos micro-frontends.
        * **Solução:** Serão criadas **pipelines de CI/CD** que, após a publicação de uma nova versão de um pacote chave, automaticamente abrirão Pull Requests para atualizar a dependência nos projetos consumidores.
    * **Performance:** Existe o risco de duplicação de bibliotecas (ex: React).
        * **Solução:** O uso do **Module Federation** continua sendo a solução para este problema, pois seu mecanismo de compartilhamento de dependências funciona entre diferentes projetos, garantindo que sejam carregadas apenas uma vez.
    


## Tecnologias


As tecnologias padrão para o desenvolvimento do front-end será a seguinte:

* **Framework: Next.js**
   Oferece renderização híbrida (SSR/SSG), crucial para **SEO** e **performance**. Altamente popular e com muitas soluções na internet.
   Podemos também optar pelo **react** sem next, e aplicar melhores práticas como code splitting, lazy loading, memo etc

* **Estado do Servidor: React Query**
   Ideal para gerenciar o ciclo de vida de dados de APIs, simplificando a lógica de dados e melhorando a experiência do usuário. 

* **Estilização: Tailwind**
    Permite a construção rápida e consistente de UIs através de classes.

* **Testes: Jest + RTL**
    **Jest** é o padrão de mercado para testes, funciona muito bem e entrega tudo que precisamos em cenarios de testes.

* **Linguagem: TypeScript**
    Quase que obrigatório para projetos grandes. Garante a segurança de tipos, reduz bugs e é como documentação código.

* **Gerenciamento de estado: Context api ou Zustand**
    Para estados globais robustos da UI (carrinho, autenticação) sugiro Zustand pois é uma solução leve, moderna e fácil de desenvolver, para estados mais simples seguiria com context api.


