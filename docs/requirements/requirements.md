## Requisitos Funcionais (RF):

*   **Consulta ao Catálogo:** O usuário deve poder buscar livros no acervo a partir de qualquer dispositivo, usando filtros como título, autor ou assunto.

*   **Verificação de Disponibilidade:** O sistema deve exibir em tempo real se um livro está disponível na prateleira, emprestado ou em fila de espera.

*   **Autoatendimento Online:** O usuário deve poder realizar ações como renovar seus empréstimos e entrar na fila de reserva para um livro que esteja ocupado, sem precisar ir à biblioteca.

*   **Área Pessoal do Usuário:** Deve haver uma área de perfil onde o usuário possa consultar seu histórico, ver as datas de devolução de seus livros e gerenciar suas reservas.

*   **Painel de Controle Centralizado:** A equipe deve ter acesso a um painel administrativo para gerenciar todas as operações da biblioteca de forma organizada.

*   **Gestão do Acervo (Catalogação):** O sistema deve permitir adicionar, editar e remover livros do acervo. Deve incluir um recurso para simplificar o cadastro, preenchendo as informações do livro automaticamente a partir do seu código de barras (ISBN).

*   **Gestão de Circulação (Empréstimos):** O processo de registrar empréstimos e devoluções deve ser rápido e à prova de erros, utilizando um leitor de código de barras para identificar os livros e os usuários.

*   **Gestão de Usuários:** A equipe deve poder cadastrar novos leitores, consultar informações e visualizar o histórico de empréstimos de cada usuário.

## Requisitos não-funcionais (RNF):

*   **Usabilidade:** A interface do sistema deve ser intuitiva e clara, tanto para os leitores quanto para a equipe. O objetivo é que qualquer pessoa consiga usar as principais funções com o mínimo de treinamento.

*   **Desempenho:** As respostas do sistema, especialmente as buscas no catálogo e as operações de empréstimo, devem ser rápidas para não atrasar o atendimento e garantir uma boa experiência ao usuário.

*   **Segurança:** Todas as informações pessoais dos usuários devem ser armazenadas de forma segura e protegida contra acessos não autorizados.

*   **Confiabilidade e Disponibilidade:** O sistema deve ser estável e permanecer online e acessível durante todo o horário de funcionamento da biblioteca, no mínimo.

*   **Compatibilidade:** A plataforma deve funcionar corretamente nos principais navegadores de internet (como Chrome, Firefox e Safari) e ser acessível por dispositivos móveis (smartphones e tablets).


## Regras de Negócio

1.  Regras de Usuário Leitor
    *   Cadastro Único: O e-mail utilizado no cadastro de um usuário deve ser único em todo o sistema. Não podem existir dois usuários com o mesmo e-mail.
    *   Campos Obrigatórios: Para se cadastrar, o usuário deve fornecer, no mínimo, Nome Completo e E-mail.
    *   Status do Usuário: Um usuário pode ter dois status: "Ativo" ou "Bloqueado".
        *   Um usuário com status "Bloqueado" não pode realizar novos empréstimos ou renovações.
        *   O status de um usuário muda para "Bloqueado" automaticamente se ele possuir um ou mais empréstimos em atraso.

2.  Regras de Livro Acervo
    *   Identificação do Livro: Um livro é definido unicamente pelo seu ISBN identificador da edição.
    *   Exemplares: Um mesmo livro mesmo ISBN pode ter um ou mais exemplares físicos no acervo. Cada exemplar possui um código de identificação único no sistema.
    *   Status do Exemplar: Cada exemplar de um livro pode ter um dos seguintes status:
        *   Disponível: O exemplar está na prateleira e pode ser emprestado.
        *   Emprestado: O exemplar está com um usuário.
        *   Reservado: O exemplar foi devolvido e está aguardando a retirada por um usuário que o reservou.

3.  Regras de Empréstimo
    *   Condição para Empréstimo: Para realizar um empréstimo, o status do usuário deve ser "Ativo" e o status do exemplar do livro deve ser "Disponível".
    *   Limite de Empréstimos: Cada usuário pode ter, no máximo, 3 três livros emprestados simultaneamente.
    *   Prazo de Empréstimo: O prazo padrão para um empréstimo é de 14 catorze dias corridos, a contar da data de retirada.
    *   Processo de Empréstimo: Ao realizar um empréstimo, o sistema deve:
        *   Alterar o status do exemplar para "Emprestado".
        *   Registrar o empréstimo no histórico do usuário.
        *   Definir e registrar a data de devolução prevista data atual + 14 dias.
    *   Renovação de Empréstimo:
        *   Cada empréstimo pode ser renovado 1 uma única vez.
        *   A renovação estende o prazo de devolução por mais 14 dias a partir da data em que foi solicitada.
        *   Um empréstimo não pode ser renovado se o livro já tiver uma reserva de outro usuário.

