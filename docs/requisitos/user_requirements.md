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

| ID | Requisito Funcional | Descrição | Atributos Principais |
|:---|:-------------------|:----------|:---------------------|
| **RF01** | **Cadastrar/Gerenciar Perfil de Usuário** | Área para criação e edição de perfil de usuário, incluindo preferências de gênero, configurações de privacidade e informações pessoais. | **Dados Pessoais:** nome, email, senha, foto_perfil, data_nascimento, genero, bio<br>**Configurações:** conta_publica, receber_notificacoes, preferencias_genero<br>**Controle:** data_criacao, ultimo_acesso, ativo, papel |
| **RF02** | **Sistema de Autenticação** | Implementar login seguro com email/senha e integração com redes sociais (Google, Facebook). Incluir recuperação de senha e autenticação de dois fatores. | **Sessão:** token_sessao, data_inicio, data_expiracao, ip_address, user_agent, ativa<br>**Segurança:** senha_hash, tentativas_login, bloqueado_ate<br>**OAuth:** provider_externo, provider_id |
| **RF03** | **Avaliar Filmes** | Interface para usuários avaliarem filmes em escala de 1-5 estrelas, com opção de adicionar resenhas detalhadas. | **Avaliação:** id_usuario, id_filme, nota (1-5), resenha, data_avaliacao, data_edicao<br>**Interação:** likes, dislikes, publica<br>**Moderação:** denunciado, aprovado |
| **RF04** | **Gerar Recomendações Personalizadas** | Sistema baseado em grafos que analisa padrões de avaliação do usuário e relacionamentos com outros usuários para gerar recomendações precisas. | **Algoritmo:** id_usuario, id_filme, score_confianca, justificativa, tipo_recomendacao<br>**Contexto:** humor_atual, tempo_disponivel, companhia<br>**Controle:** data_geracao, visualizada, rejeitada |
| **RF05** | **Gerenciar Listas de Filmes** | Permitir criação e gerenciamento de listas personalizadas (assistidos, para assistir, favoritos), com opções de organização e compartilhamento. | **Lista:** nome, descricao, publica, data_criacao, data_atualizacao, tipo_lista<br>**Organização:** ordem_exibicao, cor_tema, icone<br>**Conteúdo:** id_filme, data_adicao, posicao, nota_pessoal |
| **RF06** | **Buscar e Filtrar Filmes** | Sistema de busca avançada com filtros por gênero, ano, diretor, ator, plataforma e avaliação mínima. | **Busca:** termo_busca, filtros_aplicados, ordem_resultado<br>**Filtros:** generos[], ano_inicio, ano_fim, duracao_min, duracao_max, nota_min<br>**Pessoa:** diretor, ator, roteirista<br>**Disponibilidade:** plataformas[], tipo_acesso |
| **RF07** | **Visualizar Detalhes do Filme** | Exibir informações completas sobre filmes incluindo sinopse, elenco, diretor, trailer, onde assistir, e avaliações da comunidade. | **Metadados:** titulo, titulo_original, sinopse, ano_lancamento, duracao_minutos<br>**Visual:** poster_url, trailer_url, classificacao_etaria, idioma_original<br>**Financeiro:** orcamento, bilheteria<br>**Social:** avaliacoes_usuarios, nota_media, total_avaliacoes |
| **RF08** | **Dashboard Personalizado** | Página inicial com resumo das atividades recentes, recomendações em destaque, estatísticas pessoais de visualização e tendências. | **Atividades:** ultimas_avaliacoes, filmes_adicionados_listas, interacoes_sociais<br>**Estatísticas:** filmes_assistidos, avaliacoes_feitas, tempo_total, genero_favorito<br>**Tendências:** filmes_populares, lancamentos, recomendacoes_destaque |
| **RF09** | **Estatísticas Pessoais** | Visualização de dados sobre hábitos de visualização, gêneros preferidos, evolução do gosto ao longo do tempo e comparações com a comunidade. | **Métricas:** filmes_assistidos, avaliacoes_feitas, listas_criadas, seguidores_count<br>**Preferências:** generos_favoritos, diretores_favoritos, atores_favoritos<br>**Temporal:** evolucao_gosto, padroes_sazonais<br>**Social:** comparacao_comunidade, ranking_atividade |
| **RF10** | **Recomendações por Contexto** | Gerar sugestões baseadas em contexto específico (humor atual, tempo disponível, companhia para assistir) usando análise avançada do perfil. | **Contexto:** humor (feliz, triste, nostálgico), tempo_disponivel, companhia (sozinho, família, amigos)<br>**Situação:** dispositivo_uso, horario, dia_semana<br>**Histórico:** contextos_anteriores, efetividade_recomendacao |
| **RF11** | **Interações Sociais** | Sistema de seguir usuários, compartilhar listas, comentar avaliações e receber notificações de atividades. | **Relacionamento:** id_seguidor, id_seguido, data_inicio, notificacoes_ativas<br>**Compartilhamento:** tipo_compartilhamento, destinatarios, mensagem<br>**Comentários:** id_avaliacao, comentario, data_comentario |
| **RF12** | **Sistema de Notificações** | Alertas sobre novos lançamentos, atividades de amigos, recomendações e atualizações do sistema. | **Notificação:** tipo, titulo, mensagem, lida, data_criacao, data_leitura<br>**Configuração:** tipos_habilitados, frequencia, canais (email, push, interna)<br>**Ação:** url_acao, botoes_acao |

