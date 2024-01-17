# Manual - Eventos que são enviados para o parceiro

## Endpoint: `http(s)://<hostDoParceiro>/eventTellicon`

A API funciona como um webhook para enviar eventos relacionados a chamadas. Abaixo estão os detalhes sobre os dados que serão enviados ao parceiro.

### 1. Requisitos do parceiro
- Método HTTP: POST
- Cabeçalho Obrigatório: authTokenTellicon (contendo o token de autenticação coposto por 24 caracteres e fornecido pelo parceiro)

### 2. Resposta do parceiro
  O parceiro deve retornar uma resposta HTTP adequada para indicar o status da recepção do evento. Algumas sugestões de códigos de resposta:
- 200 OK: A solicitação foi recebida com sucesso.
- 400 Bad Request: A solicitação contém dados inválidos ou está ausente.
- 401 Unauthorized: O cabeçalho authTokenTellicon está ausente ou inválido.
- 500 Internal Server Error: O servidor encontrou um erro inesperado durante o processamento.