4.  Regras de Reserva
    *   Condição para Reserva: Um usuário só pode reservar um livro se todos os exemplares daquele título estiverem com o status "Emprestado".
    *   Limite de Reservas: Cada usuário pode ter, no máximo, 2 duas reservas ativas simultaneamente.
    *   Fila de Reserva: As reservas para um mesmo título seguirão uma fila no formato "primeiro a chegar, primeiro a ser atendido" First-In, First-Out.
    *   Atendimento da Reserva: Quando um exemplar de um livro reservado é devolvido, o sistema deve:
        *   Alterar o status do exemplar para "Reservado".
        *   Notificar o primeiro usuário da fila que o livro está disponível para retirada.
        *   O usuário notificado terá um prazo de 48 horas para retirar o livro. Se não o fizer, ele perde a vez na fila e o próximo usuário é notificado.

5.  Regras de Devolução
    *   Processo de Devolução: Ao registrar uma devolução, o sistema deve:
        *   Verificar se há reservas para aquele título.
        *   Se houver: Alterar o status do exemplar para "Reservado".
        *   Se não houver: Alterar o status do exemplar para "Disponível".
        *   Finalizar o registro do empréstimo no histórico do usuário.
    *   Devolução em Atraso: Uma devolução é considerada "em atraso" se a data de retorno for posterior à data de devolução prevista.
    *   Consequência do Atraso: Se uma devolução for registrada com atraso, o status do usuário que devolveu o livro deve ser alterado para "Bloqueado", até que sua situação seja regularizada pela equipe da biblioteca.
    *   Gestão de Multas: O sistema irá identificar e registrar o atraso, além de bloquear o usuário. No entanto, conforme o escopo do projeto, a gestão financeira cálculo de valor, pagamento de multas não será implementada. A regularização do status do usuário desbloqueio será uma ação manual da equipe da biblioteca.

    ## Casos de uso

### Caso de Uso 01: Consultar Disponibilidade de Livro

*   **Ator Principal:** Leitor qualquer usuário, mesmo não logado
*   **Resumo:** O Leitor busca por um livro no sistema para verificar se ele faz parte do acervo e se há exemplares disponíveis para empréstimo.
*   **Pré-condições:** O Leitor deve ter acesso à aplicação web.
*   **Fluxo Principal:**
    1.  O Leitor acessa a funcionalidade de busca.
    2.  O Leitor informa os dados de pesquisa título, autor, etc..
    3.  O Sistema exibe uma lista de livros que correspondem à pesquisa.
    4.  O Leitor seleciona um livro da lista.
    5.  O Sistema exibe a página de detalhes do livro, mostrando a sinopse, o autor e o status de disponibilidade ex: "Disponível", "Todos Emprestados".
*   **Pós-condições:** O Leitor é informado sobre a existência e a disponibilidade do livro no acervo.
*   **Fluxos Alternativos:**
    *   **Livro não encontrado:** Se a busca não retornar resultados, o Sistema exibe uma mensagem "Nenhum livro encontrado para o termo pesquisado".

### Caso de Uso 02: Cadastrar Novo Livro no Acervo

*   **Ator Principal:** Gestor Bibliotecário
*   **Resumo:** O Gestor adiciona um novo título de livro ao catálogo do sistema, incluindo seus dados e a quantidade de exemplares.
*   **Pré-condições:** O Gestor deve estar autenticado no painel administrativo.
*   **Fluxo Principal:**
    1.  O Gestor acessa a função "Adicionar Novo Livro".
    2.  O Gestor informa o ISBN do livro.
    3.  O Sistema busca os dados do livro título, autor, editora em uma base de dados externa e preenche os campos automaticamente.
    4.  O Gestor preenche ou confirma os dados do livro e informa a quantidade de exemplares a serem adicionados.
    5.  O Gestor salva o formulário.
    6.  O Sistema cria o registro do livro e os registros dos novos exemplares, todos com status "Disponível".
    7.  O Sistema exibe uma mensagem de sucesso.
*   **Pós-condições:** O novo livro e seus exemplares estão disponíveis no catálogo para consulta e empréstimo.
*   **Fluxos Alternativos:**
    *   **ISBN não encontrado:** Se o Sistema não encontrar os dados do livro, o Gestor deverá preencher todos os campos manualmente.
    *   **Livro já existe:** Se o ISBN informado já estiver cadastrado, o Sistema informa o Gestor e pergunta se ele deseja apenas adicionar novos exemplares ao registro existente.
