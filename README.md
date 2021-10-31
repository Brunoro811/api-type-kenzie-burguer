<h1 align="center">
  Kenzie Burger 3.0
</h1>

<p align = "center">
Este é o backend da aplicação Kenzie Burguer 3.0 - Um hub de portfólios de programadores daqui da Kenzie! O objetivo dessa aplicação é conseguir criar um frontend de qualidade, utilizando o que foi ensinado no segundo módulo do curso (Q2) - E desenvolver hard skills e soft skills. A API é de cadastro de usuários e compra de comidas para satisfazer tanto clientes como a empresa.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>
## **Endpoints**

A API tem um total de 3 endpoints, sendo em volta principalmente do usuário (dev) <br/>
Para importar o JSON no Insomnia é só clicar na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From Url" e colocar o link acima :v:

O url base da API é https://my-animals-lost-kenzie.herokuapp.com/

## Rotas que não precisam de autenticação

o usuário não cadastrado ou logado pode listar os produtos mas não pode adicionar ai carrinho pois precisa logar para fale-lo.

<h2 align ='center'> Listando Produtos </h2>
Nessa aplicação o usuário precisa fazer login ou se cadastrar pode ver os animais já cadastrados na plataforma, na API podemos acessar a lista dessa forma:
Aqui conseguimos ver os animais perdidos.

`GET /produts -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "email": "",
    "password": "",
    "name": "",
    "age": 0,
    "id": 0
  },
  {
    "email": "bruno@teste.com",
    "password": "$2a$10$s9re9chE7TY3914yDbO9VODx1WOd3eCd2WTUsKOyABhSXCo2JweVO",
    "name": "Bruno",
    "age": 25,
    "id": 1
  },
  {
    "email": "bruno@gmail.com",
    "password": "$2a$10$OiKcd9XGwwXtssoJeOhTJOeODeyQg7BlkcUVonEgl4/meDuQqzJE2",
    "name": "",
    "age": 25,
    "id": 2
  }
]
```


<h2 align ='center'> Cadastro de usuário </h2>
Nessa aplicação o cliente pode se cadastrar na plataforma, na API podemos passar no body as informações de usuário:
Aqui conseguimos ver como são passadas essas informações.

`POST /users -  Body `
```json
[
  {
      "email": "kenzinho@mail.com",
      "password": "123456",
      "name": "Kenzinho",
      "age": 38,
      "id": 1
    }
]
```

Caso dê tudo certo, a resposta será assim:

`POST /users -  FORMATO DA RESPOSTA - STATUS 201`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImJydW5vQHRlc3RlLmNvbSIsImlhdCI6MTYzNTIwNjE0MCwiZXhwIjoxNjM1MjA5NzQwLCJzdWIiOiIxIn0.84wRErC9s097Z_omKllsd1ShumzSzV6RajUm5sH7bSE",
  "user": {
     "email": "kenzinho@mail.com",
      "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
      "name": "Kenzinho",
      "age": 38,
      "id": 1
  }
}
```

Possiveis Erros :

<h2> Ao tentar cadastrar um email que já exista! </h2>

`POST /users -  FORMATO DA RESPOSTA - STATUS 404 `
```json
[
  "Email already exists"
]
```
<h2> Ao tentar cadastrar sem email ou senha! </h2>

`POST /users -  FORMATO DA RESPOSTA - STATUS 404 `
```json
[
  "Email and password are required"
]
```


<h2 align = "center"> Login </h2>
Nessa aplicação o cliente pode fazer login na plataforma, na API podemos passar no body as informações de usuário:
Aqui conseguimos ver como são passadas essas informações.

`POST /login - FORMATO DA REQUISIÇÃO`
```json
{
    "email": "bruno@teste.com",
    "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login -  FORMATO DA RESPOSTA - STATUS 201`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImJydW5vQHRlc3RlLmNvbSIsImlhdCI6MTYzNTIwNzIyMywiZXhwIjoxNjM1MjEwODIzLCJzdWIiOiIxIn0.3NRuMPBH8SVdFUdBX8gLHrI43CsB5XHb95ady2EG-Js",
  "user": {
    "email": "bruno@teste.com",
    "name": "Bruno",
    "age": 25,
    "id": 1
  }
}
```
Caso dê erro, a resposta será assim:

`POST /login -  FORMATO DA RESPOSTA - STATUS 400`
```json
{
    "Cannot find user"
}
```

## Rotas que precisam de autenticação

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h1>Usuário</h1>

<h2 align ='center'> Somente o usuário logado pode deletar o próprio usuário </h2>

Ao deletar o usuário é necessários informar o id do usuario e estar logado(possuir token válido).

  Caso dê tudo certo, a resposta será assim:

`DELETE /users/:id -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {}
]
```
  Possiveis Erros: 

 Ao informar um id de usuário que não existe!

`DELETE /users/:id -  FORMATO DA RESPOSTA - STATUS 401`
```json
[
  "Cannot read property 'id' of undefined"
]
```


 Ao informar um id de usuário que vazio!
 
`DELETE /users/:id -  FORMATO DA RESPOSTA - STATUS 403`
```json
[
  "Private resource access: entity must have a reference to the owner id"
]
```

<h2 align ='center'> Somente o usuário logado pode atualizar o próprio usuário </h2>

Ao atualziar o usuario é necessário id do usuário, o usuário deve estar logado(possuir token válido).

`PUT /users/:id - FORMATO DA REQUISIÇÃO`
`body`
```json
[
    {
      "email": "kenzie@mail.com",
      "password": "123456",
      "name": "bruno",
      "age": 38,
		"id": 1,
    }
]
```

Caso dê erro, a resposta será assim:


`PUT /users/:id - FORMATO DA RESPOSTA - STATUS 200`
```json
[
    {
  "email": "kenzie@mail.com",
  "password": "$2a$10$okUbvBmNDDPZIXUOJfs7mOPCXOIaRvIlsfp5z3ix.Wfy4jNFxb7ty",
  "name": "bruno",
  "age": 38,
  "id": 1,
  "userId": 1
}
]
```

  Possiveis Erros: 

 Ao informar um id de usuário que não é o do usuário logado!

`DELETE /users/:id -  FORMATO DA RESPOSTA - STATUS 403`
```json
[
  "Private resource replacement: request body must have a reference to the owner id"
]
```



<h1>Produtos</h1>

<h2 align ='center'> Somente o usuário logado pode cadastrar um produto </h2>


`POST /products -  FORMATO DA RESPOSTA - STATUS 201`
```json
   {
        "name": "X-Burger",
        "img": "https://drive.google.com/file/d/1Je4F_FobdZPox9KVQbxC7l5lm5Y56n_i/view?usp=sharing",
	 	"description":"Um cheeseburger é um hambúrguer coberto com queijo",
        "category": "Sanduiche",
	 	"price":14.00,
        "id": 0
    }
