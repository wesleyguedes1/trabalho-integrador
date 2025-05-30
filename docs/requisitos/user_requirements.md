# SISTEMA DE RECOMENDAÇÃO DE FILMES
**REQUISITOS DO USUÁRIO**

---

**UNIVERSIDADE FEDERAL DA FRONTEIRA SUL - UFFS** 
**CIÊNCIA DA COMPUTAÇÃO** 
**MAIO, 2025**

---

## 1. IDENTIFICAÇÃO DA SOLUÇÃO

Com o crescimento exponencial das plataformas de streaming e a vasta quantidade de conteúdo audiovisual disponível, os usuários enfrentam cada vez mais dificuldades para encontrar filmes que atendam aos seus gostos pessoais. A sobrecarga de opções frequentemente resulta em decisões de visualização insatisfatórias ou tempo excessivo gasto navegando entre catálogos.

Sistemas de recomendação tradicionais, baseados em filtros colaborativos simples ou análise de conteúdo, apresentam limitações significativas como:
- O problema do "cold start" para novos usuários
- Recomendações genéricas que não capturam preferências específicas
- Dificuldade em identificar relações complexas entre usuários e filmes

---

## 2. ELICITAÇÃO DOS REQUISITOS

### 2.1 Descrição dos Processos de Descoberta e Consumo de Filmes

**Processo Atual de Descoberta:**
O processo atual de descoberta de filmes pelos usuários geralmente segue um padrão não estruturado:
- Navegação por categorias pré-definidas nas plataformas
- Busca por recomendações de amigos
- Consulta a sites especializados como IMDb ou Rotten Tomatoes
- Escolha aleatória baseada em cartazes atrativos

**Avaliação de Filmes:**
A avaliação de filmes acontece informalmente através de conversas com amigos, posts em redes sociais, ou ocasionalmente através de sistemas de rating das plataformas. Raramente existe um registro sistemático das preferências pessoais ou uma análise detalhada das razões pelas quais determinados filmes agradaram ou não.

**Histórico de Visualização:**
O acompanhamento do histórico de visualização é fragmentado entre diferentes plataformas, resultando em perda de contexto sobre padrões de preferência a longo prazo. Não existe integração entre as diferentes fontes de conteúdo que o usuário consome, limitando a eficácia de qualquer sistema de recomendação individual.

### 2.2 Descrição dos Principais Problemas Enfrentados

- **Sobrecarga de opções** resultando em paralisia de decisão ao escolher filmes
- **Recomendações genéricas** que não refletem gostos pessoais específicos
- **Dificuldade em descobrir filmes** de nicho ou internacionais que correspondam às preferências

### 2.3 Expectativas do Sistema

- Sistema de recomendações personalizadas baseado em análise de padrões complexos de preferência
- Interface para avaliação detalhada de filmes assistidos com sistema de rating
- Gerenciamento de listas de filmes (assistidos, para assistir, favoritos)
- Integração com APIs de filmes para acesso a metadados completos
- Recursos sociais para compartilhamento de recomendações entre amigos
- Funcionalidades de descoberta avançada com filtros personalizáveis

---

## 3. ESPECIFICAÇÃO DOS REQUISITOS

### 3.1 Requisitos Funcionais do Sistema

| ID | Requisito Funcional | Descrição |
|:---|:-------------------|:----------|
| **RF01** | **Cadastrar/Gerenciar Perfil de Usuário** | Área para criação e edição de perfil de usuário, incluindo preferências de gênero, configurações de privacidade e informações pessoais. |
| **RF02** | **Sistema de Autenticação** | Implementar login seguro com email/senha e integração com redes sociais (Google, Facebook). Incluir recuperação de senha e autenticação de dois fatores. |
| **RF03** | **Avaliar Filmes** | Interface para usuários avaliarem filmes em escala de 1-5 estrelas, com opção de adicionar resenhas detalhadas. |
| **RF04** | **Gerar Recomendações Personalizadas** | Sistema baseado em grafos que analisa padrões de avaliação do usuário e relacionamentos com outros usuários para gerar recomendações precisas. |
| **RF05** | **Gerenciar Listas de Filmes** | Permitir criação e gerenciamento de listas personalizadas (assistidos, para assistir, favoritos), com opções de organização e compartilhamento. |
| **RF06** | **Buscar e Filtrar Filmes** | Sistema de busca avançada com filtros por gênero, ano e diretor. |
| **RF07** | **Visualizar Detalhes do Filme** | Exibir informações completas sobre filmes incluindo sinopse, elenco, diretor, trailer, onde assistir, e avaliações da comunidade. |
| **RF08** | **Dashboard Personalizado** | Página inicial com resumo das atividades recentes, recomendações em destaque, estatísticas pessoais de visualização e tendências. |
| **RF09** | **Estatísticas Pessoais** | Visualização de dados sobre hábitos de visualização, gêneros preferidos, evolução do gosto ao longo do tempo e comparações com a comunidade. |
| **RF10** | **Recomendações por Contexto** | Gerar sugestões baseadas em contexto específico (humor atual, tempo disponível, companhia para assistir) usando análise avançada do perfil. |

### 3.2 Requisitos Não Funcionais do Sistema

