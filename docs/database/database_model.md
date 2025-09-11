# 📘 Modelo de Dados - BiblioConecta

// BiblioConecta - Modelo de Dados

![Modelo de Dados](database_model.png)


```dbml

Table usuarios {
  id_usuario integer [primary key, increment]
  nome_completo varchar
  email varchar [unique, not null]
  senha_hash varchar
  status varchar // Ativo | Bloqueado
  data_cadastro timestamp
}

Table livros {
  id_livro integer [primary key, increment]
  isbn varchar [unique, not null]
  titulo varchar
  autor varchar
  editora varchar
  ano_publicacao integer
  sinopse text
}

Table exemplares {
  id_exemplar integer [primary key, increment]
  id_livro integer [not null]
  codigo_exemplar varchar [unique, not null]
  status varchar // Disponível | Emprestado | Reservado
}

Table emprestimos {
  id_emprestimo integer [primary key, increment]
  id_usuario integer [not null]
  id_exemplar integer [not null]
  data_retirada date
  data_prevista_devolucao date
  data_devolucao date
  renovado boolean
}

Table reservas {
  id_reserva integer [primary key, increment]
  id_usuario integer [not null]
  id_livro integer [not null]
  data_reserva date
  status varchar // Ativa | Atendida | Expirada
  posicao_fila integer
}

Table historico {
  id_historico integer [primary key, increment]
  id_usuario integer [not null]
  id_exemplar integer [not null]
  acao varchar // Emprestimo | Devolucao | Renovacao | Reserva
  data_acao timestamp
}

Table avaliacoes {
  id_avaliacao integer [primary key, increment]
  id_usuario integer [not null]
  id_livro integer [not null]
  nota integer // escala 1 a 5
  comentario text
  data_avaliacao timestamp
}

// ==============================
// Relacionamentos
// ==============================

// Usuario -> Emprestimos
Ref: emprestimos.id_usuario > usuarios.id_usuario

// Usuario -> Reservas
Ref: reservas.id_usuario > usuarios.id_usuario

// Livro -> Exemplares
Ref: exemplares.id_livro > livros.id_livro

// Exemplar -> Emprestimos
Ref: emprestimos.id_exemplar > exemplares.id_exemplar

// Livro -> Reservas
Ref: reservas.id_livro > livros.id_livro

// Usuario -> Historico
Ref: historico.id_usuario > usuarios.id_usuario

// Exemplar -> Historico
Ref: historico.id_exemplar > exemplares.id_exemplar

// Usuario -> Avaliacoes
Ref: avaliacoes.id_usuario > usuarios.id_usuario

// Livro -> Avaliacoes
Ref: avaliacoes.id_livro > livros.id_livro


# 📗 Dicionário de Dados – BiblioConecta

## Tabela: usuarios
| Campo         | Tipo       | Descrição                      | Restrição                        |
|---------------|------------|--------------------------------|---------------------------------|
| id_usuario    | integer    | Identificador único do usuário | PK, autoincrement               |
| nome_completo | varchar    | Nome completo do usuário       | Not null                        |
| email         | varchar    | E-mail do usuário              | Not null, único                 |
| senha_hash    | varchar    | Hash da senha do usuário       | Not null                        |
| status        | varchar    | Status do usuário              | Valores: Ativo, Bloqueado       |
| data_cadastro | timestamp  | Data de cadastro do usuário    | Not null                        |

## Tabela: livros
| Campo          | Tipo       | Descrição                 | Restrição                        |
|----------------|------------|---------------------------|---------------------------------|
| id_livro       | integer    | Identificador único       | PK, autoincrement               |
| isbn           | varchar    | Código ISBN do livro      | Not null, único                 |
| titulo         | varchar    | Título do livro           | Not null                        |
| autor          | varchar    | Autor(es) do livro        | Not null                        |
| editora        | varchar    | Editora do livro          | Opcional                        |
| ano_publicacao | integer    | Ano de publicação         | Opcional                        |
| sinopse        | text       | Sinopse do livro          | Opcional                        |

## Tabela: exemplares
| Campo           | Tipo       | Descrição                     | Restrição                        |
|-----------------|------------|-------------------------------|---------------------------------|
| id_exemplar     | integer    | Identificador único do exemplar | PK, autoincrement              |
| id_livro        | integer    | Referência ao livro            | FK → livros.id_livro, Not null |
| codigo_exemplar | varchar    | Código único do exemplar       | Not null, único                 |
| status          | varchar    | Status do exemplar             | Valores: Disponível, Emprestado, Reservado |

## Tabela: emprestimos
| Campo                   | Tipo       | Descrição                         | Restrição                                 |
|-------------------------|------------|----------------------------------|------------------------------------------|
| id_emprestimo           | integer    | Identificador do empréstimo       | PK, autoincrement                        |
| id_usuario              | integer    | Usuário que pegou o livro         | FK → usuarios.id_usuario, Not null       |
| id_exemplar             | integer    | Exemplar emprestado               | FK → exemplares.id_exemplar, Not null   |
| data_retirada           | date       | Data de retirada do exemplar      | Not null                                 |
| data_prevista_devolucao | date       | Data prevista de devolução        | Not null                                 |
| data_devolucao          | date       | Data real da devolução            | Pode ser null                            |
| renovado                | boolean    | Indica se o empréstimo foi renovado | Not null, default false               |

## Tabela: reservas
| Campo        | Tipo       | Descrição                     | Restrição                                 |
|--------------|------------|-------------------------------|------------------------------------------|
| id_reserva   | integer    | Identificador da reserva       | PK, autoincrement                        |
| id_usuario   | integer    | Usuário que fez a reserva      | FK → usuarios.id_usuario, Not null       |
| id_livro     | integer    | Livro reservado                | FK → livros.id_livro, Not null           |
| data_reserva | date       | Data da reserva                | Not null                                 |
| status       | varchar    | Status da reserva              | Valores: Ativa, Atendida, Expirada      |
| posicao_fila | integer    | Posição do usuário na fila     | Not null                                 |

## Tabela: historico
| Campo        | Tipo       | Descrição                       | Restrição                                 |
|--------------|------------|---------------------------------|------------------------------------------|
| id_historico | integer    | Identificador da entrada        | PK, autoincrement                        |
| id_usuario   | integer    | Usuário que realizou a ação     | FK → usuarios.id_usuario, Not null       |
| id_exemplar  | integer    | Exemplar relacionado            | FK → exemplares.id_exemplar, Not null   |
| acao         | varchar    | Tipo de ação                    | Valores: Empréstimo, Devolução, Renovação, Reserva |
| data_acao    | timestamp  | Data e hora da ação             | Not null                                 |

## Tabela: avaliacoes
| Campo         | Tipo       | Descrição                       | Restrição                                 |
|---------------|------------|---------------------------------|------------------------------------------|
| id_avaliacao  | integer    | Identificador da avaliação      | PK, autoincrement                        |
| id_usuario    | integer    | Usuário que avaliou             | FK → usuarios.id_usuario, Not null       |
| id_livro      | integer    | Livro avaliado                  | FK → livros.id_livro, Not null           |
| nota          | integer    | Nota do livro (1 a 5)           | Not null                                 |
| comentario    | text       | Comentário do usuário           | Opcional                                 |
| data_avaliacao| timestamp  | Data da avaliação               | Not null                                 |

