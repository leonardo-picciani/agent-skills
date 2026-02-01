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

## Guia de API (boas praticas)

- https://dev.senior.com.br/documentacao/guia-de-api/

## Convencoes recomendadas (padrao interno)

### Parametrizacao

Aceitar via `context`: `base_url`, `tenant` (se aplicavel), `client_id`, token (Bearer).

### Seguranca

- Nunca logar token em claro.
- Evitar expor dados financeiros sensiveis em logs.
- Ao retornar resultados, preferir saidas compactas e omitir campos desnecessarios.

### Resiliencia

- Timeout por request.
- Retry com backoff para 429/5xx.
- Para consultas grandes, paginar com limites.
