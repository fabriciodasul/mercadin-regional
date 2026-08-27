# 02 - Requisitos

Levantamento de requisitos do **Mercadin Regional**, com base no escopo definido no README e no fluxo de telas mapeado em `docs/03-ux-ui`.

---

## 1. Atores

| Ator | Descrição |
|---|---|
| **Cliente** | Usuário final que acessa o catálogo, monta o pedido e acompanha a entrega. |
| **Comerciante (mercado)** | Responsável por gerenciar produtos, categorias e confirmar/processar pedidos recebidos. |

---

## 2. Requisitos Funcionais (RF)

### Catálogo e navegação
- **RF01** — O sistema deve exibir uma tela inicial (Home) com categorias de produtos e itens em destaque.
- **RF02** — O sistema deve permitir a busca de produtos por nome.
- **RF03** — O sistema deve permitir a navegação por categoria (ex: Hortifruti, Regional, Frutas).
- **RF04** — O sistema deve permitir ordenar/filtrar produtos dentro de uma categoria.
- **RF05** — O sistema deve exibir uma tela de detalhe do produto com foto, descrição e valor.

### Carrinho
- **RF06** — O sistema deve permitir adicionar produtos ao carrinho.
- **RF07** — O sistema deve exibir um resumo do carrinho com itens, descrição e preço individual.
- **RF08** — O sistema deve permitir remover ou alterar a quantidade de itens no carrinho *(a confirmar no wireframe — não visível na tela atual)*.

### Entrega
- **RF09** — O sistema deve permitir o cadastro de um endereço de entrega.
- **RF10** — O sistema deve permitir a seleção de um endereço já cadastrado.
- **RF11** — O sistema deve permitir o cadastro de múltiplos endereços ("+ Novo endereço").

### Checkout e pedido
- **RF12** — O sistema deve exibir um resumo do pedido (quantidade de itens, valor de entrega, total) antes da confirmação.
- **RF13** — O sistema deve permitir a escolha da forma de pagamento (Cartão de crédito, Pix ou Dinheiro), sendo o pagamento efetivado apenas na entrega (sem gateway de pagamento no MVP).
- **RF14** — O sistema deve gerar uma confirmação de pedido ao cliente após o checkout.
- **RF15** — O sistema deve exibir uma previsão de entrega na tela de confirmação.
- **RF16** — O sistema deve permitir o acompanhamento do status do pedido ("Acompanhar pedido").
- **RF17** — O sistema deve notificar o comerciante sobre o novo pedido (via WhatsApp/telefone no MVP, conforme README).

### Gestão (lado comerciante) — *a validar escopo do MVP*
- **RF18** — O sistema deve permitir o cadastro/edição de produtos (nome, descrição, preço, categoria, foto).
- **RF19** — O sistema deve permitir o cadastro/edição de categorias.
- **RF20** — O sistema deve permitir ao comerciante visualizar e confirmar pedidos recebidos.

---

## 3. Requisitos Não Funcionais (RNF)

| ID | Requisito |
|---|---|
| **RNF01** | O sistema deve ter interface responsiva, com prioridade para uso mobile (conforme wireframe). |
| **RNF02** | O backend deve ser desenvolvido em Java com Spring Boot. |
| **RNF03** | O banco de dados deve ser PostgreSQL. |
| **RNF04** | O sistema deve possuir cobertura de testes automatizados (JUnit, Mockito) para as regras de negócio principais. |
| **RNF05** | As APIs devem ser testáveis via Postman/RestAssured, com documentação de endpoints. |
| **RNF06** | O tempo de resposta das telas de catálogo (busca/listagem) deve ser adequado para uso em conexões móveis mais lentas, comuns em regiões do interior. |
| **RNF07** | O sistema não deve armazenar dados sensíveis de pagamento, já que o pagamento não é processado dentro do app no MVP. |

---

## 4. Regras de negócio

- **RN01** — O pagamento é sempre realizado no momento da entrega (dinheiro, cartão ou Pix na hora), nunca via app.
- **RN02** — Um pedido só é considerado confirmado após validação/aceite (implícito ou explícito) do comerciante.
- **RN03** — O valor da entrega é somado ao total do pedido no checkout.
- **RN04** — Cada cliente pode ter mais de um endereço cadastrado, mas apenas um selecionado por pedido.

---

## 5. Fora de escopo (MVP)

- Pagamento integrado dentro do app (gateway de pagamento).
- Rastreamento de entrega em tempo real (geolocalização do entregador).
- Sistema de avaliação de produtos/pedidos.
- Múltiplos vendedores/lojas na mesma plataforma (é um catálogo de **um único comércio**).

---

## 6. Pendências / a validar com o cliente (comerciante)

- [ ] Definir se haverá login/cadastro de cliente ou se o pedido pode ser feito sem conta.
- [ ] Definir se o comerciante terá um painel administrativo (web) ou se a gestão de produtos será manual (ex: direto no banco/admin simples).
- [ ] Confirmar RF08 (edição de itens no carrinho) — não identificado no wireframe atual.
- [ ] Definir regras de disponibilidade/estoque dos produtos (ex: produto esgotado).
- [ ] Definir área de cobertura de entrega (bairros atendidos).