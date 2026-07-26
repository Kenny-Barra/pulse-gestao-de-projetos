# Parte Teórica — Do Problema ao Produto

**Produto:** Pulse — Plataforma de Inteligência de Atendimento com IA Generativa
**Disciplina:** Fundamentos de Gestão de Projetos
**Autor:** Kenedy Pereira
**Data:** Julho de 2026

---

## Sumário

1. [Visão de Produto](#1-visão-de-produto)
2. [Definição do MVP](#2-definição-do-mvp)
3. [Roadmap do Produto](#3-roadmap-do-produto)
4. [Ciclo de Vida da Aplicação](#4-ciclo-de-vida-da-aplicação)
5. [Gerenciamento de Riscos](#5-gerenciamento-de-riscos)
6. [Gestão de Produtos e IA](#6-gestão-de-produtos-e-ia)
7. [Referências](#7-referências)

---

## Contexto do desafio

Um *startup studio* está incubando um produto digital apoiado em IA Generativa para um cliente
corporativo. O time interno de atendimento do cliente recebe um volume gigantesco de interações
— tickets, chats e e-mails — e enfrenta dois problemas encadeados:

1. **Não consegue priorizar temas críticos.** A análise é feita por amostragem manual, o que gera
   viés de seleção e atraso na detecção de problemas.
2. **Não consegue gerar planos de ação rápidos.** Mesmo quando um tema é identificado, não há
   evidência estruturada nem dono definido para transformá-lo em ação.

O desafio de gestão, portanto, não é "aplicar IA em textos". É **entregar decisão priorizada com
evidência rastreável, rápido o bastante para importar e barato o bastante para escalar**.

---

## 1. Visão de Produto

### 1.1 Descrição do produto digital

**Pulse** é uma plataforma SaaS que conecta as fontes de atendimento de uma empresa (Zendesk,
Freshdesk, Intercom, caixas de e-mail e exportações CSV), processa **100% das interações** com
uma combinação de *embeddings* + *clustering* + LLM, e devolve:

- um **painel de temas** agrupados automaticamente, ordenados por criticidade;
- um **resumo executivo** por tema, com as citações originais que sustentam a conclusão;
- um **plano de ação sugerido**, com dono e esforço estimado, exportável para Jira/Notion/Slack.

O produto **não substitui o atendimento**. Ele atua na camada acima: transforma o histórico de
atendimento em insumo de decisão para produto, operações e liderança.

> **Declaração de visão (Product Vision Statement)**
>
> *Para* líderes de CX e de Produto em empresas que operam alto volume de atendimento,
> *que* precisam entender o que os clientes estão dizendo mas não conseguem ler tudo,
> *o* **Pulse** *é uma* plataforma de inteligência de atendimento
> *que* transforma 100% das interações em temas priorizados e planos de ação em minutos.
> *Diferente de* dashboards de BI e de tagueamento manual,
> *nosso produto* explica **por que** cada tema importa, mostra a **evidência bruta** que sustenta
> a conclusão e entrega o **próximo passo** já formatado para execução.

### 1.2 Público-alvo e problema atendido

| Perfil | Papel na decisão | Dor principal | O que o Pulse entrega |
|---|---|---|---|
| **Head / Coordenador de CX** | Comprador econômico | Cobrado por CSAT e custo por ticket, mas decide "no achismo" | Priorização defensável, com números e evidência |
| **Analista de Qualidade / CX Insights** | Usuário primário (diário) | Passa 60–70% do tempo tagueando e montando planilha | Recupera o tempo e vira gerador de insight, não de planilha |
| **Product Manager** | Usuário secundário | Backlog cheio, sem sinal confiável do que dói mais | Fila de problemas reais, ligada a volume e receita em risco |
| **Diretoria / COO** | Patrocinador | Descobre crises tarde demais | Alerta de tema emergente e resumo executivo semanal |

**Perfil de empresa-alvo (ICP):** empresas B2C ou B2B SaaS com **5.000+ interações/mês**, time de
CX de 10 a 200 pessoas, que já usam uma ferramenta de *helpdesk* e possuem alguma estrutura de
dados. Abaixo desse volume a leitura manual ainda é viável e o produto não se paga.

**Problema atendido, em uma frase:**
> A empresa já **tem** a resposta para "o que está quebrado" dentro do próprio atendimento — mas
> ela está diluída em dezenas de milhares de textos que ninguém consegue ler.

**Quantificação da dor (hipótese a validar na descoberta):**
- Um analista lê ~40 tickets/dia → cobre menos de **3%** do volume de uma operação média.
- O ciclo "perceber problema → levar para produto" leva **3 a 6 semanas**.
- Estima-se **15–25% dos tickets** como recorrentes e evitáveis na origem.

### 1.3 Proposta de valor

> **"De 100% das conversas com seus clientes para 5 decisões priorizadas — toda segunda-feira,
> às 8h, com a evidência anexada."**

Os quatro pilares da proposta de valor:

| Pilar | Promessa | Como se prova |
|---|---|---|
| **Cobertura** | 100% das interações analisadas, não uma amostra | Comparativo de cobertura vs. processo manual atual |
| **Velocidade** | De semanas para minutos no ciclo dado → insight | Tempo até o primeiro insight acionável (TTFI) < 30 min |
| **Confiança** | Todo insight vem com as citações originais | Taxa de insights com evidência rastreável = 100% |
| **Ação** | Termina em plano de ação com dono, não em gráfico | % de temas que viram tarefa em ferramenta externa |

**Métrica North Star:** *número de planos de ação executados originados de insights do Pulse por
mês.* Foi escolhida deliberadamente no lugar de métricas de vaidade (usuários ativos, temas
gerados) porque só ela captura o valor real: **o produto só vale se mudar o que a empresa faz.**

---

## 2. Definição do MVP

### 2.1 Princípio orientador

O MVP do Pulse foi desenhado para responder **uma única pergunta de risco**:

> *A classificação automática de temas é boa o bastante para que um líder de CX tome uma decisão
> com base nela, sem reler os tickets?*

Tudo que não ajuda a responder essa pergunta ficou **fora** do MVP. Este é um MVP de **risco
técnico e de valor**, não de escala: não há multi-tenant robusto, não há SSO corporativo, não há
app mobile. Se a resposta for "não", nenhuma dessas coisas importaria.

### 2.2 Funcionalidades essenciais do MVP

| # | Funcionalidade | Descrição | Prioridade |
|---|---|---|---|
| F1 | **Ingestão de dados** | Upload CSV + conector Zendesk (somente leitura) | Must |
| F2 | **Normalização e anonimização (PII)** | Remoção/mascaramento de CPF, e-mail, telefone e cartão antes de qualquer envio ao LLM | Must |
| F3 | **Clusterização automática de temas** | Embeddings + clustering, com rótulo do tema gerado por LLM | Must |
| F4 | **Painel de temas priorizados** | Ranking por volume × tendência × sentimento, com filtro por período | Must |
| F5 | **Evidência rastreável** | Cada tema exibe de 3 a 5 trechos originais que o sustentam, com link para o ticket | Must |
| F6 | **Resumo executivo semanal** | Digest com os 5 temas críticos e plano de ação sugerido por tema | Must |
| F7 | **Feedback do usuário no tema** | Botões "tema correto / incorreto / mesclar" para calibração | Must |
| F8 | **Exportar relatório** | Exportação em PDF/CSV e envio para Slack | Should |
| F9 | Alerta de anomalia em tempo real | Notificação quando um tema cresce acima do baseline | Could → Fase 2 |
| F10 | Chat conversacional com os dados | "Pergunte aos seus tickets" | Won't → Fase 3 |
| F11 | Previsão de churn por tema | Modelo preditivo ligado a receita | Won't → Fase 3 |

**Escopo negativo explícito (o que o MVP *não* faz):** não responde tickets, não avalia
desempenho individual de atendentes, não escreve no *helpdesk*, não suporta áudio/voz, não tem
multi-idioma além de português e inglês.

### 2.3 Justificativa de priorização (valor × viabilidade)

A priorização combinou **MoSCoW** (para o corte de escopo) com **RICE** (para ordenar dentro do
"Must"), e foi validada contra a **matriz Valor × Esforço**.

| Funcionalidade | Alcance | Impacto | Confiança | Esforço (sem.) | **RICE** | Decisão |
|---|---|---|---|---|---|---|
| F3 Clusterização | 100% | 3,0 | 70% | 6 | **35,0** | Núcleo — é o produto |
| F4 Painel priorizado | 100% | 3,0 | 90% | 3 | **90,0** | Núcleo — é a entrega de valor |
| F5 Evidência rastreável | 100% | 2,5 | 90% | 2 | **112,5** | Núcleo — mitiga alucinação |
| F6 Resumo executivo | 80% | 3,0 | 80% | 3 | **64,0** | Núcleo — cria o hábito semanal |
| F1 Ingestão | 100% | 2,0 | 95% | 3 | **63,3** | Pré-requisito técnico |
| F2 Anonimização | 100% | 2,0 | 95% | 2 | **95,0** | Pré-requisito legal (LGPD) |
| F7 Feedback | 70% | 1,5 | 85% | 1 | **89,3** | Barato e gera dado de calibração |
| F8 Exportação | 60% | 1,0 | 90% | 1 | **54,0** | Should — entra se sobrar folga |
| F9 Alertas | 50% | 2,0 | 60% | 4 | **15,0** | Adiado — depende de baseline histórico |
| F10 Chat com dados | 40% | 1,5 | 40% | 8 | **3,0** | Adiado — alto custo, valor não provado |

**Racional das quatro decisões mais relevantes:**

1. **F5 (Evidência) é Must, embora pareça "detalhe de UI".** É a mitigação de produto para o maior
   risco técnico do projeto — alucinação do LLM. Sem citação verificável, um único insight errado
   destrói a confiança e o produto morre. É a funcionalidade de maior RICE justamente por ser
   barata e proteger todo o resto.
2. **F2 (Anonimização) é Must mesmo sem gerar valor percebido.** É requisito legal (LGPD) e
   condição de compra: nenhum jurídico corporativo aprova envio de dado pessoal de cliente para
   API de terceiro sem tratamento. É custo de entrada, não diferencial.
3. **F9 (Alertas) foi adiado por dependência, não por falta de valor.** Detectar anomalia exige
   *baseline* histórico que só existe depois de meses de uso. Construir antes seria desperdício.
4. **F10 (Chat com dados) foi adiado por disciplina.** É a funcionalidade que mais impressiona em
   demo e a que menos resolve o problema declarado do cliente — que é **priorização**, não
   consulta. Entrou como Won't para evitar que o time construísse a versão bonita em vez da
   versão útil.

### 2.4 Critério de sucesso do MVP

O MVP é considerado **bem-sucedido** se, ao final de 8 semanas com 3 clientes-piloto:

| Critério | Meta |
|---|---|
| Precisão da classificação de temas (validada por especialista) | ≥ 80% |
| Temas úteis entre os 5 principais, na avaliação do líder de CX | ≥ 4 de 5 |
| Tempo até o primeiro insight acionável (TTFI) | < 30 minutos |
| Planos de ação efetivamente executados por cliente/mês | ≥ 3 |
| Retenção semanal do usuário primário (W4) | ≥ 60% |
| Custo de inferência por 1.000 tickets | ≤ R$ 25,00 |

Se a precisão ficar entre 60% e 80%, o veredito é **iterar** (ajustar prompt/modelo, mais rodadas
de feedback). Abaixo de 60%, o veredito é **pivotar** a abordagem técnica (fine-tuning ou
taxonomia assistida em vez de clustering aberto).

---

## 3. Roadmap do Produto

O roadmap é **orientado a objetivos e a hipóteses**, não a datas fixas de funcionalidade. Cada
fase existe para derrubar um risco específico; as datas são estimativas de planejamento, sujeitas
a revisão ao final de cada fase.

### Fase 1 — Descoberta e MVP *(Meses 1–3)*

**Objetivo:** provar que a IA classifica temas com precisão aceitável e que o insight gerado é
percebido como útil.
**Hipótese sob teste:** *"Um líder de CX confia no ranking automático de temas o suficiente para
agir sem reler os tickets."*

| Entregável | Descrição |
|---|---|
| Pesquisa de descoberta | 12 entrevistas com líderes de CX + análise de 3 bases reais |
| Protótipo navegável | Fluxo principal validado com 5 usuários antes de escrever código |
| Pipeline de ingestão + anonimização | F1, F2 |
| Motor de clusterização e rotulagem | F3 |
| Painel de temas + evidência | F4, F5 |
| Resumo executivo semanal | F6, F7 |
| Programa de 3 clientes-piloto | 8 semanas de uso monitorado |

**Métricas-alvo:** precisão ≥ 80%; TTFI < 30 min; 3 pilotos ativos; NPS do piloto ≥ 30.

---

### Fase 2 — Validação e Ação *(Meses 4–6)*

**Objetivo:** transformar insight em ação recorrente e provar disposição a pagar.
**Hipótese sob teste:** *"As empresas pagam por isso e o insight vira mudança operacional."*

| Entregável | Descrição |
|---|---|
| Alertas de anomalia | F9 — spike de tema acima do baseline |
| Integrações de saída | Jira, Slack, Notion — o plano vira tarefa em 1 clique |
| Acompanhamento de ação | Status do plano e impacto no volume do tema após a correção |
| Gestão de taxonomia | Cliente edita, mescla e fixa temas |
| Multiusuário e permissões | Papéis de admin, analista e leitor |
| Cobrança e planos | Primeira monetização real |

**Métricas-alvo:** 10 clientes pagantes; ≥ 3 planos de ação executados/cliente/mês; retenção
mensal ≥ 85%; redução mensurável de volume em ao menos 1 tema por cliente.

---

### Fase 3 — Escala e Inteligência Preditiva *(Meses 7–12)*

**Objetivo:** escalar a base e aumentar a profundidade analítica, saindo do descritivo para o
preditivo.
**Hipótese sob teste:** *"O produto se sustenta economicamente em escala e a análise preditiva
aumenta a retenção."*

| Entregável | Descrição |
|---|---|
| Conectores adicionais | Intercom, Freshdesk, Salesforce, WhatsApp Business |
| Análise de causa-raiz | Cruzamento entre temas, jornada e versão do produto |
| Impacto financeiro por tema | Receita em risco e custo operacional associado |
| Sinal preditivo de churn | Modelo ligando temas recorrentes a cancelamento |
| Otimização de custo de IA | Cache semântico, modelos menores em cascata, *batching* |
| Segurança corporativa | SSO/SAML, trilha de auditoria, retenção configurável |

**Métricas-alvo:** 50 clientes; margem bruta ≥ 70%; custo de inferência reduzido em 40%;
expansão de receita (NRR) ≥ 110%.

---

### Fase 4 — Plataforma e Ecossistema *(Mês 13+)*

**Objetivo:** deixar de ser ferramenta e virar camada de inteligência do cliente.
**Hipótese sob teste:** *"O valor cresce quando terceiros constroem sobre o Pulse."*

| Entregável | Descrição |
|---|---|
| API pública e webhooks | Acesso programático aos temas e insights |
| Benchmark setorial | Comparação anônima e agregada entre empresas do mesmo setor |
| Agentes de ação | Sugestão automática de atualização de base de conhecimento/macros |
| Suporte multi-idioma e voz | Transcrição de ligações e análise multilíngue |

**Métricas-alvo:** 20% dos clientes usando API; ≥ 2 parceiros de integração; ampliação do ICP.

---

### Visão consolidada

| | Fase 1 | Fase 2 | Fase 3 | Fase 4 |
|---|---|---|---|---|
| **Período** | Mês 1–3 | Mês 4–6 | Mês 7–12 | Mês 13+ |
| **Foco** | Provar o valor | Provar o negócio | Escalar | Expandir |
| **Risco atacado** | Técnico | Mercado | Econômico | Estratégico |
| **Pergunta** | Funciona? | Pagam? | Escala com margem? | Vira plataforma? |
| **Marco** | 3 pilotos, 80% precisão | 10 clientes pagantes | 50 clientes, 70% margem | API pública |

---

## 4. Ciclo de Vida da Aplicação

O ciclo de vida adotado é **incremental e iterativo**, com quatro fases e **portões de decisão
(*gates*)** entre elas. O princípio é que **nenhuma fase avança por prazo cumprido, e sim por
evidência produzida** — uma fase pode ser repetida quantas vezes for necessário.

```
┌─────────────┐   G1   ┌─────────────┐   G2   ┌─────────────┐   G3   ┌─────────────┐
│ DESCOBERTA  │ ─────► │  VALIDAÇÃO  │ ─────► │   ENTREGA   │ ─────► │   EVOLUÇÃO  │
│  (4 sem.)   │        │  (8 sem.)   │        │ (contínuo)  │        │ (contínuo)  │
└─────────────┘        └─────────────┘        └─────────────┘        └─────────────┘
       ▲                      │                      │                      │
       └──────────────────────┴──────────────────────┴──────────────────────┘
                        retorno em caso de invalidação
```

### 4.1 Fase de Descoberta *(≈ 4 semanas)*

**Objetivo:** entender o problema com profundidade e reduzir a incerteza antes de investir em
construção.

- Entrevistas com usuários e patrocinador; mapeamento da jornada atual do analista.
- Análise exploratória de bases reais de tickets (volume, ruído, presença de PII, idioma).
- Prova de conceito técnica isolada: clusterização em uma amostra de 5.000 tickets.
- Protótipo navegável e teste de usabilidade com 5 usuários.
- Lean Canvas preenchido e riscos mapeados.

### 4.2 Fase de Validação *(≈ 8 semanas)*

**Objetivo:** construir o MVP e testá-lo em ambiente real com clientes-piloto.

- Desenvolvimento em *sprints* de 2 semanas, com incremento potencialmente utilizável ao fim de
  cada uma (referência: Scrum Guide 2020).
- Implantação com 3 clientes-piloto e acompanhamento semanal.
- Medição contínua contra os critérios de sucesso do MVP (seção 2.4).
- Calibração do modelo com o *feedback* coletado em F7.

### 4.3 Fase de Entrega *(contínua, a partir do mês 4)*

**Objetivo:** disponibilizar o produto comercialmente com estabilidade e previsibilidade.

- Endurecimento de segurança, desempenho e observabilidade.
- Documentação, *onboarding* assistido e material de suporte.
- Ativação de cobrança e definição de SLA.
- Cadência de *release* quinzenal com *feature flags* e implantação gradual.

### 4.4 Fase de Evolução *(contínua)*

**Objetivo:** crescer em valor, eficiência e alcance, evitando a degradação silenciosa típica de
produtos de IA.

- Monitoramento de *drift* do modelo e reavaliação trimestral de precisão.
- Otimização contínua de custo de inferência.
- Expansão de conectores e capacidades analíticas.
- **Descontinuação planejada:** funcionalidades com uso abaixo de 5% da base são revisadas e
  removidas para conter complexidade acumulada.

### 4.5 Critérios de avanço entre fases (*gates*)

| Portão | Transição | Critérios obrigatórios | Decisão possível |
|---|---|---|---|
| **G1** | Descoberta → Validação | Problema confirmado em ≥ 8 de 12 entrevistas; PoC atinge ≥ 70% de coerência nos clusters; ≥ 3 empresas aceitam ser piloto; escopo do MVP aprovado pelo patrocinador | Avançar / Repetir descoberta / Encerrar |
| **G2** | Validação → Entrega | Precisão ≥ 80%; TTFI < 30 min; retenção W4 ≥ 60%; ≥ 3 planos de ação executados por piloto; ≥ 2 pilotos declarando intenção de compra; custo/1.000 tickets ≤ R$ 25 | Avançar / Iterar MVP / Pivotar |
| **G3** | Entrega → Evolução | 10 clientes pagantes; disponibilidade ≥ 99,5% em 60 dias; churn mensal < 5%; margem bruta ≥ 60%; zero incidente crítico de segurança/LGPD | Avançar / Estabilizar antes de escalar |
| **G4** | Revisão contínua (trimestral) | Precisão mantida ≥ 80%; NRR ≥ 100%; custo unitário estável ou em queda | Investir / Manter / Descontinuar |

**Regra de governança:** o *gate* é avaliado em reunião formal com PM, tech lead e patrocinador,
com decisão registrada. Critério não atendido **não é negociado com prazo** — ou o time itera na
fase atual, ou a decisão de avançar é assumida explicitamente como risco documentado, com
responsável nomeado.

---

## 5. Gerenciamento de Riscos

### 5.1 Metodologia

Seguindo as práticas de gerenciamento de riscos do PMI, cada risco foi **identificado**,
**analisado qualitativamente** (probabilidade × impacto), **priorizado por exposição** e associado
a uma **estratégia de resposta** e a um **responsável**.

**Escalas adotadas:**

| Nível | Probabilidade | Impacto |
|---|---|---|
| 1 – Muito baixa/o | < 10% | Efeito desprezível |
| 2 – Baixa/o | 10–30% | Atraso ≤ 1 semana |
| 3 – Média/o | 30–60% | Atraso de 2–4 semanas ou perda de 1 piloto |
| 4 – Alta/o | 60–85% | Atraso > 1 mês ou falha em *gate* |
| 5 – Muito alta/o | > 85% | Inviabiliza o produto |

**Exposição = Probabilidade × Impacto.** Classificação: 1–6 Baixo · 8–12 Médio · 15–25 Crítico.
**Estratégias de resposta a ameaças:** Mitigar, Evitar, Transferir, Aceitar.

### 5.2 Matriz de riscos

| ID | Risco | Categoria | P | I | Exp. | Nível | Estratégia | Plano de mitigação | Responsável |
|---|---|---|---|---|---|---|---|---|---|
| **R01** | Baixa precisão na clusterização torna os temas inúteis | Técnico | 4 | 5 | **20** | 🔴 Crítico | Mitigar | PoC antes de codificar; conjunto de teste rotulado por especialista; ciclo de feedback (F7); plano B com taxonomia assistida | Tech Lead de IA |
| **R02** | Alucinação do LLM gera insight falso e destrói a confiança | Técnico/IA | 4 | 5 | **20** | 🔴 Crítico | Mitigar | Evidência obrigatória (F5); *grounding* estrito no texto-fonte; recusa quando não há suporte; avaliação automatizada por amostragem a cada *release* | Tech Lead de IA |
| **R03** | Vazamento ou uso indevido de dado pessoal (LGPD) | Conformidade | 3 | 5 | **15** | 🔴 Crítico | Mitigar / Transferir | Anonimização antes da inferência (F2); contrato de não-treinamento com o fornecedor; DPA e criptografia; revisão jurídica antes do piloto; seguro cibernético | DPO + PM |
| **R04** | Custo de inferência inviabiliza a margem em escala | Financeiro | 4 | 4 | **16** | 🔴 Crítico | Mitigar | Teto de custo por cliente com alerta; cache semântico; cascata de modelos; medição de custo unitário desde a semana 1 | PM + Tech Lead |
| **R05** | Baixa adoção: o insight é lido mas não vira ação | Mercado/Produto | 3 | 5 | **15** | 🔴 Crítico | Mitigar | *Onboarding* assistido; ritual semanal de revisão com o cliente; integração 1-clique com Jira/Slack; North Star medindo ação, não acesso | PM |
| **R06** | Qualidade ruim dos dados do cliente (ruído, duplicidade, multi-idioma) | Técnico/Dados | 4 | 3 | **12** | 🟠 Médio | Mitigar | Diagnóstico de dados como pré-requisito de contrato; camada de limpeza; relatório de qualidade transparente ao cliente | Engenheiro de Dados |
| **R07** | Dependência de fornecedor único de LLM (*vendor lock-in*) | Técnico/Estratégico | 3 | 4 | **12** | 🟠 Médio | Mitigar | Camada de abstração de provedor; homologação de fornecedor alternativo desde a Fase 1; teste de portabilidade trimestral | Arquiteto |
| **R08** | Concorrente estabelecido lança funcionalidade equivalente | Mercado | 4 | 3 | **12** | 🟠 Médio | Aceitar / Mitigar | Foco no diferencial de "insight → ação com evidência"; velocidade de entrega; profundidade vertical em vez de amplitude | PM |
| **R09** | Resistência interna do time de CX (medo de substituição) | Organizacional | 3 | 3 | **9** | 🟠 Médio | Mitigar | Comunicação explícita de não-uso para avaliação individual; envolver analistas como cocriadores; treinamento e nova narrativa de papel | PM + RH do cliente |
| **R10** | Atraso na integração com o *helpdesk* (API, limites, aprovações) | Cronograma | 3 | 3 | **9** | 🟠 Médio | Mitigar | Ingestão por CSV como caminho de contingência no MVP; validar acesso à API no *kickoff* | Tech Lead |
| **R11** | Degradação silenciosa do modelo (*drift*) ao longo do tempo | Técnico/IA | 3 | 3 | **9** | 🟠 Médio | Mitigar | Monitoramento contínuo de métricas de qualidade; reavaliação trimestral com conjunto de teste; alerta de queda de precisão | Tech Lead de IA |
| **R12** | Perda de pessoa-chave do time (especialista em IA) | Recursos | 2 | 4 | **8** | 🟠 Médio | Mitigar | Documentação de arquitetura e decisões (ADRs); programação em par nos módulos críticos; sem *bus factor* = 1 | PM |
| **R13** | Escopo do MVP inflar durante os pilotos (*scope creep*) | Cronograma | 4 | 2 | **8** | 🟠 Médio | Evitar | Escopo negativo documentado; pedidos vão para backlog da Fase 2; *gate* G2 como trava formal | PM |
| **R14** | Viés algorítmico desprioriza temas de grupos minoritários | Ético/IA | 2 | 4 | **8** | 🟠 Médio | Mitigar | Auditoria de distribuição de temas por segmento; revisão humana dos temas de baixo volume e alto impacto; painel de temas emergentes | PM + Tech Lead de IA |
| **R15** | Indisponibilidade da API do fornecedor de LLM | Operacional | 2 | 3 | **6** | 🟢 Baixo | Mitigar | Processamento assíncrono com fila e reprocessamento; provedor secundário configurado; degradação graciosa | Arquiteto |

### 5.3 Mapa de calor

|  | I=1 | I=2 | I=3 | I=4 | I=5 |
|---|---|---|---|---|---|
| **P=5** | | | | | |
| **P=4** | | R13 | R06, R08 | R04 | R01, R02 |
| **P=3** | | | R09, R10, R11 | R07 | R03, R05 |
| **P=2** | | | R15 | R12, R14 | |
| **P=1** | | | | | |

🔴 Crítico (≥15) · 🟠 Médio (8–12) · 🟢 Baixo (≤6)

### 5.4 Governança de riscos

- **Revisão quinzenal** dos riscos críticos na *sprint review*; revisão completa a cada *gate*.
- **Gatilhos definidos** para cada risco crítico. Exemplos:
  - *R01:* precisão medida < 70% em qualquer *sprint* → aciona o plano B de taxonomia assistida.
  - *R04:* custo unitário > R$ 40/1.000 tickets por 2 semanas → congela novos pilotos e prioriza otimização.
  - *R05:* menos de 1 plano de ação executado por piloto no mês → sessão de diagnóstico com o cliente em 5 dias.
- **Reserva de contingência** de 20% do cronograma da Fase 1, alocada explicitamente para R01 e R06.
- Riscos aceitos são **registrados com justificativa e responsável**, não apenas ignorados.

---

## 6. Gestão de Produtos e IA

### 6.1 Riscos específicos do uso de IA

Produtos com IA Generativa introduzem uma classe de risco ausente no software tradicional: a
saída é **probabilística, não determinística**. Isso muda a natureza da gestão do produto.

| Risco | Por que é específico de IA | Como o Pulse trata |
|---|---|---|
| **Alucinação** | O modelo produz texto plausível sem base factual | Evidência obrigatória (F5); *grounding* estrito; recusa explícita quando não há suporte no texto |
| **Não-determinismo** | A mesma entrada pode gerar saídas diferentes | Temperatura baixa; versionamento de *prompt* e de modelo; conjunto de regressão a cada mudança |
| **Viés** | O modelo reproduz padrões dos dados de treino e do próprio histórico da empresa | Auditoria de distribuição de temas; revisão humana de temas de baixo volume; painel de emergentes |
| **Drift** | A qualidade cai sem que nenhuma linha de código mude | Monitoramento contínuo; reavaliação trimestral; alerta automático de queda |
| **Custo variável** | O custo cresce com o uso, não com o número de licenças | Custo unitário como métrica de produto; teto por cliente; cascata de modelos |
| **Opacidade** | Não há explicação causal para a saída | A evidência substitui a explicabilidade: mostra-se *o que sustenta*, não *como o modelo pensou* |
| **Dependência de terceiro** | Preço, política e disponibilidade estão fora do controle do time | Abstração de provedor; alternativa homologada |

**Consequência para a gestão:** o *Definition of Done* de uma funcionalidade de IA inclui
**métrica de qualidade medida**, não apenas "código em produção". E a estimativa de esforço passa
a carregar incerteza maior, o que exige *timeboxes* de pesquisa em vez de estimativas fechadas.

### 6.2 Considerações éticas, de segurança e confiabilidade

**Ética**

1. **Não-vigilância — restrição de produto assumida.** O Pulse analisa **temas**, não pessoas. Não
   produz ranking de desempenho individual de atendentes, mesmo sendo tecnicamente trivial. É uma
   decisão de produto: viabilizaria uso punitivo, destruiria a confiança dos analistas (R09) e
   traria exposição trabalhista ao cliente.
2. **Transparência.** Todo conteúdo gerado por IA é rotulado como tal na interface. O usuário
   sempre sabe o que é dado e o que é inferência.
3. **Humano no circuito.** O Pulse **recomenda**; a decisão é sempre humana. Nenhuma ação é
   executada automaticamente no MVP.
4. **Consentimento e finalidade.** O cliente é orientado a informar seus consumidores sobre o
   tratamento analítico das interações, respeitando a finalidade declarada na coleta.

**Segurança e privacidade**

1. **Minimização de dados:** anonimização de PII antes de qualquer chamada ao LLM (F2).
2. **Isolamento por cliente:** segregação lógica dos dados; sem uso cruzado entre contas.
3. **Não-treinamento:** cláusula contratual com o fornecedor de LLM proibindo uso dos dados para
   treino; comunicado formalmente ao cliente.
4. **Criptografia** em trânsito e em repouso; retenção configurável com exclusão sob demanda.
5. **Trilha de auditoria:** registro de quem acessou qual insight e quando.
6. **Defesa contra injeção de *prompt*:** o conteúdo de tickets é tratado como **dado, nunca como
   instrução** — um cliente mal-intencionado poderia escrever comandos dentro de um ticket.

**Confiabilidade**

1. **Calibração da confiança:** exibir o nível de certeza e admitir o "não sei" é preferível a uma
   resposta segura e errada.
2. **Avaliação contínua:** conjunto de testes rotulado, executado a cada alteração de *prompt* ou
   de modelo, com portão de qualidade no *pipeline* de entrega.
3. **Degradação graciosa:** se o LLM estiver indisponível, o produto ainda entrega volume,
   tendência e agrupamento estatístico, sem os resumos.

### 6.3 Impactos organizacionais

**No cliente**

| Dimensão | Antes | Depois | Implicação de gestão |
|---|---|---|---|
| Papel do analista de CX | Taguear e montar planilhas | Interpretar, questionar e conduzir ação | Requalificação; nova descrição de cargo; comunicação clara de não-demissão |
| Cadência de decisão | Relatório mensal | Ritual semanal de voz do cliente | Novo rito precisa de dono e agenda fixa, ou o produto vira relatório não lido |
| Relação CX ↔ Produto | Reclamação pontual | Backlog compartilhado com evidência | Definir alçada: quem decide o que entra no roadmap |
| Cultura de decisão | Opinião e senioridade | Evidência agregada | Resistência esperada de quem detinha o poder da interpretação |
| Governança de dados | Difusa | Formalizada (DPO, retenção, acesso) | Exige patrocínio de jurídico e segurança |

**No time do produto**

- Novos papéis: engenharia de IA/dados e responsabilidade explícita por avaliação de qualidade.
- Nova disciplina: **AI evals** entram no fluxo como testes de primeira classe.
- Nova estrutura de custo: parte do custo migra de fixo (infra) para variável (inferência),
  afetando precificação — cobrança por licença pura é arriscada; adota-se modelo híbrido com faixa
  de volume.

**Riscos de mudança organizacional e resposta**

O maior risco de adoção não é técnico, é humano (R05 e R09). A resposta de gestão adotada é:
envolver os analistas como **cocriadores** desde a descoberta; declarar formalmente o não-uso para
avaliação individual; e medir o sucesso pela **ação executada**, não pelo acesso à ferramenta —
garantindo que o produto seja avaliado por mudar o comportamento da organização, e não por
existir.

---

## 7. Referências

- **PMI — Project Management Institute.** *A Guide to the Project Management Body of Knowledge
  (PMBOK® Guide)* — conceitos de gerenciamento de riscos, ciclo de vida e governança de projetos.
  https://www.pmi.org
- **Schwaber, K.; Sutherland, J.** *The Scrum Guide* (2020) — entrega incremental, valor e ciclos
  curtos. https://scrumguides.org
- **Conteúdo da disciplina** *Fundamentos de Gestão de Projetos*: visão de produto, MVP, roadmap,
  ciclo de vida, riscos e gestão de produtos com IA.
- **Maurya, A.** *Running Lean* — Lean Canvas e validação de hipóteses de negócio.
- **Ries, E.** *The Lean Startup* — ciclo construir–medir–aprender e definição de MVP.
