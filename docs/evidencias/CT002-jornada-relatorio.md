# Relatório de Execução — CT002 (Jornada Completa)

**Caso de teste:** CT002 - Jornada Completa: Pedido "Para Levar"  
**Sistema:** McBugs - Totem de Autoatendimento  
**Data de execução:** 30/06/2026  
**Executor:** QA Engineer (Playwright MCP — Chrome Headed)  
**Ambiente:** http://localhost:3000/ (Vite dev server)  
**Documento de referência:** `docs/casos-de-testes-jornada.md`

---

## Status do cenário

✅ **Passou**

---

## Passos executados

| Passo | Ação | Resultado | Status |
|-------|------|-----------|--------|
| 1 | Acessar URL raiz (`/`) | Página inicial com opções "Para comer aqui" e "Para levar" | ✅ |
| 2 | Clicar em "Para levar" | `orderType=takeaway` no localStorage; redirecionamento para `/menu` | ✅ |
| 3 | Verificar página do menu | Categorias Lanches, Fritas, Bebidas, Sobremesas e produtos visíveis | ✅ |
| 4 | Clicar na aba "Fritas" | Apenas produtos de Fritas exibidos (sem Lanches) | ✅ |
| 5 | Clicar em Batatas Full Stack | Redirecionamento para `/product/batatas-fullstack` | ✅ |
| 6 | Verificar detalhes do produto | Imagem, nome, preço (R$ 10,90), descrição e ingredientes exibidos | ✅ |
| 7 | Manter quantidade em 1 | Quantidade = 1; botão "Quero • R$ 10,90" | ✅ |
| 8 | Clicar em "Quero • R$ 10,90" | Produto adicionado; redirecionamento para `/menu` | ✅ |
| 9 | Clicar na aba "Bebidas" | Apenas produtos de Bebidas exibidos | ✅ |
| 10 | Clicar em Fanta Warning | Redirecionamento para `/product/fanta-warning` | ✅ |
| 11 | Aumentar quantidade para 3 | Quantidade = 3; botão "Quero • R$ 17,70" | ✅ |
| 12 | Clicar em "Quero • R$ 17,70" | Fanta Warning (qty 3) adicionado; redirecionamento para `/menu` | ✅ |
| 13 | Verificar barra de carrinho | Total R$ 28,60 / 4 itens; botão "Ver pedido" visível | ✅ |
| 14 | Clicar em "Ver pedido" | Redirecionamento para `/cart` | ✅ |
| 15 | Verificar itens no carrinho | Batatas Full Stack (1x) e Fanta Warning (3x) listados | ✅ |
| 16 | Aumentar quantidade de item no carrinho | Batatas Full Stack incrementada para 2x (subtotal R$ 21,80) | ✅ |
| 17 | Verificar total do pedido | Total R$ 39,50 calculado corretamente | ✅ |
| 18 | Clicar em "Finalizar pedido" | Drawer aberto solicitando nome do cliente | ✅ |
| 19 | Inserir "Maria Santos" | Nome preenchido no campo | ✅ |
| 20 | Clicar em "Finalizar" | Mensagem "enviando a cozinha...."; pedido criado (pending, takeaway) | ✅ |
| 21 | Verificar redirecionamento | Redirecionamento para `/payment`; carrinho vazio | ✅ |
| 22 | Verificar página de pagamento | Pedido #3, total R$ 39,50; PIX, Débito e Crédito disponíveis | ✅ |
| 23 | Clicar em "Cartão de Crédito" | Método atualizado; redirecionamento para `/payment/credit/confirm` | ✅ |
| 24 | Verificar página de confirmação | Nº pedido, total, Crédito, instruções, cliente, tipo "Para levar", itens e data | ✅ |
| 25 | Verificar ausência de mensagem de aguardar | Sem mensagem sobre aguardar ser chamado | ✅ |
| 26 | Verificar pedido no banco | Dados corretos no Supabase (ver detalhes abaixo) | ✅ |
| 27 | Clicar em "Fazer Novo Pedido" | Estado limpo; redirecionamento para `/` | ✅ |

---

## Critérios de aceitação

| Critério | Resultado | Status |
|----------|-----------|--------|
| Pedido criado com status `pending` e tipo `takeaway` | Confirmado no Supabase | ✅ |
| Dados salvos corretamente | Confirmado | ✅ |
| Carrinho limpo após criação do pedido | Confirmado | ✅ |
| Confirmação sem mensagem de aguardar chamado | Confirmado (diferente de dine-in) | ✅ |
| Fluxo completo sem interrupções | 27/27 passos concluídos | ✅ |
| localStorage atualizado em cada etapa | Validado nos passos 2, 8, 12, 20, 27 | ✅ |
| Navegação entre categorias e ajuste no carrinho | Confirmado nos passos 4, 9, 16 | ✅ |
| Sem erros no console | 0 erros (2 warnings React Router v7) | ✅ |

