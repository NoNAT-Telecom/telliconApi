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
Quando uma chamada é realizada pelo interfone externo, a API envia um evento de notificação para o parceiro. Abaixo estão os detalhes sobre os dados que serão incluídos nessa notificação.

# 3.1.1. Formato dos Dados
Ao enviar uma notificação de chamada, a API incluirá um payload JSON com os seguintes campos:

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
```

# 3.1.2. Descrição dos Campos
- **type** (string): Define o tipo de evento relacionado à chamada. O valor aceitável é "pushCall" para notificações de chamada.
- **src** (string): Identifica a origem da chamada.
- **client** (integer): Código do cliente (Condominio vertiral, horizontal, empresarial e/ou empresas) onde a chamada foi direcionada.
- **building** (integer): Bloco ou quadra onde a chamada foi direcionada.
- **apt** (integer): Número do apartamento, lote ou sala onde a chamada foi direcionada.
- **dateTime** (integer): Representa a data e a hora do evento em formato Unix timestamp.