| ID | Requisito Não Funcional | Descrição |
|:---|:-----------------------|:----------|
| **RNF01** | **Usabilidade** | Interface intuitiva e responsiva que funciona adequadamente em dispositivos móveis, tablets e desktops. |
| **RNF02** | **Segurança** | Implementar criptografia para dados sensíveis.
| **RNF03** | **Desenvolvimento** | **Tecnologias:** React/Next.js (frontend), Node.js/Express e FastAPI (backend), PostgreSQL e Neo4j (dados), PyTorch Geometric (ML). |
| **RNF04** | **Integração** | APIs RESTful e GraphQL para integração com serviços externos (TMDB, streaming platforms) e aplicativos de terceiros. |
| **RNF05** | **Privacidade** | Controles de privacidade que permitem usuários controlarem visibilidade de avaliações, listas e atividades. Opção de deletar conta e todos os dados. |

### 3.3 Diagrama de Casos de Uso

#### 3.3.1 Atores do Diagrama de Casos de Uso

| Ator | Descrição |
|:-----|:----------|
| **Usuário Casual** | Usuário que utiliza o sistema esporadicamente para encontrar filmes para assistir, com interação básica de rating e listas. |
| **Administrador** | Responsável pela moderação de conteúdo, gerenciamento de usuários e manutenção do sistema. |
| **Sistema** | Componente automatizado responsável por gerar recomendações e análises. |

#### 3.3.2 Descrição dos Casos de Uso

---

**[UC01] Gerenciar Perfil de Usuário**
- **Casos de uso relacionados:** [UC02]
- **Pré-condição:** Usuário registrado no sistema
- **Descrição:** Criar, visualizar e editar informações do perfil pessoal. Definir preferências de gênero, configurações de privacidade e integração com redes sociais. Relaciona-se com autenticação [UC02].

---

**[UC02] Autenticar no Sistema**
- **Casos de uso relacionados:** Todos os outros casos de uso
- **Pré-condição:** Nenhuma
- **Descrição:** Realizar login/logout, registro de nova conta, recuperação de senha e autenticação de dois fatores.

---

**[UC03] Avaliar e Comentar Filmes**
- **Casos de uso relacionados:** [UC04], [UC08]
- **Pré-condição:** Estar autenticado
- **Descrição:** Atribuir ratings de 1-5 estrelas para filmes e escrever resenhas detalhadas. Impacta geração de recomendações [UC04] e estatísticas [UC08].

---

**[UC04] Receber Recomendações Personalizadas**
- **Casos de uso relacionados:** [UC03], [UC05]
- **Pré-condição:** Estar autenticado e ter avaliado pelo menos 5 filmes
- **Descrição:** Visualizar filmes recomendados pelo sistema, com explicações sobre critérios utilizados. Baseado em avaliações [UC03] e pode ser filtrado [UC05].

---

**[UC05] Buscar e Filtrar Filmes**
- **Casos de uso relacionados:** [UC06]
- **Pré-condição:** Estar autenticado
- **Descrição:** Utilizar sistema de busca avançada com múltiplos filtros (gênero, ano, diretor, etc.). Resultados podem ser adicionados a listas [UC06].

---

**[UC06] Gerenciar Listas de Filmes**
- **Casos de uso relacionados:** [UC09]
- **Pré-condição:** Estar autenticado
- **Descrição:** Criar, editar e organizar listas personalizadas (assistidos, para assistir, favoritos). Listas podem ser compartilhadas com outros usuários [UC09].

---

**[UC07] Visualizar Detalhes de Filme**
- **Casos de uso relacionados:** [UC03], [UC06]
- **Pré-condição:** Estar autenticado
- **Descrição:** Acessar informações completas sobre filmes incluindo metadados, trailer, onde assistir e avaliações da comunidade. Permite avaliar [UC03] ou adicionar a listas [UC06].

---

**[UC08] Visualizar Estatísticas Pessoais**
- **Casos de uso relacionados:** [UC03]
- **Pré-condição:** Estar autenticado e ter histórico de avaliações
- **Descrição:** Acessar dashboard com estatísticas de visualização, gêneros preferidos, evolução de gostos e comparações com comunidade.

---

**[UC09] Interagir Socialmente**
- **Casos de uso relacionados:** [UC06], [UC10]
- **Pré-condição:** Estar autenticado
- **Descrição:** Seguir outros usuários, compartilhar listas e recomendações, participar de discussões sobre filmes. Relaciona-se com listas [UC06] e notificações [UC10].

---

**[UC10] Receber Notificações**
- **Casos de uso relacionados:** [UC04], [UC09]
- **Pré-condição:** Estar autenticado e ter configurado preferências
- **Descrição:** Receber alertas sobre novos lançamentos relevantes, atividades de amigos e atualizações de recomendações.

---

**[UC11] Explorar Modo Descoberta**
- **Casos de uso relacionados:** [UC05], [UC06]
- **Pré-condição:** Estar autenticado
- **Descrição:** Navegar por categorias especializadas, filmes temáticos, diretores em destaque e tendências da comunidade. Combina aspectos de busca [UC05] e gerenciamento de listas [UC06].

---
