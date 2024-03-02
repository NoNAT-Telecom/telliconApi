# Manual - Inclusão, edição e exclusão de dados da portaria autonoma.

## 1. Requisitos
- Método HTTP: POST
- Endpoint: `https://<host>/webhook/cmdTellicon`
- Cabeçalho Obrigatório: authToken (contendo o token de autenticação coposto por 24 caracteres)

## 3. API
A API funciona para receber dados. Abaixo estão os detalhes sobre os dados que serão recebidos do parceiro.

## 4.1. Inclusão de ramais
Para incluir novos ramais, você deve enviar uma solicitação HTTP POST para o endpoint especificado, juntamente com os dados necessários no corpo da solicitação.

### 4.1.1. Formato dos dados
O parceiro deve enviar os dados da seguinte forma:

```json
{
  "cmdTellicon": [{
    "type": "addExten",
    "patner": 22,
    "company": 3333,
    "client": 444444,
    "exten": 1
  }]
}
```
### 4.1.2. Descrição dos Campos
- **cmdTellicon**(array): Deve ser um array contendo objetos JSON que representam as operações a serem realizadas.
- **type**(string): Indica o tipo de operação a ser realizada. Neste caso, "addExten" indica a adição de um ramal.
- **patner**(interger): Representa o identificador do parceiro (será definido por nós).
- **company**(interger): Representa o identificador da empresa.
- **client**(interger): Representa o identificador do cliente.
- **exten**(interger): Representa o número do ramal a ser adicionado.
