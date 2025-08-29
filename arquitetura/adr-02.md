# ADR-02 (Alternativa 2): Arquitetura Modular com Pacotes NPM


## Contexto

A empresa precisa desenvolver uma nova aplicação web de varejo. A arquitetura deve permitir alta escalabilidade, flexibilidade e fácil manutenção.
## Decisão

A arquitetura será composta por:

1.  Um **"Projeto Principal"**: Uma aplicação leve, responsável pela estrutura geral, roteamento principal e por ter as funcionalidades.
2.  Múltiplos **"Pacotes de Funcionalidade"**: Cada contexto de negócio (`catalogo`, `checkout` etc.) será desenvolvido como um **pacote NPM independente**.
    * Cada pacote terá seu próprio repositório, versionamento e ciclo de vida.
    * Eles serão publicados em um **registro NPM** (ex: GitHub Packages).

O **Projeto Principal** instalará os "Pacotes de Funcionalidade" como dependências em seu `package.json`. A integração final dos módulos ocorrerá em **tempo de build**, quando a aplicação principal for compilada, gerando um único *bundle* para deploy.

## Consequências

* **Positivas:**
    * **Isolamento e Fronteiras Fortes:** Esta é a principal vantagem. A separação por pacotes NPM cria a fronteira mais forte possível entre os contextos. A comunicação é um "contrato" formal via API do pacote e versionamento.
    * **Autonomia :** A equipe de `checkout` pode evoluir e lançar novas versões do seu pacote de forma totalmente independente da equipe de `catalogo`.
    * **Simplicidade de Deploy:** Assim como o monolito modular, o resultado final é uma única aplicação, o que simplifica enormemente a infraestrutura e o processo de deploy em comparação com micro-frontends.
    * **Reutilização:** Um pacote de funcionalidade bem definido poderia, teoricamente, ser reutilizado em outras aplicações da empresa.

* **Negativas:**
    * **Fluxo de Trabalho Lento:** Este é o maior ponto negativo. Para testar uma pequena alteração de um pacote na aplicação principal, o dev precisa: 1) Fazer a alteração no pacote, 2) Publicar uma nova versão, 3) Atualizar a versão no `package.json` da aplicação principal, 4) Rodar `npm install`. Este ciclo é lento e pode desencorajar refatorações rápidas. (Ferramentas como `npm link` ou um monorepo podem ajudar nisso, mas adicionam uma certa complexidade).
    * **Acoplamento no Deploy:** A aplicação inteira ainda precisa ser reconstruída e implantada para que uma atualização em um único pacote chegue à produção.

---

### Resumo da Comparação

* **Micro-frontends:** Máxima autonomia de **deploy**. Maior complexidade de infra.
* **Modular com Pacotes NPM:** Máxima autonomia de **desenvolvimento e versionamento**. O custo é a complexidade no fluxo de trabalho e na gestão de dependências.


## Tecnologias


As tecnologias padrão para o desenvolvimento do front-end será a seguinte:

* **Framework: Next.js**
   Oferece renderização híbrida (SSR/SSG), crucial para **SEO** e **performance**. Altamente popular e com muitas soluções na internet.

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