### 3.2 Requisitos Não Funcionais do Sistema

| ID | Requisito Não Funcional | Descrição | Especificações Técnicas |
|:---|:-----------------------|:----------|:----------------------|
| **RNF01** | **Usabilidade** | Interface intuitiva e responsiva que funciona adequadamente em dispositivos móveis, tablets e desktops. | **Responsividade:** Breakpoints para mobile (320px+), tablet (768px+), desktop (1024px+)<br>**Acessibilidade:** WCAG 2.1 Level AA, navegação por teclado, leitores de tela<br>**Performance UI:** Tempo de carregamento < 3s, animações suaves 60fps |
| **RNF02** | **Segurança** | Implementar criptografia para dados sensíveis, autenticação segura e prevenção contra ataques comuns. | **Criptografia:** HTTPS/TLS 1.3, bcrypt para senhas (salt rounds ≥ 12)<br>**Autenticação:** JWT com refresh tokens, sessões seguras<br>**Proteção:** CSRF tokens, rate limiting, validação input, headers segurança |
| **RNF03** | **Performance** | Sistema deve suportar múltiplos usuários simultâneos com tempos de resposta adequados. | **Escalabilidade:** Suporte mínimo 1000 usuários simultâneos<br>**Resposta:** APIs < 500ms, queries complexas < 2s<br>**Cache:** Redis para sessões, cache de recomendações, CDN para assets |
| **RNF04** | **Desenvolvimento** | Stack tecnológico definido para frontend, backend e banco de dados. | **Frontend:** React 18+/Next.js 14+, TypeScript, Tailwind CSS<br>**Backend:** Node.js/Express + FastAPI, JWT, validação Joi/Zod<br>**Banco:** PostgreSQL (relacional) + Neo4j (grafos), Redis (cache)<br>**ML:** PyTorch Geometric, scikit-learn, pandas |
| **RNF05** | **Integração** | APIs RESTful e GraphQL para integração com serviços externos e aplicativos de terceiros. | **APIs:** RESTful com OpenAPI 3.0, GraphQL para queries complexas<br>**Externas:** TMDB API, streaming platforms APIs, OAuth providers<br>**Formato:** JSON, paginação, versionamento (v1, v2), rate limiting |
| **RNF06** | **Privacidade** | Controles de privacidade que permitem usuários controlarem visibilidade de dados pessoais. | **Controles:** Perfil público/privado, visibilidade listas/avaliações<br>**LGPD:** Consentimento explícito, direito esquecimento, portabilidade dados<br>**Logs:** Auditoria acessos, retenção dados, anonimização |
| **RNF07** | **Disponibilidade** | Sistema deve ter alta disponibilidade com mecanismos de backup e recuperação. |

### 3.3 Diagrama de Casos de Uso

#### 3.3.1 Atores do Diagrama de Casos de Uso

| Ator | Descrição | Atributos |
|:-----|:----------|:----------|
| **Usuário** | Usuário do sistema que utiliza as funcionalidades para descobrir, avaliar e organizar filmes, com diferentes níveis de engajamento. | **Perfil:** nivel_engajamento (baixo, médio, alto), avaliacoes_totais, listas_criadas, uso_frequencia<br>**Comportamento:** busca_personalizada, interacao_social_opcional, curadoria_pessoal |
| **Administrador** | Responsável pela moderação de conteúdo, gerenciamento de usuários e manutenção do sistema. | **Permissões:** CRUD usuários, moderação conteúdo, analytics sistema<br>**Ferramentas:** dashboard_admin, logs_sistema, configurações_globais |
| **Sistema** | Componente automatizado responsável por gerar recomendações e análises. | **Algoritmos:** collaborative_filtering, content_based, hybrid_approach<br>**Processamento:** batch_jobs, real_time_updates, ML_pipelines |

#### 3.3.2 Descrição dos Casos de Uso Detalhados

---

**[UC01] Gerenciar Perfil de Usuário**
- **Casos de uso relacionados:** [UC02]
- **Pré-condição:** Usuário registrado no sistema
- **Atributos de entrada:** nome, email, senha, foto_perfil, data_nascimento, genero, bio, preferencias_privacidade
- **Atributos de saída:** perfil_atualizado, mensagem_confirmacao, validacoes_erro
- **Descrição:** Criar, visualizar e editar informações do perfil pessoal. Definir preferências de gênero, configurações de privacidade e integração com redes sociais. Relaciona-se com autenticação [UC02].

---

**[UC02] Autenticar no Sistema**
- **Casos de uso relacionados:** Todos os outros casos de uso
- **Pré-condição:** Nenhuma
- **Atributos de entrada:** email, senha, provider_oauth, remember_me, two_factor_code
- **Atributos de saída:** token_jwt, refresh_token, dados_usuario, permissoes
- **Descrição:** Realizar login/logout, registro de nova conta, recuperação de senha e autenticação de dois fatores.

