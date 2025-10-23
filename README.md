# Dinâmica: Design Estratégico do Projeto

## Objetivo
Identificar os subdomínios do projeto, classificá-los (Core, Supporting, Generic) e desenhar os bounded contexts, incluindo suas interações. Esse exercício ajudará a criar uma visão clara e estratégica do domínio.

---

## 1. Nome do Projeto
Life Sync

---

## 2. Objetivo Principal do Projeto
Criar uma solução digital gamificada que incentive o autocuidado físico e mental de colaboradores por meio de missões mensais, recompensas e um ranking saudável, promovendo engajamento e bem-estar de forma leve e participativa.

---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

| **Subdomínio** | **Descrição** | **Tipo** |
| :--- | :--- | :--- |
| Gamificação e Jornada | Gerencia os desafios, o progresso (pontuação, ranking, conquistas) e o fluxo da jornada de bem-estar do colaborador. É o diferencial competitivo do negócio. | Core Domain |
| Gestão de Conteúdo/Missões | Criação, gestão e fornecimento dos materiais educativos, missões e micro-intervenções que alimentam os desafios de bem-estar. | Supporting |
| Comunidade e Feed | Gerencia a interação social entre os colaboradores (feed de notícias, publicações de conquistas, comentários e curtidas). | Supporting |
| Cadastro de Colaboradores/Empresas | Gerencia o ciclo de vida das contas corporativas e os perfis detalhados dos colaboradores. | Supporting |
| Análise de Impacto/Dashboards | Processa os dados de engajamento e saúde para gerar relatórios e KPIs consolidados para os gestores da empresa. | Supporting |
| Autenticação e Autorização | Gerencia o login, a segurança de senhas e os níveis de permissão dos diferentes tipos de usuários. | Generic |
| Pagamentos (B2B) | Processa a cobrança e gestão de faturas das empresas clientes (B2B) pela utilização da plataforma. | Generic |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context** | **Responsabilidade** | **Subdomínios Relacionados** |
| :--- | :--- | :--- |
| Contexto de Jornada do Colaborador | É o núcleo do sistema. Responsável por iniciar e progredir o colaborador nos desafios, registrar a conclusão de atividades, calcular a pontuação e gerenciar o ranking. | Gamificação e Jornada |
| Contexto de Conteúdo e Missões | Responsável por fornecer os conteúdos (vídeos, artigos, quizzes) e as regras específicas das missões que alimentam a Jornada. | Gestão de Conteúdo/Missões |
| Contexto de Comunidade | Gerencia as interações sociais. Recebe eventos de conquistas e progresso e os publica no feed, permitindo interação entre os usuários. | Comunidade e Feed |
| Contexto de Análise Corporativa | Focado em transformar dados brutos de engajamento (vindos da Jornada) em informações estratégicas (KPIs, Dashboards) para os gestores da empresa. | Análise de Impacto/Dashboards |
| Contexto de Contas e Usuários | Gerencia o ciclo de vida e as informações cadastrais dos usuários e das empresas clientes. | Cadastro de Colaboradores/Empresas |
| Contexto de Identidade e Acesso | Focado exclusivamente em validar as credenciais do usuário e gerenciar permissões. Idealmente, delega a complexidade de segurança para um serviço especializado. | Autenticação e Autorização |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)** | **Para (Destino)** | **Forma de Comunicação** | **Exemplo de Evento/Chamada** |
| :--- | :--- | :--- | :--- |
| Contexto de Identidade e Acesso | Contexto de Jornada do Colaborador | Cadastro realizado. | Usuário recebe acesso à plataforma. |
| Contexto de Conteúdo e Missões | Contexto de Jornada do Colaborador | Conteúdo disponível para os usuários. | Usuário assiste um conteúdo sobre saúde e responde um quiz. |
| Contexto de Jornada do Colaborador | Contexto de Comunidade | Conquista é publicada no feed | Usuário completa desafios e compartilha com a rede de amigos. |
| Contexto de Jornada do Colaborador | Contexto de Análise Corporativa | Gerado dashboards. | Empresa recebe dashboards e dados sobre os resultados dos colaboradores. |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo** | **Descrição** |
| :--- | :--- |
| **Participante** | O colaborador de uma empresa que se inscreve e participa dos desafios de bem-estar. |
| **Desafio** | O ciclo de gamificação principal (ex: mensal), composto por um conjunto de Missões e Atividades com um objetivo de saúde. |
| **Missão** | Um objetivo temático dentro de um Desafio (ex: "Hidratação Certa"), que agrupa Atividades. |
| **Atividade** | A menor unidade de ação que o Participante deve completar para ganhar Pontos (ex: "Assistir vídeo sobre alongamento", "Responder Quiz"). |
| **Pontuação (Pontos)** | O valor numérico que o Participante acumula ao completar Atividades e Missões. É a base para o Ranking. |
| **Ranking** | A classificação dos Participantes em um Desafio, ordenada pela Pontuação total acumulada. |
| **Conquista** | Um prêmio simbólico ou distintivo recebido por alcançar um marco específico (ex: "Concluiu 5 dias seguidos"). |
| **Gestor (ou Gestor de Bem-Estar)** | O usuário da empresa (RH, benefícios) responsável por acompanhar os resultados da equipe (via Dashboard) e gerenciar os Desafios. |
| **Dashboard** | O painel de análise que consolida os KPIs e os resultados da Pontuação e Engajamento para os Gestores. |
---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Desenvolver internamente com foco total.
- **Supporting Subdomain:** Desenvolver internamente ou parcialmente terceirizar.
- **Generic Subdomain:** Usar ferramentas ou serviços de mercado.

