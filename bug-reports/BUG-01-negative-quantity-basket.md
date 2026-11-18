# [BUG-01] API retorna 500 Internal Server Error ao adicionar quantidade negativa no carrinho

- **Tipo:** Bug Funcional / Validação de Entrada
- **Severidade:** High/Alto (quebra a API com erro 500 não tratado)
- **Prioridade:** High/Alto
- **Ambiente:** OWASP Juice Shop (Local / Docker) | Postman

## Pré-condições
- Usuário autenticado com JWT válido (`token`) e `bid` válido.

## Passos para Reproduzir
1. Enviar `POST http://localhost:3000/api/BasketItems/` com header `Authorization: Bearer {{token}}`.
2. Enviar no Body JSON:
   ```json
   {
     "ProductId": 1,
     "BasketId": "{{bid}}",
     "quantity": -5
   }
   ```

## Resultado Atual
A API retorna `500 Internal Server Error` (página HTML com erro SQLite) em vez de validar o valor.

## Resultado Esperado
A API deve validar `quantity >= 1` e retornar `400 Bad Request` com mensagem clara de erro.