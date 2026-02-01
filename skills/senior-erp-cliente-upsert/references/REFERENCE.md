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

O artigo descreve dois caminhos:
1) Capturar token via DevTools (em chamadas que tenham `authorization`).
2) Obter via Postman/cliente HTTP (POST no endpoint de login informado no artigo):
   `https://platform.senior.com.br/t/senior.com.br/bridge/1.0/rest/platform/authentication/actions/login`

Importante: endpoints e caminhos podem variar por tenant/ambiente. Parametrize sempre.

## Guia de API (boas praticas)

- https://dev.senior.com.br/documentacao/guia-de-api/

Use como referencia para consistencia de requests/responses, padrao de erros e convencoes.

## Convencoes recomendadas (padrao interno)

### Parametrizacao (nao hardcode)

Toda skill que chama API deve aceitar via `context`:
- `base_url`
- `tenant` (se aplicavel)
- `client_id`
- token (`access_token`) e/ou metodo de obtencao (preferir secrets/variaveis do agente)

### Seguranca e compliance

- Nunca logar token em claro.
- Evitar registrar payload com PII (CPF/CNPJ, emails, telefones) em logs; quando inevitavel, mascarar.
- Para operacoes de alto risco, exigir confirmacao explicita antes da mutacao.

### Resiliencia

- Definir timeout por request.
- Implementar retry com backoff exponencial para falhas transientes (timeouts, 429, 5xx).
- Se houver paginacao, iterar de forma controlada e com limites.

### Idempotencia e deduplicacao (jobs mutaveis)

- Antes de criar recursos (POST), consultar se ja existe (quando possivel) e evitar duplicidade.
- Se o fluxo suportar chave idempotente, usar (ou simular via armazenamento de `external_id`).
- Em reprocessamentos, preferir atualizar o registro encontrado em vez de recriar.