| **Subdomínio** | **Estratégia** | **Ferramentas ou Serviços (se aplicável)** |
| :--- | :--- | :--- |
| **Gamificação e Jornada** (Core) | **Desenvolvimento Interno com Foco Total.** É a inteligência do negócio; deve ser construída pela equipe. | - |
| **Gestão de Conteúdo/Missões** (Supporting) | **Desenvolvimento Interno.** Permite total controle sobre a estrutura dos desafios e a experiência do usuário. | Sistema de Gerenciamento de Conteúdo (CMS) headless como Strapi ou Contentful. |
| **Comunidade e Feed** (Supporting) | **Desenvolvimento Interno/Parcialmente Terceirizar.** O feed é crucial para o engajamento, mas a notificação/mensageria pode ser terceirizada. | Serviço de Notificação (ex: Firebase Cloud Messaging, AWS SNS). |
| **Cadastro de Colaboradores/Empresas** (Supporting) | **Desenvolvimento Interno.** A complexidade do modelo B2B (Empresa -> Colaborador) exige controle interno. | - |
| **Análise de Impacto/Dashboards** (Supporting) | **Desenvolvimento Interno e Ferramentas de BI.** A lógica de cálculo de KPIs é interna, mas a visualização pode usar ferramentas de mercado. | Ferramenta de BI (ex: Metabase, Tableau, Power BI). |
| **Autenticação e Autorização** (Generic) | **Terceirizar usando Serviço Especializado.** Não é o foco do negócio e exige alta segurança. | Auth0, Firebase Auth, AWS Cognito. |
| **Pagamentos (B2B)** (Generic) | **Terceirizar usando API de Pagamentos.** Uso de gateways de mercado para gestão de assinaturas e faturamento B2B. | Stripe, PagSeguro, Vindi. |

---

## 8. Diagrama Visual (Opcional, mas Recomendado)
Desenhe um diagrama que mostre:
- Os bounded contexts.
- Como eles se comunicam.
- A relação com os subdomínios.

Use ferramentas como **Miro**, **Lucidchart** ou mesmo papel e caneta para criar seu diagrama e adicionar ao projeto.

---

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀
