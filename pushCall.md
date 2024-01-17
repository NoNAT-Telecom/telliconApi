# Manual do Webhook - Eventos de Chamadas

## Endpoint do Webhook: `/webhook/eventTellicon`

A API funciona como um webhook para receber eventos relacionados a chamadas. Abaixo estão os detalhes sobre os dados que serão enviados ao webhook.

### 1. Formato dos Dados Recebidos

Ao receber um evento, o webhook deve esperar um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "type": "pushCall",
    "src": "9001",
    "client": 505,
    "building": 121,
    "apt": 1001,
    "dateTime": 1705338959
  }
}