```

<h2 align ='center'> Somente o usuário logado pode deletar um produto </h2>
    
`DELETE /products/:id-do-produto  FORMATO DA RESPOSTA - STATUS 200`
```json
   {}
```

<h2 align ='center'> Somente o usuário logado pode atualizar um produto </h2>
    
`PUT /products/:id-do-produto  FORMATO DA RESPOSTA - STATUS 200`
```json
   {
      "name": "X-Burger Duplo Queijo",
      "img": "https://drive.google.com/file/d/1Je4F_FobdZPox9KVQbxC7l5lm5Y56n_i/view?usp=sharing",
      "description": "Um cheeseburger Duplo são dois hambúrguers coberto com queijo",
      "category": "Sanduiche",
      "price": 18,
      "id": 2,
      "userId": 1
    }
```

<h2 align ='center'> Listando Vendas de Produtos </h2>
Nessa aplicação o usuário precisa fazer login ou se cadastrar, fazer um pedido, finaliziar o pedido e listar o pedido na plataforma, na API podemos acessar o pedido dessa forma:
`userId` é o id do usuário que fez o pedido.

`GET /sales/userId -  FORMATO DA RESPOSTA - STATUS 200`
```json
{
  "saleNumber": 0,
  "priceTotal": 0,
  "status": false,
  "userId": 1,
  "products": [
    {
      "name": "X-Burger",
      "img": "https://drive.google.com/file/d/1Je4F_FobdZPox9KVQbxC7l5lm5Y56n_i/view?usp=sharing",
      "category": "Sanduiche",
      "price": 14,
      "id": 0,
      "userId": 0,
      "saleId": 0
    },
    {
      "name": "X-Burger Duplo",
      "img": "https://drive.google.com/file/d/1Je4F_FobdZPox9KVQbxC7l5lm5Y56n_i/view?usp=sharing",
      "category": "Sanduiche",
      "price": 14,
      "id": 0,
      "userId": 0,
      "saleId": 0
    }
  ],
  "id": 1
}
```
<h1>Sales de Products</h1>

<h2 align ='center'> Somente o usuário logado pode cadastrar um venda de produto </h2>

`POST /sales -  FORMATO DA RESPOSTA - STATUS 201`
```json
     {
      "saleNumber": 0,
      "priceTotal": 0,
      "status":false,
      "userId": 1,
      "products": [
        {
          "name": "X-Burger",
          "img": "https://drive.google.com/file/d/1Je4F_FobdZPox9KVQbxC7l5lm5Y56n_i/view?usp=sharing",
          "category": "Sanduiche",
          "price": 14,
          "id": 0,
          "userId": 0,
          "saleId": 0
        },
        {
          "name": "X-Burger Duplo",
          "img": "https://drive.google.com/file/d/1Je4F_FobdZPox9KVQbxC7l5lm5Y56n_i/view?usp=sharing",
          "category": "Sanduiche",
          "price": 14,
          "id": 0,
          "userId": 0,
          "saleId": 0
        }
      ],
      "id": 1
    }
```

