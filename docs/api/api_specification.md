**Este documento apresenta os principais endpoints da API ConectaBairro, os parâmetros esperados, formatos de resposta, autenticação e exemplos de chamadas. A API será planejada para facilitar o cadastro, consulta e gerenciamento de empreendimentos locais, promovendo a economia colaborativa entre moradores e empreendedores.**

---
## Sumário

1. [Endpoints Previstos](#endpoints-previstos)
2. [Parâmetros de Requisição](#parâmetros-de-requisição)
3. [Formatos de resposta](#formatos-de-resposta)
4. [Autenticação e Autorização](#autenticação-e-autorização)
5. Exemplos de chamadas e respostas](#exemplos-de-chamadas-e-respostas)

## Endpoints Previstos

| Método | Rota                          | Descrição                                 | Protegida |
|--------|-------------------------------|-------------------------------------------|-----------|
| POST   | /usuarios/cadastroUsuario     | Cadastro de novo usuário                  | Não       |
| POST   | /usuarios/login               | Autenticação e geração de token JWT       | Não       |
| POST   | /empreendimentos              | Cadastro de empreendimento                | Sim       |
| PUT    | /empreendimentos/:id          | Edição de empreendimento                  | Sim       |
| DELETE | /empreendimentos/:id          | Exclusão de empreendimento                | Sim       |
| GET    | /empreendimentos              | Listagem e busca de empreendimentos       | Não       |

---

## Parâmetros de Requisição

### Headers

```http
Content-Type: application/json
Authorization: Bearer SEU_TOKEN_JWT  // Apenas para rotas protegidas
```

### Body (JSON)

- Selecione a opção raw

- Escolha o tipo JSON

- Insira os dados conforme os exemplos abaixo

## Formatos de resposta

Todas as respostas da API seguirão o formato JSON, com estrutura padronizada: 

```json
{
  "mensagem": "Operação realizada com sucesso",
  "dados": {
    "Conteúdo retornado"
  }
}
```
### Em caso de erro:

```json
{
  "erro": "Descrição do erro"
}
```
---

## Autenticação e Autorização

A API utilizará JWT (JSON Web Token) para autenticação. Após o login, o token deverá ser incluído no header das requisições protegidas:

```Http
Authorization: Bearer SEU_TOKEN_JWT
```
- Rotas públicas: /usuarios/cadastroUsuario, /usuarios/login, /empreendimentos (GET)

- Rotas protegidas: /empreendimentos (POST, PUT, DELETE)

### Integração com o Frontend

No frontend, o token será armazenado no localStorage após o login do usuário. Para chamadas às rotas protegidas, o token será recuperado e incluído no header da requisição utilizando a função fetch.

Exemplo de uso com fetch:

```javascript
const token = localStorage.getItem("token");

fetch("/empreendimentos", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": `Bearer ${token}`
  },
  body: JSON.stringify({
    nome: "Peixaria do Seu Zé",
    descricao: "Comércio de frutos do mar",
    // demais campos...
  })
});
```
Essa abordagem garantirá que apenas usuários autenticados possam acessar funcionalidades sensíveis, como cadastro, edição e exclusão de empreendimentos.


---

## Exemplos de chamadas e respostas

### Cadastro de Usuário

**POST /usuarios/cadastroUsuario**

Requisição:

```json
{
  "nome": "Teste",
  "email": "teste@email.com",
  "senha": "123456"
}
```

Resposta esperada:

```json
{
  "mensagem": "Usuário cadastrado com sucesso",
  "_id": "68b4d4cdb98dfb4abe6addff",
  "nome": "Teste Usuário",
  "email": "teste@teste.com",
  "token": "TOKEN_JWT_GERADO"
}
```

### Login

**POST /usuarios/login**

Requisição:

```json
{
  "email": "teste@email.com",
  "senha": "123456"
}
```

Resposta esperada:

```json
{
  "_id": "689fb6a91270e26fb9e6b14a",
  "nome": "Teste Usuário",
  "email": "teste@teste.com",
  "token": "TOKEN_JWT_GERADO"
}
```

### Cadastro de Empreendimento

**POST /empreendimentos**

Requisição:

```json
{
  "nome": "Peixaria do Seu Zé",
  "descricao": "Comércio de frutos do mar",
  "endereco": {
    "cep": "60180-900",
    "rua": "Rua Benedito Macêdo",
    "bairro": "Cais do Porto",
    "numero": "100",
    "complemento": "",
    "cidade": "Fortaleza",
    "estado": "CE"
  },
  "telefone": "85998989999",
  "email": "peixe_do_ze@teste.com",
  "palavrasChave": ["peixe", "camarão", "frutos do mar", "polvo"]
}
```

**Obs: Também é possível enviar apenas o CEP, e a API preencherá os campos restantes via ViaCEP.**

Resposta esperada:

```json
{
  "mensagem": "Empreendimento cadastrado com sucesso",
  "empreendimento": {
    "nome": "Peixaria do Seu Zé",
    "descricao": "Comércio de frutos do mar",
    "endereco": {
      "cep": "60180900",
      "rua": "Rua Benedito Macêdo",
      "bairro": "Cais do Porto",
      "numero": "100",
      "complemento": "",
      "cidade": "Fortaleza",
      "estado": "CE"
    },
    "telefone": "85998989999",
    "email": "peixe_do_ze@teste.com",
    "palavrasChave": ["peixe", "camarão", "frutos do mar", "polvo"],
    "cidadeNormalizada": "fortaleza",
    "bairroNormalizado": "cais do porto",
    "palavrasChaveNormalizadas": ["peixe", "camarao", "frutos do mar", "polvo"],
    "criadoPor": "68b4e46d43368a8855a1d76a",
    "_id": "68b4e88dbed3289d2d46e6d3",
    "createdAt": "2025-09-01T00:27:57.178Z",
    "updatedAt": "2025-09-01T00:27:57.178Z",
    "__v": 0
  }
}
```

### Edição de Empreendimento

**PUT /empreendimentos/:id**

Requisição (exemplo de múltiplos campos):

```json
{
  "descricao": "Comércio de mariscos",
  "telefone": "85999999999",
  "endereco": {
    "rua": "Rua Lindoya",
    "numero": "300"
  },
  "palavrasChave": ["praia", "fortaleza", "mar"]
}
```

Obs: Se o campo endereco.cep for alterado, a API buscará os dados atualizados via API ViaCEP.

Resposta esperada:

```json
{
  "mensagem": "Empreendimento atualizado com sucesso",
  "empreendimento": {
    "endereco": {
      "cep": "60180650",
      "rua": "Rua Lindoya",
      "bairro": "Cais do Porto",
      "numero": "300",
      "complemento": "",
      "cidade": "Fortaleza",
      "estado": "CE"
    },
    "_id": "68af1af559c823c81a7ba1f3",
    "nome": "Peixaria do seu Zé",
    "descricao": "Comércio de mariscos",
    "telefone": "85999999999",
    "email": "peixe_do_Ze@teste.com",
    "palavrasChave": ["peixe", "camarão", "frutos do mar", "polvo"],
    "cidadeNormalizada": "fortaleza",
    "bairroNormalizado": "cais do porto",
    "palavrasChaveNormalizadas": ["peixe", "camarao", "frutos do mar", "polvo"],
    "criadoPor": "689fb6a91270e26fb9e6b14a",
    "createdAt": "2025-08-27T14:49:25.334Z",
    "updatedAt": "2025-08-27T14:49:58.836Z",
    "__v": 0
  }
}
```

### Exclusão de Empreendimento

**DELETE /empreendimentos/:id**

Requisição:

```http
DELETE /empreendimentos/ID_DO_EMPREENDIMENTO
Authorization: Bearer SEU_TOKEN_JWT
```
Resposta esperada:

```json
{
  "mensagem": "Empreendimento deletado com sucesso"
}
```

### 🔍 Listagem e Busca de Empreendimentos

**GET /empreendimentos**

A API permitirá listar todos os empreendimentos cadastrados e realizará buscas específicas utilizando filtros via query params. Abaixo estão os principais filtros planejados:

| Filtro           | Exemplo de Requisição                                               |
|------------------|----------------------------------------------------------------------|
| Cidade + Bairro  | `/empreendimentos?cidade=Fortaleza&bairro=Cais do Porto`            |
| CEP              | `/empreendimentos?cep=60180-900`                                     |
| Rua              | `/empreendimentos?rua=Rua Benedito Macêdo`                           |
| Bairro           | `/empreendimentos?bairro=Cais do Porto`                              |
| Cidade           | `/empreendimentos?cidade=Fortaleza`                                  |
| Estado           | `/empreendimentos?estado=CE`                                         |
| Palavra-chave    | `/empreendimentos?palavra=peixe`                                     |

**Resposta esperada:**  

Ao utilizar o query params GET `/empreendimentos?cidade=Fortaleza` a API retornará os dados do empreendimento separados por cidade, exibindo também o clima da cidade buscada (via API OpenWatherMap).


```json
[
  {
    "cidade": "fortaleza",
    "clima": {
      "cidade": "Fortaleza",
      "temperatura": 27.07,
      "descricao": "algumas nuvens",
      "umidade": 74,
      "vento": 4.63
    },
    "empreendimentos": [
      {
        "endereco": {
          "cep": "60180-900",
          "rua": "Rua Benedito Macêdo",
          "bairro": "Cais do Porto",
          "numero": "800",
          "complemento": "",
          "cidade": "Fortaleza",
          "estado": "CE"
        },
        "_id": "68af3e50f131eef692759a91",
        "nome": "Peixaria do seu Zé",
        "descricao": "Comércio de peixes, polvos e frutos do mar em geral",
        "telefone": "85998989999",
        "email": "peixe_do_Ze@teste.com",
        "palavrasChave": [
          "peixe fresco",
          "ostra",
          "marisco"
        ],
        "cidadeNormalizada": "fortaleza",
        "bairroNormalizado": "cais do porto",
        "palavrasChaveNormalizadas": [
          "peixe fresco",
          "ostra",
          "marisco"
        ],
        "criadoPor": null,
        "createdAt": "2025-08-27T17:20:17.011Z",
        "updatedAt": "2025-08-27T19:06:23.354Z",
        "__v": 0
      }
    ]
  }
]
```

### Respostas de Erro (Padronizadas)

```json
{
  "erro": "Usuário já cadastrado"
}
```

```json
{
  "erro": "Credenciais inválidas"
}
```

```json
{
  "erro": "Token inválido ou expirado"
}
```

```json
{
  "erro": "Usuário não autorizado para esta ação"
}
```

```json
{
  "erro": "Erro ao editar empreendimento",
  "camposObrigatorios": [
    "endereco.rua",
    "endereco.bairro",
    "endereco.cidade",
    "endereco.estado"
  ],
  "mensagem": "Os seguintes campos são obrigatórios e não podem estar em branco: endereco.rua, endereco.bairro, endereco.cidade, endereco.estado"
}
```

### Tratamento de Erros no Frontend

As mensagens de erro retornadas pela API serão exibidas ao usuário por meio de alertas ou componentes visuais.  
Exemplo com `fetch`:

```javascript
fetch("/usuarios/login", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ email, senha })
})
.then(res => res.json())
.then(data => {
  if (data.erro) {
    alert(data.erro); // ou exibir em um componente de erro
  } else {
    localStorage.setItem("token", data.token);
  }
});
```
### Validação no Frontend

Antes de enviar dados para a API, o frontend fará validações como:

- Garantir que a senha tenha no mínimo 6 caracteres.

- Impedir envio de campos obrigatórios em branco.


### Segurança de Origem (CORS)

Durante a implantação, o backend será configurado para aceitar requisições apenas do domínio oficial do frontend, utilizando políticas de CORS. Isso evita que aplicações externas não autorizadas consumam a API.

### Expiração de Sessão
Se a API retornar erro de token inválido ou expirado, o frontend deverá:
1. Limpar o token do `localStorage`.
2. Redirecionar o usuário para a página de login.
3. Exibir mensagem informando que a sessão expirou.

--- 