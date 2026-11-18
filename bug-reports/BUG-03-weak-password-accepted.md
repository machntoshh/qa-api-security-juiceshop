# [BUG-03] Cadastro aceita senha fraca, sem validação de complexidade

- **Tipo:** Bug Funcional / Validação de Entrada
- **Severidade:** High/Alto
- **Prioridade:** Medium/Médio
- **Ambiente:** OWASP Juice Shop (Local / Docker) | Postman

## Pré-condições
- Usuário na tela de cadastro

## Passos para Reproduzir
1. Suba o app do OWASP JuiceShop e entre no [http://localhost:3000]
2. Insira um e-mail
3. Insira uma senha fraca, "123456" por exemplo

## Resultado Atual
O site aceita, não é feita uma validação de complexidade de senha, não é pedido nenhum tipo de uppercase ou symbols (@, #, $).

## Resultado Esperado
O site deveria bloquear senhas fracas, solicitando que o usuário colocasse algo mais forte para não haver problemas de segurança