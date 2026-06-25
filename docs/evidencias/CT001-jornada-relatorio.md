# Relatório de Execução — CT001 (Jornada Completa)

**Caso de teste:** CT001 - Jornada Completa: Pedido "Para Comer Aqui"  
**Sistema:** McBugs - Totem de Autoatendimento  
**Data de execução:** 25/06/2026  
**Executor:** QA Engineer (Playwright MCP — Chrome Headed)  
**Ambiente:** http://localhost:3002/ (Vite dev server)  
**Documento de referência:** `docs/casos-de-testes-jornada.md`

---

## Status do cenário

✅ **Passou**

---

## Passos executados

| Passo | Ação | Resultado | Status |
|-------|------|-----------|--------|
| 1 | Acessar URL raiz (`/`) | Página inicial com opções "Para comer aqui" e "Para levar" | ✅ |
| 2 | Clicar em "Para comer aqui" | `orderType=dine-in` no localStorage; redirecionamento para `/menu` | ✅ |
| 3 | Verificar página do menu | Categorias Lanches, Fritas, Bebidas, Sobremesas e produtos visíveis | ✅ |
| 4 | Clicar em Big Mock | Redirecionamento para `/product/big-mock` | ✅ |
| 5 | Verificar detalhes do produto | Imagem, nome, preço (R$ 39,90), descrição e ingredientes exibidos | ✅ |
| 6 | Aumentar quantidade para 2 | Quantidade = 2; botão atualizado para "Quero • R$ 79,80" | ✅ |
| 7 | Clicar em "Quero • R$ 79,80" | Produto adicionado (qty 2); redirecionamento para `/menu` | ✅ |
| 8 | Verificar barra de carrinho | Total R$ 79,80 / 2 itens; botão "Ver pedido" visível | ✅ |
| 9 | Clicar em Coca-Crash (aba Bebidas) | Redirecionamento para `/product/coca-crash` | ✅ |
| 10 | Clicar em "Quero • R$ 5,90" | Coca-Crash adicionado; redirecionamento para `/menu` | ✅ |
| 11 | Clicar em "Ver pedido" | Redirecionamento para `/cart` | ✅ |
| 12 | Verificar itens no carrinho | Big Mock (2x, R$ 79,80) e Coca-Crash (1x, R$ 5,90) listados | ✅ |
| 13 | Verificar total do pedido | Total R$ 85,70 calculado corretamente | ✅ |
| 14 | Clicar em "Finalizar pedido" | Drawer aberto solicitando nome do cliente | ✅ |
| 15 | Inserir "João Silva" | Nome preenchido no campo | ✅ |
| 16 | Clicar em "Finalizar" | Mensagem "enviando a cozinha...."; pedido criado (status pending, dine-in) | ✅ |
| 17 | Verificar redirecionamento | Redirecionamento para `/payment`; carrinho vazio | ✅ |
| 18 | Verificar página de pagamento | Pedido #2, total R$ 85,70; PIX, Débito e Crédito disponíveis | ✅ |
| 19 | Clicar em PIX | Método atualizado; redirecionamento para `/payment/pix/confirm` | ✅ |
| 20 | Verificar página de confirmação | Nº pedido, total, PIX, instruções, cliente, tipo "Comer no local", itens e mensagem de aguardar chamado | ✅ |
| 21 | Verificar pedido no banco | Dados corretos no Supabase (ver detalhes abaixo) | ✅ |
| 22 | Clicar em "Fazer Novo Pedido" | Estado limpo; redirecionamento para `/` | ✅ |

---

## Critérios de aceitação

| Critério | Resultado | Status |
|----------|-----------|--------|
| Pedido criado com status `pending` e tipo `dine-in` | Confirmado no Supabase | ✅ |
| Dados salvos corretamente (itens, total, tipo, cliente, pagamento) | Confirmado | ✅ |
| Carrinho limpo após criação do pedido | Confirmado | ✅ |
| Mensagem específica dine-in na confirmação | "Após o pagamento, aguarde ser chamado pelo número do seu pedido." | ✅ |
| Fluxo completo sem interrupções | 22/22 passos concluídos | ✅ |
| localStorage atualizado em cada etapa | Validado em passos 2, 7, 10, 16, 22 | ✅ |
| Sem erros no console | 0 erros (2 warnings React Router v7) | ✅ |

