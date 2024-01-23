# Manual - Eventos que são enviados para o parceiro

### 1. Requisitos do parceiro
- Método HTTP: POST
- Endpoint: `http(s)://<hostDoParceiro>/eventTellicon`
- Cabeçalho Obrigatório: authTokenTellicon (contendo o token de autenticação coposto por 24 caracteres e fornecido pelo parceiro)

### 2. Resposta do parceiro
  O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Algumas sugestões de códigos de resposta:
- 200 OK: A solicitação foi recebida com sucesso.
- 400 Bad Request: A solicitação contém dados inválidos ou está ausente.
- 401 Unauthorized: O cabeçalho authTokenTellicon está ausente ou inválido.
- 500 Internal Server Error: O servidor encontrou um erro inesperado durante o processamento.

### 3. API
A API funciona como um webhook para enviar eventos. Abaixo estão os detalhes sobre os dados que serão enviados ao parceiro.

## 3.1. Notificação de Chamada
Quando uma chamada é realizada pelo interfone externo, a API envia um evento de notificação para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nesse evento.

#### 3.1.1. Formato dos Dados
Ao enviar uma notificação de chamada, a API incluirá um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "type": "pushCall",
    "src": "9001",
    "client": 505,
    "building": 121,
    "apt": 1001,
    "eventDateTime": 1705338959
  }
}
```

#### 3.1.2. Descrição dos Campos
- **type** (string): Define o tipo de evento relacionado à chamada. O valor aceitável é "pushCall" para notificações de chamada.
- **src** (string): Identifica a origem da chamada.
- **client** (integer): Código do cliente (Condominio vertiral, horizontal, empresarial e/ou empresas) onde a chamada foi direcionada.
- **building** (integer): Bloco ou quadra onde a chamada foi direcionada.
- **apt** (integer): Número do apartamento, lote ou sala onde a chamada foi direcionada.
- **eventDateTime** (integer): Representa a data e a hora do evento em formato Unix timestamp.

#### 3.1.3. Resposta do parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Algumas sugestões de códigos de resposta:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

#### 3.1.4. Observações
Ao receber essa notificação, o parceiro deve processar os dados conforme necessário.

## 3.2. Registro de Atendimento

Quando um atendimento é registrado, a API envia um evento de controle de acesso para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nessa notificação.

### 3.2.1. Formato dos Dados

Ao enviar esse evento de registro de atendimento, a API incluirá um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "type": "answerCall",
    "src": "9001",
    "dst": "018988776655",
    "client": 505,
    "building": 121,
    "apt": 1001,
    "eventDateTime": 1705338959,
    "answerDateTime": 1705338959,
    "hangupDateTime": 1705338969,
    "callDurationTime": 10
  }
}
```

### 3.2.2. Descrição dos Campos
- **type** (string): Define o tipo de evento relacionado à resposta de chamada. O valor aceitável é "answerCall" para notificações desse tipo.
- **src** (string): Identifica a origem da chamada.
- **dst** (string): Número de quem fez o atendimento da chamada.
- **client** (integer): Código do cliente (Condomínio vertical, horizontal, empresarial e/ou empresas) associado à chamada.
- **building** (integer): Bloco ou quadra associado à chamada.
- **apt** (integer): Número do apartamento, lote ou sala associado à chamada.
- **eventDateTime** (integer): Representa a data e a hora do evento em formato Unix timestamp.
- **answerDateTime** (integer): Representa a data e a hora em que a chamada foi atendida em formato Unix timestamp.
- **hangupDateTime** (integer): Representa a data e a hora em que a chamada foi encerrada em formato Unix timestamp.
- **callDurationTime** (integer): Representa a duração total da chamada em segundos.

### 3.2.3. Resposta do Parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Sugestões de códigos de resposta incluem:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

### 3.2.4. Observações
Ao receber essa notificação, o parceiro deve processar os dados conforme necessário.

## 3.3. Comando DTMF

Quando um comando de DTMF (Dual-tone Multi-frequency) é detectado durante uma chamada, a API envia um evende de controle de acesso para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nesse evento.

### 3.3.1. Formato dos Dados

Ao enviar esse evento de comando de DTMF, a API incluirá um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "type": "dtmfCommand",
    "src": "018988776655",
    "dst": "9001",
    "client": 505,
    "building": 121,
    "apt": 1001,
    "dtmfCommand": "*2",
    "eventDateTime": 1705338965
  }
}
```
### 3.3.2. Descrição dos Campos
- **type** (string): Define o tipo de evento relacionado ao comando DTMF. O valor aceitável é "dtmfCommand" para notificações desse tipo.
- **src** (string): Origem do comando DTMF.
- **dst** (string): Destino do comando DTMF.
- **client** (integer): Código do cliente (Condomínio vertical, horizontal, empresarial e/ou empresas) associado à chamada.
- **building** (integer): Bloco ou quadra associado à chamada.
- **apt** (integer): Número do apartamento, lote ou sala associado à chamada.
- **dtmfCommand** (string): Representa o comando DTMF enviado durante a chamada.
- **eventDateTime** (integer): Representa a data e a hora do evento em formato Unix timestamp.

### 3.2.3. Resposta do Parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Sugestões de códigos de resposta incluem:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

### 3.2.4. Observações
Ao receber essa notificação, o parceiro deve processar os dados conforme necessário.
