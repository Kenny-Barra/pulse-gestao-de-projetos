# Matriz de Riscos · Pulse

**Artefato obrigatório da Parte Prática**
**Produto:** Pulse, plataforma de inteligência de atendimento com IA generativa
**Versão:** 1.0 · **Autor:** Kenedy Pereira · **Data:** Julho de 2026
**Metodologia:** Análise qualitativa de riscos (PMI / PMBOK® Guide)
**Cadência de revisão:** quinzenal para riscos críticos · completa a cada *gate*

---

## 1. Escalas de avaliação

### Probabilidade

| Nível | Classificação | Faixa | Interpretação prática |
|:---:|---|---|---|
| 1 | Muito baixa | < 10% | Improvável no horizonte do projeto |
| 2 | Baixa | 10 a 30% | Já aconteceu em projetos similares, mas é exceção |
| 3 | Média | 30 a 60% | Razoavelmente esperado |
| 4 | Alta | 60 a 85% | Provável. Planejar assumindo que vai ocorrer |
| 5 | Muito alta | > 85% | Praticamente certo |

### Impacto

| Nível | Classificação | Efeito no projeto |
|:---:|---|---|
| 1 | Muito baixo | Efeito desprezível; absorvido pela rotina |
| 2 | Baixo | Atraso de até 1 semana ou retrabalho pontual |
| 3 | Médio | Atraso de 2 a 4 semanas ou perda de 1 cliente-piloto |
| 4 | Alto | Atraso superior a 1 mês ou falha em um *gate* |
| 5 | Muito alto | Inviabiliza o produto ou gera dano legal/reputacional grave |

### Exposição ao risco

**Exposição = Probabilidade × Impacto**

| Faixa | Nível | Tratamento exigido |
|:---:|---|---|
| 15 a 25 | 🔴 **Crítico** | Plano de mitigação ativo, dono nomeado e revisão quinzenal obrigatória |
| 8 a 12 | 🟠 **Médio** | Plano definido, monitorado a cada *gate* |
| 1 a 6 | 🟢 **Baixo** | Aceito e monitorado, sem ação preventiva dedicada |

### Estratégias de resposta

| Estratégia | Quando aplicar |
|---|---|
| **Mitigar** | Reduzir probabilidade e/ou impacto por ação direta |
| **Evitar** | Eliminar a causa, alterando escopo ou abordagem |
| **Transferir** | Passar a consequência a terceiro (contrato, seguro, fornecedor) |
| **Aceitar** | Assumir conscientemente, com registro e responsável nomeado |

---

## 2. Matriz de riscos completa

### 🔴 Riscos críticos (exposição ≥ 15)

| ID | Risco | Categoria | P | I | Exp. | Estratégia | Plano de mitigação | Responsável |
|:---:|---|---|:---:|:---:|:---:|---|---|---|
| **R01** | Baixa precisão na clusterização torna os temas inúteis para decisão | Técnico | 4 | 5 | **20** | Mitigar | Prova de conceito antes de qualquer código de produção; conjunto de teste rotulado por especialista; ciclo de feedback do usuário (F7) alimentando calibração; plano B com taxonomia assistida caso a precisão fique abaixo de 60% | Tech Lead de IA |
| **R02** | Alucinação do LLM gera insight falso e destrói a confiança do cliente | Técnico / IA | 4 | 5 | **20** | Mitigar | Evidência rastreável obrigatória (F5); *grounding* estrito no texto-fonte; recusa explícita quando não há suporte factual; avaliação automatizada por amostragem a cada *release*; rótulo "baixa confiança" excluindo o tema do resumo executivo | Tech Lead de IA |
| **R04** | Custo de inferência inviabiliza a margem do produto em escala | Financeiro | 4 | 4 | **16** | Mitigar | Custo unitário medido como métrica de produto desde a semana 1; teto de custo por cliente com alerta automático; cache semântico; cascata de modelos (modelo menor primeiro, maior só quando necessário); *batching* de requisições | PM + Tech Lead |
| **R03** | Vazamento ou uso indevido de dado pessoal de clientes finais (LGPD) | Conformidade | 3 | 5 | **15** | Mitigar + Transferir | Anonimização de PII antes de qualquer inferência (F2), com bloqueio em caso de falha do sanitizador; cláusula contratual de não-treinamento com o fornecedor de LLM; DPA assinado; criptografia em trânsito e repouso; revisão jurídica antes do primeiro piloto; seguro de responsabilidade cibernética | DPO + PM |
| **R05** | Baixa adoção: o insight é lido, mas não se converte em ação | Mercado / Produto | 3 | 5 | **15** | Mitigar | *Onboarding* assistido nas 4 primeiras semanas; ritual semanal de revisão conduzido junto ao cliente; integração de 1 clique com Jira/Slack para converter insight em tarefa; North Star medindo **ação executada**, não acesso à ferramenta | PM |

