# [BUG-02] Front-end envia parâmetro q= vazio na API de busca e filtra produtos apenas no navegador

- **Tipo:** Bug Funcional / Validação de Entrada
- **Severidade:** Medium/Médio
- **Prioridade:** Medium/Médio
- **Ambiente:** OWASP Juice Shop (Local / Docker) | Chrome DevTools (Network)

## Pré-condições
- Usuário autenticado com JWT válido (`token`) e `bid` válido.

## Passos para Reproduzir
1. Já logado pesquise por "apple" por exemplo e observe a aba de network do devtools

## Resultado Atual
Front-end dispara GET /rest/products/search?q= vazio, baixa o catálogo inteiro (5.5 kB) e filtra localmente no navegador.

## Resultado Esperado
Front-end deveria enviar GET /rest/products/search?q=apple para o servidor filtrar antes de responder.