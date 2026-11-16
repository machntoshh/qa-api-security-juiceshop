# Mapeamento de API — OWASP Juice Shop

Base URL local: `http://localhost:3000`

| Fluxo | Método | Endpoint | Status Esperado | Payload / Notas |
| :--- | :--- | :--- | :--- | :--- |
| Cadastro | `POST` | `/api/Users/` | `201 Created` | `{ "email", "password", "passwordRepeat", "securityAnswer" }` |
| Login (JWT) | `POST` | `/rest/user/login` | `200 OK` | `{ "email", "password" }` → Retorna `authentication.token` e `bid` |
| Busca de Produtos | `GET` | `/rest/products/search?q=` | `200 OK` | Front-end filtra localmente; endpoint aceita `?q=termo` |
| Adicionar ao Carrinho | `POST` | `/api/BasketItems/` | `200 OK` | `{ "ProductId", "BasketId", "quantity" }` (usa JWT) |
| Ver Carrinho | `GET` | `/rest/basket/{bid}` | `200 OK` | Usa `bid` retornado no login + JWT |