### 🟠 Riscos médios (exposição de 8 a 12)

| ID | Risco | Categoria | P | I | Exp. | Estratégia | Plano de mitigação | Responsável |
|:---:|---|---|:---:|:---:|:---:|---|---|---|
| **R06** | Qualidade ruim dos dados do cliente (ruído, duplicidade, multi-idioma) | Técnico / Dados | 4 | 3 | **12** | Mitigar | Diagnóstico de dados obrigatório como pré-requisito contratual; camada de limpeza e deduplicação na ingestão; relatório de qualidade de dados transparente ao cliente, deslocando a expectativa antes do resultado | Engenheiro de Dados |
| **R07** | Dependência de fornecedor único de LLM (*vendor lock-in*) | Técnico / Estratégico | 3 | 4 | **12** | Mitigar | Camada de abstração de provedor desde o primeiro dia; fornecedor alternativo homologado ainda na Fase 1; teste de portabilidade executado trimestralmente | Arquiteto |
| **R08** | Concorrente estabelecido lança funcionalidade equivalente | Mercado | 4 | 3 | **12** | Aceitar + Mitigar | Diferenciação por "insight → ação com evidência", não por capacidade bruta de IA; velocidade de entrega como vantagem; profundidade vertical em CX em vez de amplitude genérica | PM |
| **R09** | Resistência interna do time de CX por receio de substituição | Organizacional | 3 | 3 | **9** | Mitigar | Comunicação formal e escrita de que o produto não avalia desempenho individual; analistas envolvidos como cocriadores desde a descoberta; treinamento e reposicionamento do papel (de tagueador a estrategista) | PM + RH do cliente |
| **R10** | Atraso na integração com o *helpdesk* (API, limites de taxa, aprovações internas) | Cronograma | 3 | 3 | **9** | Mitigar | Ingestão por CSV disponível como caminho de contingência já no MVP; validação de acesso à API no *kickoff*, antes do início do desenvolvimento | Tech Lead |
| **R11** | Degradação silenciosa da qualidade do modelo (*drift*) | Técnico / IA | 3 | 3 | **9** | Mitigar | Monitoramento contínuo das métricas de qualidade em produção; reavaliação trimestral contra conjunto de teste fixo; alerta automático quando a precisão cai abaixo do limiar | Tech Lead de IA |
| **R12** | Perda de pessoa-chave do time (especialista em IA) | Recursos | 2 | 4 | **8** | Mitigar | Registro de decisões de arquitetura (ADRs); programação em par nos módulos críticos; regra de *bus factor* mínimo 2 em todo componente central | PM |
| **R13** | Inflação de escopo do MVP durante os pilotos (*scope creep*) | Cronograma | 4 | 2 | **8** | Evitar | Escopo negativo formalmente documentado e comunicado; todo pedido novo vai para o backlog da Fase 2 sem exceção; *gate* G2 como trava formal de encerramento | PM |
| **R14** | Viés algorítmico desprioriza temas de grupos minoritários de clientes | Ético / IA | 2 | 4 | **8** | Mitigar | Auditoria periódica da distribuição de temas por segmento; revisão humana obrigatória de temas de baixo volume e alto impacto; painel dedicado a temas emergentes, protegendo o sinal fraco do domínio do volume | PM + Tech Lead de IA |

### 🟢 Riscos baixos (exposição ≤ 6)

| ID | Risco | Categoria | P | I | Exp. | Estratégia | Plano de mitigação | Responsável |
|:---:|---|---|:---:|:---:|:---:|---|---|---|
| **R15** | Indisponibilidade temporária da API do fornecedor de LLM | Operacional | 2 | 3 | **6** | Mitigar | Processamento assíncrono com fila e reprocessamento automático; provedor secundário pré-configurado; degradação graciosa entregando volume e tendência sem os resumos gerados | Arquiteto |

