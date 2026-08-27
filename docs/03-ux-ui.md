# 03 - UX/UI

Documentação de fluxo de usuário e telas do **Mercadin Regional**, com base no wireframe desenvolvido no Figma.

> Link do Figma: [Mercadin Regional - Wireframe](https://www.figma.com/design/4i4oMIvRmdMNc43roCw6Yl/Sem-título)

---

## 1. Visão geral do fluxo

O fluxo foi desenhado para dispositivos mobile e cobre a jornada completa do cliente, desde a navegação pelo catálogo até a confirmação do pedido:

```
Home → Catálogo → Detalhe do produto → Carrinho → Entrega → Checkout → Pedido confirmado
```

Como o MVP não possui pagamento integrado, o fluxo termina com a confirmação do pedido no app e a comunicação (envio/confirmação) acontece via WhatsApp/telefone com o mercado.

---

## 2. Catálogo de telas

### 2.1 Home
Tela inicial com ponto de entrada para navegação.

**Componentes:**
- Barra de busca
- Banner de destaque
- Categorias (navegação rápida por ícone: ex. Frutas, Regional, Hortifruti)
- Lista/grid de produtos em destaque

---

### 2.2 Catálogo
Listagem de produtos filtrada por categoria.

**Componentes:**
- Botão de voltar + título da categoria (ex: "Hortifruti")
- Campo de busca dentro da categoria
- Filtro
- Ordenação ("Ordenar por")
- Grid de produtos (2 colunas)

---

### 2.3 Detalhe do produto
Exibe as informações completas de um item antes da compra.

**Componentes:**
- Botão de voltar + nome da categoria
- Foto do produto (destaque)
- Descrição do produto
- Valor (preço por unidade/kg)

---

### 2.4 Carrinho ("Meu carrinho")
Resumo dos itens adicionados antes de seguir para entrega.

**Componentes:**
- Botão de voltar + título "Meu carrinho"
- Lista de itens: foto, nome, descrição curta, preço
- Botão "Continuar"

> ⚠️ **Ajuste pendente no Figma:** essa tela está nomeada como "Detalhe do produto" no painel de camadas — renomear para "Carrinho" para evitar confusão com a tela 2.3.

---

### 2.5 Entrega
Seleção/cadastro do endereço de entrega.

**Componentes:**
- Botão de voltar + título "Endereço de entrega"
- Card de endereço cadastrado (rua, bairro, cidade/UF, complemento)
- Ação "+ Novo endereço"
- Botão "Continuar"

---

### 2.6 Checkout
Revisão final do pedido antes da confirmação.

**Componentes:**
- Botão de voltar + título "Checkout"
- Resumo do pedido: nº de itens, valor de entrega, total
- Card de endereço de entrega (reexibido)
- Formas de pagamento: Cartão de crédito / Pix / Dinheiro (seleção única)
- Aviso: "Pagamento somente na hora da entrega"
- Botão "Continuar"

---

### 2.7 Pedido confirmado
Tela de sucesso após finalização do pedido.

**Componentes:**
- Ícone/indicador "Verificado"
- Previsão de entrega
- Botão "Acompanhar pedido"
- Botão "Continuar"

---

## 3. Componentes recorrentes

| Componente | Onde aparece | Observação |
|---|---|---|
| Botão "Continuar" | Carrinho, Entrega, Checkout | Ação primária, fixada na base da tela |
| Botão de voltar (`<`) | Catálogo, Detalhe do produto, Carrinho, Entrega, Checkout | Padrão de navegação entre telas |
| Card de endereço | Entrega, Checkout | Reutilizado — mesmo componente em dois contextos |
| Card de produto | Home, Catálogo, Carrinho | Varia a quantidade de informação exibida por contexto |

---

## 4. Decisões de design (MVP)

- **Sem pagamento integrado**: pagamento é escolhido apenas como preferência (Cartão/Pix/Dinheiro) e efetivado na entrega — reduz complexidade técnica do MVP.
- **Confirmação via WhatsApp/telefone**: o app não substitui o contato direto com o mercado, apenas organiza o pedido.
- **Fluxo linear**: cada tela tem uma única ação principal de avanço ("Continuar"), reduzindo decisões e fricção para o público-alvo (clientes locais, nem sempre familiarizados com apps de compra).

---

## 5. Pendências / próximos passos

- [ ] Renomear camada "Detalhe do produto" (carrinho) no Figma
- [ ] Definir estados vazios (carrinho vazio, catálogo sem resultados de busca)
- [ ] Definir tela/estado de erro (ex: falha ao confirmar pedido)
- [ ] Definir paleta de cores e tipografia (design visual ainda não aplicado sobre o wireframe)
- [ ] Especificar tela "Acompanhar pedido" (referenciada no botão da tela de confirmação, mas ainda não desenhada)
- [ ] Exportar prints/specs das telas em alta resolução para referência de handoff