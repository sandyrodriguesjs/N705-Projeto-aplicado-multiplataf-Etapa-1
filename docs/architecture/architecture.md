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





### Decisões Técnicas e Justificativas

1.  **Backend Monolítico com Node.js/TypeScript:**
    *   **Justificativa:** Para um projeto de porte médio como o BiblioConecta, um backend monolítico simplifica o desenvolvimento inicial, a implantação e a manutenção, pois todas as funcionalidades estão em uma única codebase. Node.js foi escolhido por sua capacidade de lidar com alta concorrência (E/S não bloqueante), ideal para aplicações web em tempo real e APIs. TypeScript adiciona tipagem estática, reduzindo erros em tempo de execução e melhorando a legibilidade e manutenibilidade do código, especialmente em equipes.

2.  **Frontend SPA com React/TypeScript:**
    *   **Justificativa:** React é uma escolha popular para SPAs devido à sua eficiência na renderização de UI, componentização e vasta comunidade. Uma SPA proporciona uma experiência de usuário mais fluida e responsiva, sem recarregamentos completos da página, o que é crucial para otimizar a interação do usuário com o catálogo e as funcionalidades de autoatendimento. A inclusão de TypeScript no frontend oferece os mesmos benefícios de segurança e manutenibilidade que no backend.

3.  **Comunicação via API REST:**
    *   **Justificativa:** REST é um padrão amplamente aceito e compreendido para a comunicação entre sistemas distribuídos. É stateless, o que facilita a escalabilidade, e utiliza métodos HTTP padrão (GET, POST, PUT, DELETE), tornando a interação entre frontend e backend previsível e robusta. A escolha de JSON como formato de dados para a API é padrão da indústria e otimiza a performance.

Diagrama ER - Sistema BiblioConecta