---

## Verificação no banco de dados (Passo 21)

Pedido **#2** consultado via Supabase REST API:

| Campo | Valor esperado | Valor obtido |
|-------|----------------|--------------|
| `customer_name` | João Silva | João Silva |
| `order_type` | dine-in | dine-in |
| `payment_method` | pix | pix |
| `status` | pending | pending |
| `total` | 85.70 | 85.70 |
| `items` | Big Mock (2x) + Coca-Crash (1x) | JSON com 2 itens corretos |

---

## Evidências (screenshots)

| Passo | Arquivo |
|-------|---------|
| 1 | [passo-01-pagina-inicial.png](./CT001-jornada/passo-01-pagina-inicial.png) |
| 2 | [passo-02-para-comer-aqui.png](./CT001-jornada/passo-02-para-comer-aqui.png) |
| 3 | [passo-03-pagina-menu.png](./CT001-jornada/passo-03-pagina-menu.png) |
| 4 | [passo-04-produto-big-mock.png](./CT001-jornada/passo-04-produto-big-mock.png) |
| 5 | [passo-05-detalhes-produto.png](./CT001-jornada/passo-05-detalhes-produto.png) |
| 6 | [passo-06-quantidade-2.png](./CT001-jornada/passo-06-quantidade-2.png) |
| 7 | [passo-07-adicionar-big-mock.png](./CT001-jornada/passo-07-adicionar-big-mock.png) |
| 8 | [passo-08-barra-carrinho.png](./CT001-jornada/passo-08-barra-carrinho.png) |
| 9 | [passo-09-produto-coca-crash.png](./CT001-jornada/passo-09-produto-coca-crash.png) |
| 10 | [passo-10-adicionar-coca-crash.png](./CT001-jornada/passo-10-adicionar-coca-crash.png) |
| 11 | [passo-11-ver-pedido.png](./CT001-jornada/passo-11-ver-pedido.png) |
| 12 | [passo-12-itens-carrinho.png](./CT001-jornada/passo-12-itens-carrinho.png) |
| 13 | [passo-13-total-pedido.png](./CT001-jornada/passo-13-total-pedido.png) |
| 14 | [passo-14-finalizar-pedido-drawer.png](./CT001-jornada/passo-14-finalizar-pedido-drawer.png) |
| 15 | [passo-15-nome-cliente.png](./CT001-jornada/passo-15-nome-cliente.png) |
| 16 | [passo-16-pedido-criado.png](./CT001-jornada/passo-16-pedido-criado.png) |
| 17 | [passo-17-redirecionamento-payment.png](./CT001-jornada/passo-17-redirecionamento-payment.png) |
| 18 | [passo-18-pagina-pagamento.png](./CT001-jornada/passo-18-pagina-pagamento.png) |
| 19 | [passo-19-selecionar-pix.png](./CT001-jornada/passo-19-selecionar-pix.png) |
| 20 | [passo-20-confirmacao-pix.png](./CT001-jornada/passo-20-confirmacao-pix.png) |
| 21 | [passo-21-verificacao-banco.png](./CT001-jornada/passo-21-verificacao-banco.png) |
| 22 | [passo-22-novo-pedido.png](./CT001-jornada/passo-22-novo-pedido.png) |

---

## Problemas encontrados

Nenhum bug funcional identificado durante a jornada.

---

## Sugestões de melhoria (opcional)

- Suprimir warnings do React Router v7 future flags no console durante testes.
- No passo 9, foi necessário navegar para a aba "Bebidas" antes de selecionar Coca-Crash (comportamento esperado, pois o produto não está na categoria padrão "Lanches").

---

**Conclusão:** A jornada completa "Para Comer Aqui" foi executada com sucesso. Todos os 22 passos e critérios de aceitação foram atendidos.
