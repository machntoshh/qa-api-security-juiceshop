# QA & API Security Testing — OWASP Juice Shop

Projeto prático de testes funcionais, validação de contratos de API e checagens básicas de AppSec aplicados ao **OWASP Juice Shop** (ambiente local via Docker).

## Objetivo
Demonstrar domínio prático em:
- Engenharia reversa de endpoints via **Chrome DevTools (Network)**
- Testes automatizados de API com **Postman** (`pm.test`, variáveis de ambiente, encadeamento de JWT)
- Testes negativos e checagens básicas de segurança (**IDOR**, **SQL Injection**, **Exposição de Dados**)
- Documentação de defeitos no padrão **Jira**

## Ferramentas Utilizadas
- **Alvo:** OWASP Juice Shop (Docker local — `http://localhost:3000`)
- **Inspeção de Rede:** Chrome DevTools (`Fetch/XHR`)
- **Testes de API:** Postman (Collection v2.1 + Environment + Assertions JS)
- **Versionamento & Docs:** Git / GitHub / Markdown

## Estrutura do Repositório
```text
├── docs/
│   └── api-mapping.md          # Mapeamento dos 4 fluxos principais via DevTools
├── postman/
│   ├── juiceshop.postman_collection.json
│   └── juiceshop.postman_environment.json
├── bug-reports/                # 5 bug reports detalhados (padrão Jira)
│   ├── BUG-01-negative-quantity-basket.md
│   ├── BUG-02-empty-search.md
│   ├── BUG-03-weak-password-accepted.md
│   ├── BUG-04-IDOR-basket.md
│   └── BUG-05-vazamento-injection-sql.md
└── README.md
```

## Cobertura de Testes (Postman)
- **Auth:** Cadastro (`POST /api/Users/`), Login com extração automática de JWT e `bid` (`POST /rest/user/login`), senha inválida (`401`), e-mail duplicado (`400`).
- **Products:** Busca de produtos (`GET /rest/products/search?q=`) e busca por termo inexistente.
- **Basket:** Adição ao carrinho com Bearer Token (`POST /api/BasketItems/`), consulta do carrinho (`GET /rest/basket/{{bid}}`) e teste negativo de quantidade negativa.
- **Security Checks:**
  - **Controle de Acesso / IDOR:** Tentativa de leitura do carrinho de outro usuário (`GET /rest/basket/1`) e acesso sem token (`401`).
  - **Validação de Entrada / SQLi:** Payload `' OR 1=1--` na busca expondo erro `500` (`SQLITE_ERROR`).
  - **Exposição de Dados:** Verificação de campos sensíveis em `/rest/user/whoami` e no payload do JWT de login.

## Principais Achados (Bug Reports)
| ID | Tipo | Resumo | Severidade |
| :--- | :--- | :--- | :--- |
| [BUG-01](bug-reports/BUG-01-negative-quantity-basket.md) | Funcional | Erro `500` ao enviar quantidade negativa no carrinho | High |
| [BUG-02](bug-reports/BUG-02-empty-search.md) | Funcional | Front-end envia `q=` vazio e filtra catálogo no navegador | Medium |
| [BUG-03](bug-reports/BUG-03-weak-password-accepted.md) | Funcional | Cadastro aceita senha fraca (`123456`) sem complexidade mínima | High |
| [BUG-04](bug-reports/BUG-04-IDOR-basket.md) | Segurança | IDOR permite ler carrinho de outro usuário (`GET /rest/basket/1`) | High |
| [BUG-05](bug-reports/BUG-05-vazamento-injection-sql.md) | Segurança | Payload SQLi retorna `500` vazando `SQLITE_ERROR` | High |

## Como Executar Localmente
1. Subir o OWASP Juice Shop via Docker:
   ```bash
   docker run --rm -p 3000:3000 bkimminich/juice-shop
   ```
2. Importar a Collection e o Environment da pasta `/postman` no Postman.
3. Selecionar o Environment **`Juiceshop - Local`** e rodar primeiro **`Register User`** e **`Login`** (o token JWT e o `bid` são salvos automaticamente).