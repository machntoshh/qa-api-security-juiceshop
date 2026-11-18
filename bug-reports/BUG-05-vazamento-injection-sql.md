# [BUG-05] Erro 500 e exposição de SQLITE_ERROR ao enviar payload de SQL Injection na busca

- **Tipo:** Segurança / AppSec
- **Severidade:** High/Alto
- **Prioridade:** High/Alto
- **Ambiente:** OWASP Juice Shop (Local / Docker) | Postman

## Pré-condições
- Usuário autenticado com JWT válido (`token`) e `bid` válido.

## Passos para Reproduzir
1. Suba o app do OWASP JuiceShop e entre no [http://localhost:3000]
2. Altere a URL colocando um outro valor em [http://localhost:3000/rest/products/search?q=' OR 1=1--]

## Resultado Atual
O site retorna um internal error 500, expondo o tipo de erro no banco de dados, sendo ele SQLITE_ERROR

## Resultado Esperado
Tratação correta, retornando 200 com os dados em um array vazio ou status code 400