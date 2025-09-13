# Especificação da API

## 1. Endpoints previstos:

### Autenticação e Usuários
- POST /auth/register → Registrar novo usuário
- POST /auth/login → Autenticar usuário (gera token JWT)
- POST /auth/logout → Encerrar sessão
- GET /admin/usuarios  → Listar usuários
- PUT /admin/usuarios/{id}/status  → Alterar status (Ativo | Bloqueado)

### Livros e Exemplares
- GET /books → Listar todos os livros
- GET /books/{id} → Detalhes de um livro
- GET /books/search?query=... → Buscar por título, autor, categoria etc.
- GET /books/{id}/exemplares → Listar exemplares do livro e seus status
- POST /admin/books → Adicionar novo livro
- PUT /admin/books/{id} → Atualizar informações do livro
- DELETE /admin/books/{id} → Remover livro do acervo

### Empréstimos
- POST /loans → Solicitar empréstimo de um exemplar
- PUT /loans/{id}/renew → Renovar empréstimo
- PUT /loans/{id}/return → Devolver exemplar
- GET /loans/my → Listar empréstimos do usuário logado
- GET /admin/loans (admin) → Listar todos os empréstimos

### Reservas
- POST /reservas → Criar reserva para um livro
- GET /reservas/my → Listar reservas do usuário logado
- DELETE /reservas/{id} → Cancelar reserva

### Histórico
- GET /historico/my → Histórico do usuário logado
- GET /admin/historico (admin) → Histórico geral (auditoria)

### Avaliações
- POST /books/{id}/avaliacoes → Avaliar um livro
- GET /books/{id}/avaliacoes → Listar avaliações de um livro
- PUT /avaliacoes/{id} → Editar avaliação
- DELETE /avaliacoes/{id} → Remover avaliação

## 2. Parâmetros de requisição:

### Registro de usuário
```
{
  "nome_completo": "Sophia Rocha Dias",
  "email": "sophia.rd@email.com",
  "senha": "123456"
}
```

### Empréstimo de exemplar
```
{
  "id_exemplar": 42
}
```

### Reserva de livro
```
{
  "id_livro": 12
}
```

### Avaliação de livro
```
{
  "nota": 5,
  "comentario": "Excelente leitura!"
}
```

## 3. Formatos de resposta

### Sucesso
```
{
  "success": true,
  "data": { ... }
}
```

### Erro
```
{
  "success": false,
  "error": {
    "code": 401,
    "message": "Token inválido ou expirado"
  }
}
```

## 4. Autenticação e autorização:

- Autenticação via JWT.
- Claims no token diferenciam usuários (role: "user") e administradores (role: "admin").
- Regras:
    - /admin/* → apenas administradores.
    - /loans, /reservas, /historico/my, /books/{id}/avaliacoes → requerem usuário autenticado.
    - /books, /books/search podem ser públicos (opcional).

## 5. Exemplos de chamadas e respostas:

### Login:

#### Request
```
POST /auth/login
Content-Type: application/json

{
  "email": "user@email.com",
  "senha": "123456"
}
```

#### Response
```
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1..."
}
```

### Buscar livro:

#### Request
```
GET /books/search?query=harry&page=1&limit=2
```

#### Response
```
{
  "success": true,
  "data": [
    {
      "id_livro": 1,
      "isbn": "978-85-325-1234-5",
      "titulo": "Harry Potter e a Pedra Filosofal",
      "autor": "J.K. Rowling",
      "ano_publicacao": 1997
    },
    {
      "id_livro": 2,
      "isbn": "978-85-325-2345-6",
      "titulo": "Harry Potter e a Câmara Secreta",
      "autor": "J.K. Rowling",
      "ano_publicacao": 1998
    }
  ]
}
```

### Criar empréstimo:

#### Request
```
POST /loans
Authorization: Bearer <token>
Content-Type: application/json

{
  "id_exemplar": 42
}
```

#### Response
```
{
  "success": true,
  "data": {
    "id_emprestimo": 101,
    "id_usuario": 5,
    "id_exemplar": 42,
    "data_retirada": "2025-09-13",
    "data_prevista_devolucao": "2025-09-27",
    "renovado": false
  }
}
```

### Fazer reserva:

#### Request
```
POST /reservas
Authorization: Bearer <token>
Content-Type: application/json

{
  "id_livro": 12
}
```

#### Response
```
{
  "success": true,
  "data": {
    "id_reserva": 88,
    "id_usuario": 5,
    "id_livro": 12,
    "data_reserva": "2025-09-13",
    "status": "Ativa",
    "posicao_fila": 1
  }
}
```
### Avaliar livro:

#### Request
```
POST /books/12/avaliacoes
Authorization: Bearer <token>
Content-Type: application/json

{
  "nota": 5,
  "comentario": "Um clássico imperdível!"
}
```

#### Response
```
{
  "success": true,
  "data": {
    "id_avaliacao": 501,
    "id_usuario": 5,
    "id_livro": 12,
    "nota": 5,
    "comentario": "Um clássico imperdível!",
    "data_avaliacao": "2025-09-13T14:25:00"
  }
}
```