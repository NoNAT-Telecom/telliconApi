# Manual - Eventos que são enviados para o parceiro

## 1. Requisitos do parceiro
- Método HTTP: POST
- Endpoint: `http(s)://<hostDoParceiro>/eventTellicon`
- Cabeçalho Obrigatório: authTokenTellicon (contendo o token de autenticação coposto por 24 caracteres e fornecido pelo parceiro)

## 2. Resposta do parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Algumas sugestões de códigos de resposta:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

## 3. API
A API funciona como um webhook para enviar eventos. Abaixo estão os detalhes sobre os dados que serão enviados ao parceiro.

## 4.1. Notificação de Chamada
Quando uma chamada é realizada pelo interfone externo, a API envia um evento de notificação para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nesse evento.

### 4.1.1. Formato dos Dados
Ao enviar uma notificação de chamada, a API incluirá um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "tipo": "pushCall",
    "parceiro": 11,
    "contrato": 2222, 
    "licenca": 333333,
    "bloco": 555,
    "unidade": 6666,
    "ramal": "77988888888",
    "dataHoraEvento": 1705338959
  }
}
```

### 4.1.2. Descrição dos Campos
- **tipo** (string): Define o tipo de evento relacionado à chamada. O valor aceitável é "pushCall" para notificações de chamada.
- **parceiro** (interger): Identifica o parceiro na base de dados.
- **contrato** (integer): Codigo da empresa cadastrada.
- **licenca** (integer): Código do cliente (Condominio vertiral, horizontal, empresarial e/ou empresas) onde a chamada foi direcionada.
- **bloco** (integer): Bloco ou quadra onde a chamada foi direcionada.
- **unidade** (integer): Número do apartamento, lote ou sala onde a chamada foi direcionada.
- **ramal** (string): Identifica o ramal de origem da chamada.
- **dataHoraEvento** (integer): Representa a data e a hora do evento em formato Unix timestamp.

### 4.1.3. Resposta do parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Algumas sugestões de códigos de resposta:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

### 4.1.4. Observações
Ao receber essa notificação, o parceiro deve processar os dados conforme necessário.

## 4.2. Registro de Atendimento

Quando um atendimento é registrado, a API envia um evento de controle de acesso para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nessa notificação.

### 4.2.1. Formato dos Dados

Ao enviar esse evento de registro de atendimento, a API incluirá um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "tipo": "answerCall",
    "parceiro": 11,
    "contrato": 2222, 
    "licenca": 333333,
    "bloco": 555,
    "unidade": 6666,
    "ramal": "77988888888",
    "telefone": "77988888888",
    "dataHoraEvento": 1705338900,
    "dataHoraAtendido": 1705338910,
    "dataHoraEncerrado": 17053389625,
    "tempoEspera": 10,
    "tempoConversa": 15
  }
}
```

### 4.2.2. Descrição dos Campos
- **tipo** (string): Define o tipo de evento relacionado à resposta de chamada. O valor aceitável é "answerCall" para notificações desse tipo.
- **parceiro** (interger): Identifica o parceiro na base de dados.
- **contrato** (integer): Codigo da empresa cadastrada.
- **licenca** (integer): Código do cliente (Condominio vertiral, horizontal, empresarial e/ou empresas) associado à chamada.
- **bloco** (integer): Bloco ou quadra associado à chamada.
- **unidade** (integer): Número do apartamento, lote ou sala associado à chamada.
- **ramal** (string): Identifica o ramal de origem da chamada.
- **telefone** (string): Número de quem fez o atendimento da chamada.
- **dataHoraEvento** (integer): Representa a data e a hora do evento em formato Unix timestamp.
- **dataHoraAtendido** (integer): Representa a data e a hora em que a chamada foi atendida em formato Unix timestamp.
- **dataHoraEncerrado** (integer): Representa a data e a hora em que a chamada foi encerrada em formato Unix timestamp.
- **tempoEspera** (integer): Representa a tempo total em espera até ser atendido.
- **tempoConversa** (integer): Representa a duração total de conversação em segundos.

### 4.2.3. Resposta do Parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Sugestões de códigos de resposta incluem:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

### 4.2.4. Observações
Ao receber essa notificação, o parceiro deve processar os dados conforme necessário.

## 4.3. Comando DTMF

Quando um comando de DTMF (Dual-tone Multi-frequency) é detectado durante uma chamada, a API envia um evento de controle de acesso para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nesse evento.

### 4.3.1. Formato dos Dados

Ao enviar esse evento de comando de DTMF, a API incluirá um payload JSON com os seguintes campos:

```json
{
  "eventTellicon": {
    "type": "dtmfCommand",
    "parceiro": 11,
    "contrato": 2222, 
    "licenca": 333333,
    "bloco": 555,
    "unidade": 6666,
    "ramal": "77988888888",
    "telefone": "77988888888",
    "dtmfComando": "*2",
    "dataHoraEvento": 1705338965
  }
}
```
### 4.3.2. Descrição dos Campos
- **tipo** (string): Define o tipo de evento relacionado ao comando DTMF. O valor aceitável é "dtmfCommand" para notificações desse tipo.
- **parceiro** (interger): Identifica o parceiro na base de dados.
- **contrato** (integer): Codigo da empresa cadastrada.
- **licenca** (integer): Código do cliente (Condominio vertiral, horizontal, empresarial e/ou empresas) associado à chamada.
- **bloco** (integer): Bloco ou quadra associado à chamada.
- **unidade** (integer): Número do apartamento, lote ou sala associado à chamada.
- **telefone** (string): Origem do comando DTMF.
- **ramal** (string): Destino do comando DTMF.
- **dtmfComando** (string): Representa o comando DTMF enviado durante a chamada.
- **dataHoraEvento** (integer): Representa a data e a hora do evento em formato Unix timestamp.

### 4.2.3. Resposta do Parceiro
O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Sugestões de códigos de resposta incluem:

- **200 OK**: A solicitação foi recebida com sucesso.
- **400 Bad Request**: A solicitação contém dados inválidos ou está ausente.
- **401 Unauthorized**: O cabeçalho authTokenTellicon está ausente ou inválido.
- **500 Internal Server Error**: O servidor encontrou um erro inesperado durante o processamento.

### 4.2.4. Observações
Ao receber essa notificação, o parceiro deve processar os dados conforme necessário.
