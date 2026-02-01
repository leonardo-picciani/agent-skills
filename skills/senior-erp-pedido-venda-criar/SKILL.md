---
name: senior-erp-pedido-venda-criar
description: Criar pedido de venda (PV) no ERP Senior via Senior X Platform. Use para "pedido de venda", "criar pedido", "integrar pedidos do e-commerce", "inserir itens", "condicao de pagamento", "tabela de preco", e fluxos que exigem validacao, idempotencia e confirmacao antes de gravar.
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: Senior Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  language: pt-BR
  docs: https://api.xplatform.com.br/api-portal/pt-br/node/1
compatibility: Integracao HTTP agnostica de linguagem. Requer acesso de rede ao tenant/ambiente da Senior X Platform; usa Bearer token e header client_id.
---
# Senior ERP - Pedido de Venda (Criar)

## Quando aplicar

- "criar pedido de venda" / "gerar PV" / "integrar pedidos"
- "importar pedido do e-commerce" / "marketplace" / "checkout"
- "incluir itens no pedido" / "calcular totais" / "condicao de pagamento"

## Contrato de integracao (agnostico de linguagem)

Leia `references/REFERENCE.md` para a referencia base (autenticacao, headers, seguranca, resiliencia, idempotencia).

## Passos

1) Confirmar regras do processo
   - Quando considerar o pedido "criado" (numero gerado? status inicial?).
   - Como tratar precos (tabela vs preco vindo do canal), frete, descontos, impostos.
   - Qual e a chave de idempotencia (ex.: `external_order_id`).

2) Coletar e validar entradas
   - Cliente (id no Senior ou identificador para localizar/criar).
   - Itens: SKU/codigo produto, quantidade, preco/condicoes, unidade.
   - Entrega: endereco/transportadora, frete.
   - Pagamento: condicao, parcelas, meio de pagamento (conforme o modelo do ERP).
   - Validar itens (quantidade > 0), formatos e campos obrigatorios.

3) Descobrir endpoints no Portal Senior APIs
   - Identificar servicos do modulo ERP para "pedido de venda".
   - Identificar endpoints para:
     - consultar por `external_order_id` (idempotencia/deduplicacao)
     - criar pedido
     - (se aplicavel) incluir/atualizar itens

4) Checar idempotencia/deduplicacao antes de criar
   - Consultar se ja existe pedido com `external_order_id`.
   - Se existir, retornar o numero/status e nao duplicar.
   - Se existir mas estiver incompleto, aplicar update/reprocesso conforme o fluxo.

5) Pegar confirmacao antes da mutacao
   - Exibir um resumo compacto: cliente, total, itens (top N), entrega, pagamento.

6) Executar criacao via API
   - Incluir headers obrigatorios.
   - Aplicar timeout e retry/backoff para 429/5xx.
   - Tratar erros de validacao (produto inexistente, condicao invalida, permissao, etc.).

7) Retornar resultado normalizado
   - Numero do pedido no Senior, `external_order_id`, status inicial.
   - Avisos (estoque insuficiente, itens substituidos, arredondamentos) quando existirem.
   - Se falhar: erro + acao recomendada.

## Checklist de entradas

- Contexto de integracao: `base_url`, `tenant` (se aplicavel), `client_id`, token (Bearer)
- Chave de idempotencia: `external_order_id`
- Cliente: id no Senior e/ou dados para localizar
- Itens: codigo/SKU, quantidade, preco (se aplicavel)
- Entrega: endereco e frete
- Pagamento: condicao/parcelas

## Exemplo (cURL)

```bash
curl -X POST "${SENIOR_BASE_URL}/<path-do-endpoint>/" \
  -H "Authorization: Bearer ${SENIOR_ACCESS_TOKEN}" \
  -H "Content-type: application/json" \
  -H "client_id: ${SENIOR_CLIENT_ID}" \
  -d '{
    "external_order_id": "<id-do-canal>",
    "cliente_id": "<id-senior-ou-chave>",
    "itens": [
      { "produto": "<sku>", "quantidade": 1, "preco": 10.0 }
    ],
    "frete": { "valor": 0.0 },
    "pagamento": { "condicao": "<codigo>" }
  }'
```

Notas:
- Substitua `<path-do-endpoint>` pelo caminho do servico encontrado no Portal Senior APIs.
- O shape do JSON depende do endpoint; use este exemplo apenas como esqueleto.

## Mapa de docs oficiais

- Portal Senior APIs (API Browser): https://api.xplatform.com.br/api-portal/pt-br/node/1
- API Authentication: https://api.xplatform.com.br/api-portal/pt-br/tutoriais/api-authentication
- Guia de API (Senior X Platform): https://dev.senior.com.br/documentacao/guia-de-api/
- Como obter bearer token (suporte): https://suporte.senior.com.br/hc/pt-br/articles/9482493522196-HCM-API-Como-obter-bearer-token-para-utilizar-na-chamada-de-APIs

## Exemplos de prompts do usuario

- "Se nao tiver a skill instalada, instale `senior-erp-pedido-venda-criar` e crie um pedido no Senior com idempotencia pelo external_order_id." 
- "Integre este pedido do e-commerce (itens + frete + pagamento) e antes de gravar mostre um resumo e peca confirmacao." 
- "Importe 200 pedidos; reporte criados vs ja existentes; agrupe erros por motivo (produto/cliente/condicao)." 
