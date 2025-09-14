# Arquitetura do Sistema BiblioConecta

## Descrição da Arquitetura  
A arquitetura do sistema **BiblioConecta** é dividida em duas camadas principais: um **backend monolítico** e um **frontend de aplicação de página única (SPA)**. Esta abordagem visa otimizar o desenvolvimento, a manutenção e a experiência do usuário, separando claramente as responsabilidades de cada componente. A comunicação entre essas camadas é padronizada através de uma **API REST**.

---

## Componentes do Sistema  

### Backend (Node.js/TypeScript – Monolítico)  
**Função:** Atua como o cérebro do sistema, centralizando toda a lógica de negócio, as regras de empréstimo e reserva, a gestão de usuários e acervo, e o acesso ao banco de dados.  

**Tecnologia:** Desenvolvido em Node.js para alta performance e escalabilidade, utilizando TypeScript para maior robustez e manutenibilidade do código através de tipagem estática.  

**Responsabilidades:**  
- Gerenciamento de usuários (cadastro, autenticação, status).  
- Gestão completa do acervo (adicionar, editar, remover livros e exemplares).  
- Controle de circulação (empréstimos, devoluções, renovações).  
- Gerenciamento de reservas e filas de espera.  
- Exposição de dados e funcionalidades através da API REST.  
- Interação com o banco de dados.  

### Frontend (React/TypeScript – SPA)  
**Função:** Responsável por toda a interface de usuário (UI) e a experiência de usuário (UX). Oferece uma navegação fluida e dinâmica, sem recarregamento completo da página.  

**Tecnologia:** Desenvolvido em React, utilizando TypeScript para garantir a consistência e segurança do código.  

**Responsabilidades:**  
- Apresentação do catálogo de livros e detalhes.  
- Interface para consulta de disponibilidade.  
- Área pessoal do usuário (histórico, empréstimos, reservas).  
- Painel administrativo para a equipe da biblioteca.  
- Comunicação com o backend via API REST.  

### API REST  
**Função:** Serve como o contrato de comunicação entre o frontend e o backend. Define um conjunto de endpoints e métodos HTTP para acessar e manipular os recursos do sistema.  

**Tecnologia:** Implementada no backend Node.js, seguindo os princípios RESTful para comunicação *stateless* e padronizada.  

---

## Padrões Arquiteturais Utilizados  
- **Monolítico (Backend):** toda a lógica de negócio, acesso a dados e API encapsulados em uma única aplicação.  
- **SPA – Single Page Application (Frontend):** a interface é carregada uma vez e atualizada dinamicamente via requisições assíncronas.  
- **API REST (Comunicação):** estilo arquitetural REST para interação entre cliente e servidor, utilizando métodos HTTP padrão (GET, POST, PUT, DELETE).  

---

## Diagrama de Arquitetura  
<img src="./architecture/architecture.png" alt="Diagrama de Arquitetura" width="300">


---

## Decisões Técnicas e Justificativas  

### Backend Monolítico com Node.js/TypeScript  
**Justificativa:** Para um projeto de porte médio como o BiblioConecta, um backend monolítico simplifica o desenvolvimento inicial, a implantação e a manutenção, pois todas as funcionalidades estão em uma única codebase.  
- **Node.js:** capacidade de lidar com alta concorrência (E/S não bloqueante), ideal para aplicações web em tempo real e APIs.  
- **TypeScript:** adiciona tipagem estática, reduzindo erros em tempo de execução e melhora a legibilidade/manutenção do código em equipes.  

### Frontend SPA com React/TypeScript  
**Justificativa:** React é eficiente na renderização de UI, possui vasta comunidade e suporte a componentização. Uma SPA oferece experiência de usuário fluida, essencial para interação com o catálogo e autoatendimento.  
- **TypeScript no Frontend:** garante consistência de código, segurança e melhor manutenção.  

### Comunicação via API REST  
**Justificativa:** REST é amplamente aceito e bem documentado.  
- Comunicação **stateless**, facilitando escalabilidade.  
- Utilização de métodos HTTP padrão torna a integração previsível e robusta.  
- **JSON** como formato de dados, padrão de mercado e otimizado para performance.  
