# 🚀 Testes Automatizados de API com Postman
Projeto de testes automatizados de API REST desenvolvido para validação de integridade de dados e regras de negócio.
## 🎯 Objetivo
Validar os fluxos principais (caminho feliz e tratamento de erros) dos endpoints de Posts e Usuários, garantindo contrato, integridade dos dados e tempo de resposta aceitável.
## 🛠️ Tecnologias Utilizadas
- **Postman Desktop** (Criação de requisições e execução em lote com Collection Runner)
- **JavaScript / Chai Assertion Library** (Scripts de validação automatizada)
- **Git & GitHub** (Versionamento e portfólio)
- **API Testada:** [JSONPlaceholder](https://jsonplaceholder.typicode.com/)
---
## 🧪 Cenários de Teste Cobertos
| Método | Endpoint | Cenário / Objetivo | Validações Automatizadas | Status Esperado |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/posts/1` | Consulta de post existente | - Status Code 200<br>- Validação do `id == 1` | `200 OK` |
| **POST** | `/posts` | Cadastro de novo post | - Status Code 201<br>- Tempo de resposta < 1000ms<br>- Validação do título enviado | `201 Created` |
| **GET** | `/posts/9999` | Cenário negativo (id inexistente) | - Validação de erro controlado | `404 Not Found` |
