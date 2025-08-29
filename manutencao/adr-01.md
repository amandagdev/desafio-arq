# ADR-02: Plano de Refatoração

## Contexto

Temos um sistema legado com alta divída tecnica e precisamos ter um plano de ação para refatorar esse sistema de forma segura e eficaz.


## Decisão

Faremos um plano de ação que consiste em uma **refatoração incremental**, evitando uma reescrita completa que teria um alto risco e paralisaria algumas entregas. O plano é dividido em três:

**1: Análise**

1.  **Mapeamento:** Realizar um mapeamento de fluxos de usuário mais críticos e as contextos com maior dificuldade em código. Utilizar ferramentas de análise (ex: SonarQube) para identificar pontos críticos.
2.  **Verificação de testes:** Antes de qualquer alteração, seria importante verificar os testes existentes e utiliza los para manter tudo funcionando.

**2: Refatoração Incremental**

1.  Novas funcionalidades serão construídas usando a nova arquitetura com todos os novos padrões definidos. Gradualmente, funcionalidades antigas serão reescritas ou substituídas por estes novos módulos, substituindo o código legado até que ele possa ser removido.
2. Ao trabalhar em uma tarefa (bug fix, feature etc) em uma área legada, a equipe se compromete a deixar o código um pouco mais limpo do que encontrou. Isso inclui renomear variáveis, quebrar funções grandes e, **adicionar novos testes unitários** na área modificada.

**3: Melhoria Contínua**

1.  **Documentação:** Documentar os novos padrões de arquitetura e código para que sirvam de guia para toda a equipe.
2.  **Revisão de Código:** Implementar um processo de revisão de código onde todo PR deve incluir testes e aderir aos novos padrões. Isso se torna a principal ferramenta para garantir a qualidade e conhecimento da equipe.

## Consequências

* **Positivas:**

    **Entrega Contínua:** A aplicação nunca para de receber melhorias e novas funcionalidades. Não há um período de stop para a refatoração.

    **Conhecimento:** Com o tempo, as novas partes do sistema se tornam a maior parte da base de código, facilitando o fluxo de novos desenvolvedores. juntamente com a nova documentação.

* **Negativas:**

     **Progresso Lento:** Os resultados não tão rápidos, pois o passo 1 consome tempo em análise e nos ajustes dos testes.

     **Complexidade:** Durante a transição, a equipe precisará lidar com a complexidade de ter dois sistemas (o legado e o novo).

     **Exige muita disciplina:** O sucesso do plano depende inteiramente da equipe em seguir as novas práticas, e seguir com o processo de code review.