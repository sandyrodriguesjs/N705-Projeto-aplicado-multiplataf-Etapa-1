# N705 - Projeto Aplicado Multiplataforma Etapa 1

## Descrição do projeto

O projeto BiblioConecta é uma plataforma desenvolvida para modernizar a interação entre bibliotecas e seus usuários. A solução aborda o problema da falta de acesso remoto ao acervo, permitindo que leitores consultem o catálogo, verifiquem a disponibilidade de livros e gerenciem seus empréstimos online. Para a equipe da biblioteca, o sistema oferece um painel administrativo que otimiza a gestão do acervo e o controle de circulação dos livros. 

## Problema abordado e justificativa do projeto

O problema que o projeto busca resolver é o distanciamento entre a biblioteca e seus usuários, causado pela falta de ferramentas digitais que atendam às expectativas atuais de acesso à informação. Essa lacuna se manifesta em dificuldades práticas que criam uma experiência ineficiente e desestimulante para quem busca utilizar o acervo.

As principais dificuldades enfrentadas pelo usuário são a falta de um catálogo online, o usuário não consegue saber, sem ser presencialmente a disponibilidade de livros que a biblioteca possui. A incerteza se a biblioteca possui aquele livro, e a dependência do espaço físico para renovar empréstimos ou solicitar uma reserva.
O projeto justifica-se por trazer acessibilidade, praticidade e modernização, incentivando o uso do acervo e otimizando a gestão da equipe.

O sistema busca entender dois tipos de usuários: a comunidade em geral que necessita de forma rápida e prática não depender de intermediários para tarefas como consultar, renovar ou reservar um livro; e a equipe da biblioteca, formada por bibliotecários, assistentes e administradores que precisam de algo simples e fácil de usar para organizar seu trabalho diário e automatizar tarefas repetitivas como fazer cadastros de livros e dar baixas.


## Objetivos do sistema
- Permitir consulta online ao acervo de livros;
- Viabilizar reservas e renovações sem necessidade de presença física;
- Oferecer painel administrativo para bibliotecários com funções de cadastro e controle de circulação;
- Modernizar o relacionamento entre biblioteca e comunidade.

## Escopo do projeto
Na primeira etapa do projeto inclui na perspectiva do Frontend a aplicação web responsiva (usuário e administrador), no Backend a API REST para operações de consulta, cadastro, reservas e empréstimos e no banco de dados o armazenamento de informações de usuários, livros e movimentações. Não inclui no escopo da primeira etapa o desenvolvimento de aplicativo mobile nativo e integrações externas com sistemas de outras bibliotecas.

## Visão geral da arquitetura

Backend: Será uma aplicação monolítica construída em Node.js com TypeScript. Ele centralizará toda a lógica de negócio, regras e acesso ao banco de dados.
Frontend: Será uma Single Page Application (SPA) desenvolvida em React com TypeScript, responsável por toda a interface e experiência do usuário.
Comunicação: A conexão entre o frontend e o backend será feita exclusivamente através de uma API REST.

![Diagrama de Arquitetura](./docs/architecture/arquitetura.png)


## Tecnologias propostas

O sistema é construído com Node.js/TypeScript API REST no backend e React/TypeScript SPA no frontend.

## Cronograma para Etapa 2

| Etapa | Atividade | Período | Responsável |
|-------|------------|----------|-------------|
| 1 | Modelagem final do banco de dados | Semana 1 | Equipe Backend |
| 2 | Desenvolvimento da API REST (usuários, livros, empréstimos) | Semanas 2-3 | Equipe Backend |
| 3 | Desenvolvimento do frontend (telas principais) | Semanas 3-4 | Equipe Frontend |
| 4 | Integração frontend + backend | Semana 5 | Todos |
| 5 | Testes, ajustes e documentação final | Semana 6 | Todos |

## Integrantes da equipe e responsabilidades

Antonio Mikael Vasconcelos Aguiar (2326335) - 
Sandy Rodrigues do Nascimento (2326334) - 
Vitória de Oliveira Almeida (2325332) - 
Renato (    ) - 