---

## 3. Mapa de calor

|  | **I=1** | **I=2** | **I=3** | **I=4** | **I=5** |
|:---:|:---:|:---:|:---:|:---:|:---:|
| **P=5** | 🟢 | 🟢 | 🟠 | 🔴 | 🔴 |
| **P=4** | 🟢 | 🟠 **R13** | 🟠 **R06 · R08** | 🔴 **R04** | 🔴 **R01 · R02** |
| **P=3** | 🟢 | 🟢 | 🟠 **R09 · R10 · R11** | 🟠 **R07** | 🔴 **R03 · R05** |
| **P=2** | 🟢 | 🟢 | 🟢 **R15** | 🟠 **R12 · R14** | 🟠 |
| **P=1** | 🟢 | 🟢 | 🟢 | 🟢 | 🟠 |

**Distribuição:** 5 riscos críticos, 9 médios e 1 baixo, totalizando **15 riscos mapeados**.

**Leitura do mapa:** a concentração no quadrante superior direito era esperada. Os riscos de maior
exposição (R01, R02 e R04) são **técnicos e inerentes ao uso de IA generativa**, em vez de falhas
de planejamento. Isso explica a estrutura do MVP: as três funcionalidades que os mitigam (F3, F5 e
a medição de custo) começam na **semana 1**, sem ficarem espalhadas pelo cronograma.

---

## 4. Gatilhos e planos de contingência

Cada risco crítico possui um **gatilho mensurável**. Ao ser atingido, o plano de contingência é
acionado automaticamente, sem nova rodada de discussão.

| ID | Gatilho (métrica observável) | Contingência acionada | Prazo de resposta |
|:---:|---|---|---|
| **R01** | Precisão medida < 70% em qualquer *sprint* | Ativar plano B: taxonomia assistida com sementes definidas pelo cliente, em vez de clustering totalmente aberto | 1 *sprint* |
| **R02** | Qualquer insight sem evidência verificável chegando ao cliente | Suspender o resumo executivo automático; revisão humana obrigatória até correção da causa-raiz | Imediato |
| **R03** | Detecção de PII não mascarada em log de envio ao LLM | Interromper o processamento; acionar DPO; notificar o cliente em até 24h conforme LGPD | Imediato |
| **R04** | Custo unitário > R$ 40 / 1.000 tickets por 2 semanas seguidas | Congelar entrada de novos pilotos e priorizar otimização (cache, cascata de modelos) na *sprint* seguinte | 2 semanas |
| **R05** | Menos de 1 plano de ação executado por piloto no mês | Sessão de diagnóstico presencial com o cliente para identificar se a falha é de valor, de usabilidade ou de processo interno | 5 dias úteis |
| **R06** | Mais de 25% dos tickets classificados como "não classificados" | Revisar a camada de limpeza e reportar formalmente a qualidade dos dados ao cliente antes de prosseguir | 1 *sprint* |
| **R13** | Mais de 2 funcionalidades novas solicitadas e aceitas no ciclo | Congelamento formal de escopo até o *gate* G2, com registro da decisão | Imediato |

---

## 5. Reservas e governança

**Reserva de contingência de cronograma:** 3 semanas/dev (12,5% da capacidade da Fase 1),
alocadas nominalmente para **R01** e **R06**, os dois riscos com maior probabilidade de consumir
tempo não planejado.

**Rotina de governança:**

| Ritual | Frequência | Participantes | Saída |
|---|---|---|---|
| Revisão de riscos críticos | Quinzenal (na *sprint review*) | PM, Tech Lead, Arquiteto | Atualização de P/I e status dos gatilhos |
| Revisão completa da matriz | A cada *gate* (G1, G2, G3) | PM, Tech Lead, Patrocinador, DPO | Matriz reavaliada e decisão de avanço registrada |
| Auditoria de conformidade e viés | Trimestral | DPO, PM, Tech Lead de IA | Relatório de PII, viés e *drift* |

**Regra de aceitação de risco:** nenhum risco crítico pode ser aceito informalmente. A aceitação
exige registro escrito com justificativa, responsável nomeado e data de reavaliação. Sem isso,
o risco permanece com mitigação ativa.

**Regra de propriedade:** todo risco tem **um único responsável nomeado**. Quando o dono é o time
inteiro, na prática ninguém assume.
