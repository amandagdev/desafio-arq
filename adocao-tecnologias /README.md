# Adoção de Novas Tecnologias

Escolher uma nova tech, como um framework, é uma decisão de grande impacto.
Nosso plano para avaliar e potencialmente adotar um novo framework tem que ser dividido:

### 1: Pesquisa

1.  **Motivação:** Antes de tudo, precisamos definir qual problema ou quais problemas o novo framework vai resolver.

2.  **Análise:** Análise inicial para pesquisar problemas atuais do novo framework, resoluções, tamanho da comunidade, adoção do mercado etc

### 2: Prova de Conceito (PoC)

Esta é a fase mais importante, onde validamos o framework

1.  **Escopo Definido:** Selecionamos uma funcionalidade **pequena** do nosso projeto existente (ou uma nova porém pequena) para ser reconstruída com o novo framework.
2.  **1:** Não devemos gastar muito tempo nela e nem muitos devs alocados.
3.  **2:** Ao final, a equipe da PoC apresenta um relatório com:
    * Exemplos de código (prós e contras).
    * Uma recomendação final baseada na experiência.

### Fase 3: Decisão

1.  **Decisão com base na POC:** Com o relatório da PoC, a equipe toma a decisão final.
2.  **Implementação Gradual:** Se a decisão for "sim", a implementação será feita de forma gradual e segura.
    * **Começar com o Novo:** Todas as *novas funcionalidades* serão construídas com o novo framework.
    * **Não Recrever o Antigo (por enquanto):** Evitaremos a reescrita de funcionalidades legadas que estão estáveis, mas se a ideia for reenscrever todo o sistema teria que ser feito uma nova estratégia para a implementação longo prazo, algo parecido com o que foi abordado no tópico de manutenção desse desafio.
