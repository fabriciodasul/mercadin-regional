# 05 - Testes

Estratégia de testes do **Mercadin Regional**, com base na stack definida no README (JUnit, Mockito, MockMvc/RestAssured, Postman) e nos requisitos em `docs/02-requisitos`.

---

## 1. Objetivo

Garantir que as regras de negócio principais (cálculo de pedido, seleção de endereço, checkout) funcionem corretamente e que a API REST se comporte conforme o contrato esperado pelo frontend.

---

## 2. Ferramentas

| Ferramenta | Uso |
|---|---|
| **JUnit** | Testes unitários (camada Service, regras de negócio) |
| **Mockito** | Mock de dependências (ex: Repository) nos testes unitários |
| **MockMvc** | Testes de integração da camada Controller, sem subir servidor real |
| **RestAssured** | Testes de API end-to-end (opcional, para fluxos completos) |
| **Postman** | Testes manuais/exploratórios e documentação de endpoints (collection) |

---

## 3. Níveis de teste

### 3.1 Testes unitários (Service)
Foco nas regras de negócio isoladas, com dependências mockadas.

**Casos previstos:**
- Cálculo do valor total do pedido (itens + entrega).
- Validação de forma de pagamento (deve ser uma das opções permitidas: Cartão, Pix, Dinheiro).
- Regra de que o pedido não pode ser criado sem endereço de entrega selecionado.
- Regra de que o carrinho não pode ser finalizado vazio.

### 3.2 Testes de integração (Controller)
Foco no comportamento da API — status HTTP, formato de resposta, validação de entrada.

**Casos previstos:**
- `GET /produtos` retorna lista de produtos.
- `GET /produtos?categoria=hortifruti` filtra corretamente por categoria.
- `GET /produtos/{id}` retorna 404 quando produto não existe.
- `POST /pedidos` cria pedido com dados válidos e retorna 201.
- `POST /pedidos` retorna 400 quando faltar endereço ou forma de pagamento.
- `GET /pedidos/{id}` retorna o status atual do pedido.

### 3.3 Testes end-to-end / exploratórios (Postman)
Fluxos completos simulando o uso real do app, via collection do Postman.

**Fluxo sugerido (collection):**
1. Listar categorias
2. Listar produtos por categoria
3. Consultar detalhe de um produto
4. Criar pedido (com itens, endereço e forma de pagamento)
5. Consultar status do pedido criado

---

## 4. Cobertura esperada (MVP)

| Camada | Meta |
|---|---|
| Service (regras de negócio) | Alta cobertura — prioridade máxima |
| Controller (contrato da API) | Cobertura dos principais endpoints (happy path + erros esperados) |
| Repository | Não é prioridade testar (delegado ao Spring Data JPA), exceto queries customizadas |

> Não há meta numérica de cobertura fixada ainda (ex: 80%) — a definir conforme o projeto avançar.

---

## 5. Pendências

- [ ] Criar collection do Postman e versionar em `docs/05-testes/postman/`.
- [ ] Definir se serão usados testes de contrato (ex: Spring Cloud Contract) — provavelmente fora de escopo do MVP.
- [ ] Definir ambiente de testes (banco de dados em memória como H2, ou PostgreSQL via Testcontainers).
- [ ] Adicionar testes específicos assim que o módulo de Usuário/autenticação for definido.