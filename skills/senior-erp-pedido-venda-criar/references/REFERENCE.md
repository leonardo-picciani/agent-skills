# Senior X Platform - Referencia base (para integracao via APIs)

Este arquivo contem a referencia base (pt-BR) para integrar com APIs do ecossistema Senior X Platform.
Use como contrato minimo para autenticacao, headers, seguranca e resiliencia.

## Portal oficial de APIs (ponto de partida)

- Portal "Senior APIs" (documentacao, tutoriais e API Browser):
  https://api.xplatform.com.br/api-portal/pt-br/node/1

## Autenticacao e headers obrigatorios

Tutorial oficial: https://api.xplatform.com.br/api-portal/pt-br/tutoriais/api-authentication

Em chamadas autenticadas, incluir:
- `Authorization: Bearer {access_token}`
- `Content-type: application/json`
- `client_id: {client_id_da_aplicacao}`

Observacao: endpoints de login (ex.: `login`, `loginMFA`, `loginWithKey`) podem nao exigir token.

## Como obter bearer token (suporte / exemplo)

Artigo: https://suporte.senior.com.br/hc/pt-br/articles/9482493522196-HCM-API-Como-obter-bearer-token-para-utilizar-na-chamada-de-APIs

Exemplo de endpoint de login citado no artigo:
`https://platform.senior.com.br/t/senior.com.br/bridge/1.0/rest/platform/authentication/actions/login`

Importante: endpoints e caminhos podem variar por tenant/ambiente. Parametrize sempre.

## Guia de API (boas praticas)

- https://dev.senior.com.br/documentacao/guia-de-api/

## Convencoes recomendadas (padrao interno)

### Parametrizacao (nao hardcode)

Toda skill que chama API deve aceitar via `context`:
- `base_url`
- `tenant` (se aplicavel)
- `client_id`
- token (`access_token`) e/ou metodo de obtencao (preferir secrets/variaveis do agente)

### Seguranca e compliance

- Nunca logar token em claro.
- Evitar registrar payload com PII em logs; quando inevitavel, mascarar.
- Para operacoes mutaveis, pedir confirmacao explicita antes de gravar.

### Resiliencia

- Timeout por request.
- Retry com backoff exponencial para falhas transientes (timeouts, 429, 5xx).
- Se o endpoint for assincorno (job), implementar consulta de status conforme a documentacao do servico.

### Idempotencia e deduplicacao (pedidos)

- Definir `external_order_id` como chave primaria do job (canal -> Senior).
- Sempre consultar antes de criar para evitar duplicidade.
- Em reprocesso, preferir atualizar/reconciliar em vez de recriar.
