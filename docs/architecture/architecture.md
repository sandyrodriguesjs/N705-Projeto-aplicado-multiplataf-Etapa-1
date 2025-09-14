## Arquitetura do Sistema BiblioConecta

### Descrição da Arquitetura

A arquitetura do sistema BiblioConecta é dividida em duas camadas principais: um **backend monolítico** e um **frontend de aplicação de página única (SPA)**. Esta abordagem visa otimizar o desenvolvimento, a manutenção e a experiência do usuário, separando claramente as responsabilidades de cada componente. A comunicação entre essas camadas é padronizada através de uma **API REST**.

### Componentes do Sistema

1.  **Backend Node.js/TypeScript (Monolítico):**
    *   **Função:** Atua como o cérebro do sistema, centralizando toda a lógica de negócio, as regras de empréstimo e reserva, a gestão de usuários e acervo, e o acesso ao banco de dados.
    *   **Tecnologia:** Desenvolvido em Node.js para alta performance e escalabilidade, utilizando TypeScript para maior robustez e manutenibilidade do código através de tipagem estática.
    *   **Responsabilidades:**
        *   Gerenciamento de usuários (cadastro, autenticação, status).
        *   Gestão completa do acervo (adicionar, editar, remover livros e exemplares).
        *   Controle de circulação (empréstimos, devoluções, renovações).
        *   Gerenciamento de reservas e filas de espera.
        *   Exposição de dados e funcionalidades através da API REST.
        *   Interação com o banco de dados.

2.  **Frontend React/TypeScript (Single Page Application - SPA):**
    *   **Função:** Responsável por toda a interface de usuário (UI) e a experiência de usuário (UX). Oferece uma navegação fluida e dinâmica, sem recarregamento completo da página.
    *   **Tecnologia:** Desenvolvido em React, uma biblioteca JavaScript popular para construção de interfaces reativas, e TypeScript para garantir a consistência e segurança do código.
    *   **Responsabilidades:**
        *   Apresentação do catálogo de livros e detalhes.
        *   Interface para consulta de disponibilidade.
        *   Área pessoal do usuário (histórico, empréstimos, reservas).
        *   Painel administrativo para a equipe da biblioteca.
        *   Interação com o backend através da API REST para buscar e enviar dados.

3.  **API REST:**
    *   **Função:** Serve como o contrato de comunicação entre o frontend e o backend. Define um conjunto de endpoints e métodos HTTP para acessar e manipular os recursos do sistema.
    *   **Tecnologia:** Implementada no backend Node.js, seguindo os princípios RESTful para comunicação stateless e padronizada.

### Padrões Arquiteturais Utilizados

*   **Monolítico (para o Backend):** Toda a lógica de negócio, acesso a dados e API estão encapsuladas em uma única aplicação.
*   **Single Page Application - SPA (para o Frontend):** A interface do usuário é carregada uma única vez e as atualizações de conteúdo são feitas dinamicamente através de requisições assíncronas ao backend.
*   **API REST (para Comunicação):** Utiliza o estilo arquitetural REST para a comunicação cliente-servidor, focando em recursos e operações HTTP padrão.

### Diagrama de Arquitetura

![Arquitetura do Sistema](./docs/architecture/Arquitetura.png)


### Decisões Técnicas e Justificativas

1.  **Backend Monolítico com Node.js/TypeScript:**
    *   **Justificativa:** Para um projeto de porte médio como o BiblioConecta, um backend monolítico simplifica o desenvolvimento inicial, a implantação e a manutenção, pois todas as funcionalidades estão em uma única codebase. Node.js foi escolhido por sua capacidade de lidar com alta concorrência (E/S não bloqueante), ideal para aplicações web em tempo real e APIs. TypeScript adiciona tipagem estática, reduzindo erros em tempo de execução e melhorando a legibilidade e manutenibilidade do código, especialmente em equipes.

2.  **Frontend SPA com React/TypeScript:**
    *   **Justificativa:** React é uma escolha popular para SPAs devido à sua eficiência na renderização de UI, componentização e vasta comunidade. Uma SPA proporciona uma experiência de usuário mais fluida e responsiva, sem recarregamentos completos da página, o que é crucial para otimizar a interação do usuário com o catálogo e as funcionalidades de autoatendimento. A inclusão de TypeScript no frontend oferece os mesmos benefícios de segurança e manutenibilidade que no backend.

3.  **Comunicação via API REST:**
    *   **Justificativa:** REST é um padrão amplamente aceito e compreendido para a comunicação entre sistemas distribuídos. É stateless, o que facilita a escalabilidade, e utiliza métodos HTTP padrão (GET, POST, PUT, DELETE), tornando a interação entre frontend e backend previsível e robusta. A escolha de JSON como formato de dados para a API é padrão da indústria e otimiza a performance.

