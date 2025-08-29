# Integração com APIs


### Serviço

* Podemos criar uma arquivo api.js dentro de um util pra melhor abstração nos services que vamos criar para cada contexto
* Criamos um service.ts para cada contexto: auth/service-auth.ts, client/service-client.ts e dentro de cada um vai ter ser serviço seja ele de adicionar, remover, duplicar etc

---

### Autenticação

* Usamos **JWT** (`accessToken` + `refreshToken`).
* O `accessToken` fica na memória; o `refreshToken` em um **cookie HttpOnly** para segurança.
* Um **interceptor** adiciona o token `Authorization` em todas as requisições.
* O mesmo interceptor detecta erros `401` e usa o `refreshToken` para renovar o token automaticamente.

---

### Tratamento de Erros e Logging

* O interceptor também centraliza o tratamento de erros (como `404` ou `500`).
* Ele mostra uma notificação para o usuário (ex: "Ocorreu um erro ao cadastrar um novo orçamento").
* Em produção, ele envia os detalhes do erro para uma ferramenta como o **Sentry** para facilitar a depuração.

---

### Comunicação

* podemos usar o **React Query** para gerenciar as chamadas de API.
* **Benefícios:**
    * **Cache:** Evita carregar os mesmos dados várias vezes.
    * **De-duplicação:** junta chamadas idênticas em uma só.
    * **Revalidação:** Mantém os dados atualizados de forma automática.
    

### Estrutura de Pastas


```text
/src
|
├── /features                
│   |
│   ├── /quotes           
│   │   ├── /components
│   │   │   └── quote-list.tsx
│   │   ├── quote.service.ts
│   │   └── index.ts         
│   |
│   ├── /clients            
│   │   ├── /components
│   │   │   └── client-list.tsx
│   │   ├── client.service.ts
│   │   └── index.ts
│   |
│   └── /auth                
│       ├── /components
│       │   └── login.tsx
│       ├── auth.service.ts
│       └── index.ts
|
└── /shared                 
    |
    ├── /api
    │   └── index.ts  
    |
    ├── /ui
    │   ├── Button.tsx  
    │ 
    |
    └── /store
        └── auth.store.ts    / Store para o token de autenticação