---

## Verificação no banco de dados (Passo 26)

Pedido **#3** consultado via Supabase REST API:

| Campo | Valor esperado | Valor obtido |
|-------|----------------|--------------|
| `customer_name` | Maria Santos | Maria Santos |
| `order_type` | takeaway | takeaway |
| `payment_method` | credit | credit |
| `status` | pending | pending |
| `total` | 39.50 | 39.50 |
| `items` | Batatas Full Stack (2x) + Fanta Warning (3x) | JSON com 2 itens corretos |

---

## Evidências (screenshots)

| Passo | Arquivo |
|-------|---------|
| 1 | [passo-01-pagina-inicial.png](./CT002-jornada/passo-01-pagina-inicial.png) |
| 2 | [passo-02-para-levar.png](./CT002-jornada/passo-02-para-levar.png) |
| 3 | [passo-03-pagina-menu.png](./CT002-jornada/passo-03-pagina-menu.png) |
| 4 | [passo-04-aba-fritas.png](./CT002-jornada/passo-04-aba-fritas.png) |
| 5 | [passo-05-produto-batatas-fullstack.png](./CT002-jornada/passo-05-produto-batatas-fullstack.png) |
| 6 | [passo-06-detalhes-produto.png](./CT002-jornada/passo-06-detalhes-produto.png) |
| 7 | [passo-07-quantidade-1.png](./CT002-jornada/passo-07-quantidade-1.png) |
| 8 | [passo-08-adicionar-batatas.png](./CT002-jornada/passo-08-adicionar-batatas.png) |
| 9 | [passo-09-aba-bebidas.png](./CT002-jornada/passo-09-aba-bebidas.png) |
| 10 | [passo-10-produto-fanta-warning.png](./CT002-jornada/passo-10-produto-fanta-warning.png) |
| 11 | [passo-11-quantidade-3.png](./CT002-jornada/passo-11-quantidade-3.png) |
| 12 | [passo-12-adicionar-fanta.png](./CT002-jornada/passo-12-adicionar-fanta.png) |
| 13 | [passo-13-barra-carrinho.png](./CT002-jornada/passo-13-barra-carrinho.png) |
| 14 | [passo-14-ver-pedido.png](./CT002-jornada/passo-14-ver-pedido.png) |
| 15 | [passo-15-itens-carrinho.png](./CT002-jornada/passo-15-itens-carrinho.png) |
| 16 | [passo-16-aumentar-item-carrinho.png](./CT002-jornada/passo-16-aumentar-item-carrinho.png) |
| 17 | [passo-17-total-pedido.png](./CT002-jornada/passo-17-total-pedido.png) |
| 18 | [passo-18-finalizar-drawer.png](./CT002-jornada/passo-18-finalizar-drawer.png) |
| 19 | [passo-19-nome-cliente.png](./CT002-jornada/passo-19-nome-cliente.png) |
| 20 | [passo-20-pedido-criado.png](./CT002-jornada/passo-20-pedido-criado.png) |
| 21 | [passo-21-redirecionamento-payment.png](./CT002-jornada/passo-21-redirecionamento-payment.png) |
| 22 | [passo-22-pagina-pagamento.png](./CT002-jornada/passo-22-pagina-pagamento.png) |
| 23 | [passo-23-selecionar-credito.png](./CT002-jornada/passo-23-selecionar-credito.png) |
| 24 | [passo-24-confirmacao-credito.png](./CT002-jornada/passo-24-confirmacao-credito.png) |
| 25 | [passo-25-sem-mensagem-aguardar.png](./CT002-jornada/passo-25-sem-mensagem-aguardar.png) |
| 26 | [passo-26-verificacao-banco.png](./CT002-jornada/passo-26-verificacao-banco.png) |
| 27 | [passo-27-novo-pedido.png](./CT002-jornada/passo-27-novo-pedido.png) |

---

## Problemas encontrados

Nenhum bug funcional identificado durante a jornada.

---

## Sugestões de melhoria (opcional)

- Suprimir warnings do React Router v7 future flags no console durante testes.

---

**Conclusão:** A jornada completa "Para Levar" foi executada com sucesso. Todos os 27 passos e critérios de aceitação foram atendidos.
