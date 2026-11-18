# [BUG-04] Vazamento de dados de usuário por IDOR

- **Tipo:** Segurança / AppSec
- **Severidade:** High/Alto
- **Prioridade:** High/Alto
- **Ambiente:** OWASP Juice Shop (Local / Docker) | Postman

## Pré-condições
- Usuário autenticado com JWT válido (`token`) e `bid` válido.

## Passos para Reproduzir
1. Suba o app do OWASP JuiceShop e entre no [http://localhost:3000]
2. Faça o login
3. Altere a URL colocando um outro valor em [http://localhost:3000/rest/basket/1] (enviado via Postman com Authorization: Bearer {{token}})

## Resultado Atual
O usuário consegue acessar outra "basket" caso esteja logado, basta apenas trocar o número da URL.

## Resultado Esperado
O usuário deveria ser bloqueado de visualização ou deveria receber um erro, mantendo as informações do usuário, seguras
Status esperado: 401 Unauthorized ou 403 Forbidden.