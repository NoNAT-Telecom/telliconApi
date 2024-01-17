# Manual do Webhook - Eventos de Chamadas

## Endpoint: `http(s)://<hostDoParceiro>/eventTellicon`

A API funciona como um webhook para enviar eventos relacionados a chamadas. Abaixo estão os detalhes sobre os dados que serão enviados ao parceiro.

### 1. Requisitos do Webhook
  - Método HTTP: POST
  - Cabeçalho Obrigatório: authTokenTellicon (contendo o token de autenticação)

### 1. Formato dos Dados Recebidos

Ao receber um evento, o parceiro deve esperar um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "type": "pushCall",    // Tipo de evento recebido ex: pushCall,...
    "src": "9001",         // Origem do ramal.
    "client": 505,         // Cliente (Condominio vertiral ou horizontal, empresa ou etc).
    "building": 121,       // Número Bloco ou quadra, sendo 0 discartando o uso de bloco ou quadra.
    "apt": 1001,           // Número do apartamento, lote ou sala.
    "dateTime": 1705338959 // Data e hora do evendo no formato epoch.
  }
}
```

## Descrição dos Campos

- **type** (string): Define o tipo de evento relacionado à chamada. Valor aceitável: "pushCall" para eventos de chamada.
- **src** (string): Identifica a origem da chamada.
- **client** (integer): Identificador único do cliente relacionado à chamada.
- **building** (integer): Identificador único do prédio onde a chamada ocorreu.
- **apt** (integer): Número do apartamento relacionado à chamada.
- **dateTime** (integer): Representa a data e a hora do evento em formato Unix timestamp.

3. Requisitos do Webhook
Método HTTP: POST
Cabeçalho Obrigatório: authTokenTellicon (contendo o token de autenticação)