```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diagrama ER - BiblioConecta</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            color: #2c3e50;
        }
        
        .container {
            width: 100%;
            max-width: 1200px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            margin: 20px 0;
        }
        
        header {
            background: #3498db;
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .content {
            padding: 30px;
            display: flex;
            flex-direction: column;
            gap: 30px;
        }
        
        .er-diagram {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }
        
        .entity {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border-left: 5px solid #3498db;
        }
        
        .entity h3 {
            color: #3498db;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .entity ul {
            list-style: none;
        }
        
        .entity li {
            padding: 8px 0;
            border-bottom: 1px dashed #e0e0e0;
            display: flex;
            align-items: center;
        }
        
        .entity li:last-child {
            border-bottom: none;
        }
        
        .pk {
            color: #e74c3c;
            font-weight: bold;
            margin-right: 8px;
        }
        
        .fk {
            color: #3498db;
            font-weight: bold;
            margin-right: 8px;
        }
        
        .relationships {
            background: #e8f4fc;
            padding: 25px;
            border-radius: 10px;
        }
        
        .relationships h2 {
            color: #2c3e50;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .relationship-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }
        
        .relationship-item {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
        }
        
        .relationship-item p {
            font-weight: 500;
        }
        
        .relationship-type {
            display: inline-block;
            background: #3498db;
            color: white;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            margin-top: 8px;
        }
        
        footer {
            text-align: center;
            padding: 20px;
            background: #2c3e50;
            color: white;
        }
        
        @media (max-width: 768px) {
            .er-diagram {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Diagrama Entidade-Relacionamento</h1>
            <p class="subtitle">Sistema BiblioConecta - Gestão de Biblioteca</p>
        </header>
        
        <div class="content">
            <div class="er-diagram">
                <div class="entity">
                    <h3>USUARIO</h3>
                    <ul>
                        <li><span class="pk">PK</span> id: INT</li>
                        <li>nome: VARCHAR(100)</li>
                        <li>email: VARCHAR(100) <span style="color: #27ae60;">UK</span></li>
                        <li>senha_hash: VARCHAR(255)</li>
                        <li>status: ENUM('Ativo', 'Bloqueado')</li>
                        <li>data_criacao: DATETIME</li>
                        <li>data_atualizacao: DATETIME</li>
                    </ul>
                </div>
                
                <div class="entity">
                    <h3>LIVRO</h3>
                    <ul>
                        <li><span class="pk">PK</span> id: INT</li>
                        <li>isbn: VARCHAR(20) <span style="color: #27ae60;">UK</span></li>
                        <li>titulo: VARCHAR(200)</li>
                        <li>autor: VARCHAR(100)</li>
                        <li>editora: VARCHAR(100)</li>
                        <li>ano_publicacao: INT</li>
                        <li>categoria: VARCHAR(50)</li>
                        <li>sinopse: TEXT</li>
                        <li>capa_url: VARCHAR(255)</li>
                        <li>data_cadastro: DATETIME</li>
                    </ul>
                </div>
                
                <div class="entity">
                    <h3>EXEMPLAR</h3>
                    <ul>
                        <li><span class="pk">PK</span> id: INT</li>
                        <li><span class="fk">FK</span> livro_id: INT</li>
                        <li>codigo_identificacao: VARCHAR(50) <span style="color: #27ae60;">UK</span></li>
                        <li>status: ENUM('Disponível', 'Emprestado', 'Reservado')</li>
                        <li>data_aquisicao: DATETIME</li>
                        <li>disponivel: BOOLEAN</li>
                    </ul>
                </div>
                
                <div class="entity">
                    <h3>EMPRESTIMO</h3>
                    <ul>
                        <li><span class="pk">PK</span> id: INT</li>
                        <li><span class="fk">FK</span> usuario_id: INT</li>
                        <li><span class="fk">FK</span> exemplar_id: INT</li>
                        <li>data_emprestimo: DATETIME</li>
                        <li>data_devolucao_prevista: DATETIME</li>
                        <li>data_devolucao_real: DATETIME</li>
                        <li>renovado: BOOLEAN</li>
                        <li>status: ENUM('Ativo', 'Finalizado', 'Atrasado')</li>
                    </ul>
                </div>
                
                <div class="entity">
                    <h3>RESERVA</h3>
                    <ul>
                        <li><span class="pk">PK</span> id: INT</li>
                        <li><span class="fk">FK</span> usuario_id: INT</li>
                        <li><span class="fk">FK</span> livro_id: INT</li>
                        <li>data_reserva: DATETIME</li>
                        <li>data_expiracao: DATETIME</li>
                        <li>status: ENUM('Ativa', 'Cancelada', 'Expirada', 'Concluída')</li>
                        <li>posicao_fila: INT</li>
                    </ul>
                </div>
            </div>
            
            <div class="relationships">
                <h2>Relacionamentos</h2>
                <div class="relationship-list">
                    <div class="relationship-item">
                        <p>USUARIO → EMPRESTIMO</p>
                        <span class="relationship-type">1:N (Um para Muitos)</span>
                    </div>
                    <div class="relationship-item">
                        <p>USUARIO → RESERVA</p>
                        <span class="relationship-type">1:N (Um para Muitos)</span>
                    </div>
                    <div class="relationship-item">
                        <p>LIVRO → EXEMPLAR</p>
                        <span class="relationship-type">1:N (Um para Muitos)</span>
                    </div>
                    <div class="relationship-item">
                        <p>LIVRO → RESERVA</p>
                        <span class="relationship-type">1:N (Um para Muitos)</span>
                    </div>
                    <div class="relationship-item">
                        <p>EXEMPLAR → EMPRESTIMO</p>
                        <span class="relationship-type">1:N (Um para Muitos)</span>
                    </div>
                </div>
            </div>
        </div>
        
        <footer>
            <p>BiblioConecta - Sistema de Gestão de Biblioteca | Diagrama ER</p>
        </footer>
    </div>
</body>
</html>
```