---

**[UC03] Avaliar e Comentar Filmes**
- **Casos de uso relacionados:** [UC04], [UC08]
- **Pré-condição:** Estar autenticado
- **Atributos de entrada:** id_filme, nota (1-5), resenha, publica, tags_personalizadas
- **Atributos de saída:** avaliacao_salva, pontuacao_atualizada, notificacao_seguidores
- **Descrição:** Atribuir ratings de 1-5 estrelas para filmes e escrever resenhas detalhadas. Impacta geração de recomendações [UC04] e estatísticas [UC08].

---

**[UC04] Receber Recomendações Personalizadas**
- **Casos de uso relacionados:** [UC03], [UC05]
- **Pré-condição:** Estar autenticado e ter avaliado pelo menos 5 filmes
- **Atributos de entrada:** contexto_atual, filtros_preferencia, limite_resultados
- **Atributos de saída:** lista_recomendacoes, score_confianca, justificativas, metadados_algoritmo
- **Descrição:** Visualizar filmes recomendados pelo sistema, com explicações sobre critérios utilizados. Baseado em avaliações [UC03] e pode ser filtrado [UC05].

---

**[UC05] Buscar e Filtrar Filmes**
- **Casos de uso relacionados:** [UC06]
- **Pré-condição:** Estar autenticado
- **Atributos de entrada:** termo_busca, generos[], ano_inicio, ano_fim, duracao_min, duracao_max, nota_min, plataformas[]
- **Atributos de saída:** resultados_paginados, filtros_aplicados, contagem_total, sugestoes_refinamento
- **Descrição:** Utilizar sistema de busca avançada com múltiplos filtros (gênero, ano, diretor, etc.). Resultados podem ser adicionados a listas [UC06].

---

**[UC06] Gerenciar Listas de Filmes**
- **Casos de uso relacionados:** [UC09]
- **Pré-condição:** Estar autenticado
- **Atributos de entrada:** nome_lista, descricao, tipo_lista, publica, filmes[], ordenacao
- **Atributos de saída:** lista_criada, estatisticas_lista, opcoes_compartilhamento
- **Descrição:** Criar, editar e organizar listas personalizadas (assistidos, para assistir, favoritos). Listas podem ser compartilhadas com outros usuários [UC09].

---

**[UC07] Visualizar Detalhes de Filme**
- **Casos de uso relacionados:** [UC03], [UC06]
- **Pré-condição:** Estar autenticado
- **Atributos de entrada:** id_filme
- **Atributos de saída:** metadados_completos, trailer_url, disponibilidade_plataformas, avaliacoes_comunidade, recomendacoes_similares
- **Descrição:** Acessar informações completas sobre filmes incluindo metadados, trailer, onde assistir e avaliações da comunidade. Permite avaliar [UC03] ou adicionar a listas [UC06].

---

**[UC08] Visualizar Estatísticas Pessoais**
- **Casos de uso relacionados:** [UC03]
- **Pré-condição:** Estar autenticado e ter histórico de avaliações
- **Atributos de entrada:** periodo_analise, tipo_estatistica
- **Atributos de saída:** metricas_visualizacao, graficos_evolucao, comparacoes_comunidade, insights_personalizados
- **Descrição:** Acessar dashboard com estatísticas de visualização, gêneros preferidos, evolução de gostos e comparações com comunidade.

---

**[UC09] Interagir Socialmente**
- **Casos de uso relacionados:** [UC06], [UC10]
- **Pré-condição:** Estar autenticado
- **Atributos de entrada:** id_usuario_alvo, tipo_interacao, conteudo_compartilhamento
- **Atributos de saída:** relacionamento_atualizado, notificacao_enviada, feed_atualizado
- **Descrição:** Seguir outros usuários, compartilhar listas e recomendações, participar de discussões sobre filmes. Relaciona-se com listas [UC06] e notificações [UC10].

---

**[UC10] Receber Notificações**
- **Casos de uso relacionados:** [UC04], [UC09]
- **Pré-condição:** Estar autenticado e ter configurado preferências
- **Atributos de entrada:** tipos_notificacao[], frequencia, canais_entrega[]
- **Atributos de saída:** notificacoes_personalizadas, configuracoes_atualizadas, historico_entrega
- **Descrição:** Receber alertas sobre novos lançamentos relevantes, atividades de amigos e atualizações de recomendações.

---

**[UC11] Explorar Modo Descoberta**
- **Casos de uso relacionados:** [UC05], [UC06]
- **Pré-condição:** Estar autenticado
- **Atributos de entrada:** modo_descoberta, contexto_atual, historico_exploração
- **Atributos de saída:** filmes_curados, categorias_tematicas, tendencias_comunidade, surpresas_personalizadas
- **Descrição:** Navegar por categorias especializadas, filmes temáticos, diretores em destaque e tendências da comunidade. Combina aspectos de busca [UC05] e gerenciamento de listas [UC06].

---
