# 04 - Arquitetura

Documentação da arquitetura técnica do **Mercadin Regional**, com base nos requisitos definidos em `docs/02-requisitos` e no fluxo de telas em `docs/03-ux-ui`.

---

## 1. Visão geral

O sistema é composto por um **backend REST em Java/Spring Boot**, um **banco de dados relacional PostgreSQL** e um **frontend mobile-first** (tecnologia a definir) que consome a API.

```
[ Cliente / App mobile-first ]
            |
            v  (HTTP/REST, JSON)
[ Backend - Spring Boot ]
            |
            v  (JDBC)
[ PostgreSQL ]
```

No MVP não há integração com gateway de pagamento nem serviço de notificação automatizado — a confirmação do pedido ao comerciante ocorre via WhatsApp/telefone (processo manual, fora do sistema).

---

## 2. Estilo arquitetural

- **Arquitetura em camadas (Layered Architecture)**, padrão para aplicações Spring Boot:
  - **Controller** — camada de entrada HTTP, recebe requisições e retorna respostas (DTOs).
  - **Service** — regras de negócio (ex: cálculo do total do pedido, validação de endereço).
  - **Repository** — acesso a dados via Spring Data JPA.
  - **Model/Entity** — representação das tabelas do banco.

- **API REST** como contrato entre frontend e backend, retornando JSON.

---

## 3. Módulos / domínios

Com base nos requisitos funcionais (RF01–RF20):

| Módulo | Responsabilidade | RFs relacionados |
|---|---|---|
| **Catálogo** | Categorias e produtos (listagem, busca, filtro) | RF01–RF05, RF18, RF19 |
| **Carrinho** | Itens selecionados pelo cliente antes do checkout | RF06–RF08 |
| **Endereço** | Cadastro e seleção de endereços de entrega | RF09–RF11 |
| **Pedido** | Criação, checkout, status e acompanhamento do pedido | RF12–RF17, RF20 |

> Cliente e autenticação ainda não têm requisito definido (ver pendência em `02-requisitos`) — módulo de **Usuário** será adicionado quando essa decisão for tomada.

---

## 4. Modelo de dados (rascunho inicial)

Entidades previstas com base no catálogo de telas e requisitos. **Sujeito a revisão** conforme o modelo evoluir.

```
Categoria
 - id
 - nome

Produto
 - id
 - nome
 - descricao
 - preco
 - foto_url
 - categoria_id (FK -> Categoria)

Endereco
 - id
 - rua
 - numero
 - complemento
 - bairro
 - cidade
 - estado
 - cliente_id (FK -> Cliente, se houver módulo de usuário)

Pedido
 - id
 - status (ex: CRIADO, CONFIRMADO, EM_ENTREGA, ENTREGUE)
 - forma_pagamento (CARTAO, PIX, DINHEIRO)
 - endereco_id (FK -> Endereco)
 - valor_entrega
 - valor_total
 - data_criacao
 - previsao_entrega

ItemPedido
 - id
 - pedido_id (FK -> Pedido)
 - produto_id (FK -> Produto)
 - quantidade
 - preco_unitario
```

---

## 5. Decisões de arquitetura (ADRs resumidos)

| Decisão | Justificativa |
|---|---|
| Sem gateway de pagamento no MVP | Reduz complexidade e escopo; pagamento é feito na entrega (RN01). |
| API REST (não GraphQL) | Simplicidade, aderência ao padrão usado no bootcamp e facilidade de consumo pelo frontend mobile. |
| PostgreSQL | Banco relacional robusto, gratuito, e adequado ao volume de dados de um comércio local. |
| Sem microsserviços | Escopo de MVP não justifica a complexidade operacional; monólito modular é suficiente. |

---

## 6. Pendências

- [ ] Definir tecnologia do frontend (ver README — "a definir").
- [ ] Definir se haverá autenticação/módulo de usuário (impacta modelo de dados: `Cliente`).
- [ ] Definir hospedagem/deploy (ex: Render, Railway, VPS) — ainda não mencionado no README.
- [ ] Definir estratégia de armazenamento de imagens dos produtos (ex: S3, Cloudinary, ou pasta local no MVP).
- [ ] Detalhar diagrama de entidade-relacionamento (DER) formal após validação do modelo acima.