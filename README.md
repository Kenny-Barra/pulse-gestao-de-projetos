# Pulse — Planejamento de um Produto Digital com IA

**Do Problema ao Produto: Planejamento de um Produto Digital com IA, MVP e Roadmap**

Trabalho da disciplina **Fundamentos de Gestão de Projetos**
**Autor:** Kenedy Pereira · **Data:** Julho de 2026

---

## O que é este repositório

Este repositório contém o **planejamento estratégico completo** de um produto digital apoiado em
IA generativa — não a sua implementação em código. O trabalho simula a rotina real de um Product
Manager / Project Manager em um *startup studio*: transformar um problema mal definido de cliente
em visão de produto, escopo de MVP, roadmap por fases, ciclo de vida com portões de decisão e
matriz de riscos com donos nomeados.

### O problema do cliente

Um time interno de atendimento recebe volumes gigantescos de interações — tickets, chats e
e-mails — e não consegue priorizar temas críticos nem gerar planos de ação rápidos. A informação
sobre o que está quebrado no produto **já existe** dentro dessas conversas; ela só não é legível
em escala humana.

### A solução planejada

**Pulse** — plataforma SaaS que processa 100% das interações de atendimento e devolve temas
priorizados, resumo executivo semanal e plano de ação com evidência rastreável até o ticket de
origem.

> **Proposta de valor:** de 100% das conversas com seus clientes para 5 decisões priorizadas —
> toda segunda-feira, às 8h, com a evidência anexada.

---

## 🔗 Links dos entregáveis

| Entregável | Link |
|---|---|
| 📊 **Board visual dos artefatos** (canvas, roadmap e matriz de riscos) | [Abrir board interativo](https://claude.ai/code/artifact/d97c4252-b307-4b16-913d-e1fc83636114) |
| 🎥 **Vídeo pitch** (até 4 min) | _[colar link do YouTube após a gravação]_ |

O board é uma página web responsiva com tema claro e escuro. As mesmas informações estão nos
documentos deste repositório e nos prints da pasta [`prints/`](prints/), caso o link não abra.

---

## Estrutura do repositório

```
.
├── README.md                          ← você está aqui
├── docs/
│   ├── 01-parte-teorica.md            Parte teórica completa (entregável 1)
│   ├── 02-documento-mvp.md            Documento de MVP com critérios de aceitação
│   └── 03-matriz-de-riscos.md         Matriz de riscos detalhada com gatilhos
├── artefatos/
│   └── board.html                     Board visual (fonte da versão publicada)
├── prints/
│   ├── 00-board-completo.png          Print do board inteiro
│   ├── 01-canvas-de-visao.png         Print do Lean Canvas
│   ├── 02-roadmap.png                 Print do roadmap
│   ├── 03-matriz-de-riscos.png        Print da matriz de riscos
│   ├── 04-norte-estrategico.png       Print do norte estratégico
│   └── tema-claro/                    Mesmos prints em tema claro (para impressão)
└── enunciado/
    └── TRABALHO - Fundamentos de Gestão de projetos.docx.pdf
```

---

## Mapa dos requisitos → onde está cada coisa

### Entregável 1 — Parte Teórica (1,5 pts)

| Requisito do enunciado | Onde está |
|---|---|
| 1.1 Visão de Produto | [`docs/01-parte-teorica.md` § 1](docs/01-parte-teorica.md#1-visão-de-produto) |
| 1.2 Definição do MVP | [`docs/01-parte-teorica.md` § 2](docs/01-parte-teorica.md#2-definição-do-mvp) |
| 1.3 Roadmap (mín. 3 fases) | [§ 3](docs/01-parte-teorica.md#3-roadmap-do-produto) — **4 fases entregues** |
| 1.4 Ciclo de Vida | [§ 4](docs/01-parte-teorica.md#4-ciclo-de-vida-da-aplicação) — 4 fases + 4 *gates* |
| 1.5 Gerenciamento de Riscos (mín. 5) | [§ 5](docs/01-parte-teorica.md#5-gerenciamento-de-riscos) — **15 riscos mapeados** |
| 1.6 Gestão de Produtos e IA | [§ 6](docs/01-parte-teorica.md#6-gestão-de-produtos-e-ia) |

### Entregável 2 — Parte Prática (3,5 pts)

| Artefato obrigatório | Onde está |
|---|---|
| Canvas de Visão de Produto (Lean Canvas) | [Board § 01](https://claude.ai/code/artifact/d97c4252-b307-4b16-913d-e1fc83636114) · [print](prints/01-canvas-de-visao.png) |
| Documento de MVP (funcionalidades, prioridade, critérios de aceitação) | [`docs/02-documento-mvp.md`](docs/02-documento-mvp.md) |
| Roadmap visual | [Board § 02](https://claude.ai/code/artifact/d97c4252-b307-4b16-913d-e1fc83636114) · [print](prints/02-roadmap.png) |
| Matriz de Riscos (risco, prob., impacto, mitigação, responsável) | [Board § 03](https://claude.ai/code/artifact/d97c4252-b307-4b16-913d-e1fc83636114) · [`docs/03-matriz-de-riscos.md`](docs/03-matriz-de-riscos.md) · [print](prints/03-matriz-de-riscos.png) |
| Prints dos artefatos | [`prints/`](prints/) |
| Links públicos das ferramentas | seção [Links dos entregáveis](#-links-dos-entregáveis) |
| README explicando a lógica | este arquivo |

### Entregável 3 — Vídeo Pitch (2,0 pts)

Vídeo de até 4 minutos defendendo o projeto, cobrindo os seis pontos exigidos: contexto do
problema, visão do produto, MVP proposto, roadmap, principais riscos e mitigação, e justificativa
estratégica das decisões tomadas.

**Link:** _[colar link do YouTube após a gravação]_

---

## A lógica do planejamento

Esta seção explica **por que** os artefatos têm a forma que têm — é a linha de raciocínio que
conecta os três entregáveis.

### 1. Tudo parte de uma métrica, não de uma funcionalidade

A primeira decisão foi escolher a métrica North Star: **número de planos de ação executados por
mês**. Não usuários ativos, não temas gerados, não tickets processados.

A escolha é deliberada e restritiva. Um produto de análise pode ter engajamento alto e valor zero
— basta que as pessoas olhem os gráficos e não mudem nada. Ao medir **ação executada**, o produto
só pontua quando altera o comportamento da organização.

Essa escolha define tudo o que vem depois: o MVP prioriza o que gera ação, o roadmap sequencia
por remoção de risco à ação, e a matriz de riscos trata "insight que não vira ação" (R05) como
risco **crítico**, e não como problema de adoção a resolver depois.

### 2. O MVP responde a uma pergunta, não entrega um pacote

O MVP foi desenhado ao redor de uma única hipótese falsificável:

> *Um líder de CX confia no ranking automático de temas a ponto de decidir sem reler os tickets?*

Isso permitiu cortar escopo sem culpa. O que ficou de fora está **documentado explicitamente**
como escopo negativo — inclusive o chat conversacional com os dados, que é a funcionalidade que
mais impressiona em demonstração e a que menos resolve o problema declarado do cliente.

A priorização usou **MoSCoW** para o corte de escopo e **RICE** para ordenar dentro do essencial.
O resultado tem uma inversão que vale notar: a funcionalidade de maior pontuação **não é a
inteligência artificial** — é a *evidência rastreável* (RICE 112,5), porque é barata de construir
e protege todo o resto do produto contra o risco de alucinação.

### 3. Cada fase do roadmap existe para matar um risco

O roadmap não é uma lista de funcionalidades distribuídas no tempo. Cada fase carrega **uma
pergunta** e **um tipo de risco**:

| Fase | Pergunta | Risco atacado |
|---|---|---|
| 1 · Descoberta e MVP | Funciona? | Técnico |
| 2 · Validação e Ação | As empresas pagam? | Mercado e adoção |
| 3 · Escala e Predição | Escala com margem? | Econômico |
| 4 · Plataforma | Vira plataforma? | Estratégico |

Consequência prática: as datas são estimativas negociáveis, mas os **critérios de passagem entre
fases não são**. Uma fase não avança por prazo cumprido — avança por evidência produzida.

### 4. Os riscos de IA são de natureza diferente

Software tradicional é determinístico: a mesma entrada gera a mesma saída, e o teste é binário.
Produto com IA generativa não é. Isso muda a gestão em três pontos concretos:

- **A qualidade cai sem ninguém mexer no código** (*drift*) → exige monitoramento contínuo, não
  apenas testes de regressão.
- **O custo cresce com o uso, não com o número de licenças** → o custo de inferência virou
  *métrica de produto* medida desde a semana 1, e a precificação é por faixa de volume.
- **A saída pode estar convincentemente errada** (alucinação) → a mitigação é de produto, não de
  engenharia: evidência obrigatória, e o tema sem suporte factual simplesmente não entra no
  resumo executivo.

Por isso a *Definition of Done* de qualquer funcionalidade de IA neste planejamento inclui
**métrica de qualidade medida** — não basta "está em produção".

### 5. Uma restrição ética assumida como decisão de produto

O Pulse analisa **temas, não pessoas**. Não produz ranking de desempenho individual de
atendentes, embora fosse tecnicamente trivial.

É uma restrição permanente, não uma limitação temporária de escopo. Viabilizar uso punitivo
destruiria a confiança do time que usa a ferramenta todos os dias (risco R09) e traria exposição
trabalhista ao cliente. Aparece no canvas como **vantagem competitiva**, porque é exatamente isso:
uma escolha que compra confiança e que o concorrente teria dificuldade de copiar sem abrir mão de
uma funcionalidade vendável.

---

## Como interpretar os artefatos

### Canvas de Visão (Lean Canvas)

Nove blocos numerados na ordem canônica de preenchimento (Problema → Segmentos → Proposta de Valor
→ Solução → Canais → Receita → Custos → Métricas → Vantagem). **Leia o bloco central primeiro**:
a proposta de valor única é a origem de todas as decisões dos outros dois artefatos. Os blocos de
Custos e Receita estão na base porque o modelo econômico é, neste produto, uma restrição de
projeto — não um detalhe comercial.

### Roadmap

Leia cada coluna de cima para baixo: **pergunta da fase → hipótese sob teste → entregáveis →
métricas-alvo → risco atacado**. Abaixo das quatro fases estão os *gates* (G1 a G4) com os
critérios objetivos de passagem. A régua de avaliação do roadmap não são as datas — são os gates.

### Matriz de Riscos

- **Exposição = Probabilidade × Impacto**, ambas em escala de 1 a 5.
- 🔴 Crítico (15–25) · 🟠 Médio (8–12) · 🟢 Baixo (1–6).
- O **mapa de calor** mostra a distribuição; a **tabela** traz mitigação e responsável.
- A concentração no canto superior direito é *diagnóstica, não um defeito de planejamento*: os
  riscos de maior exposição (R01, R02, R04) são inerentes ao uso de IA generativa. É por isso que
  as funcionalidades que os mitigam foram alocadas para a **semana 1**, e não distribuídas ao
  longo do cronograma.
- Cada risco crítico tem um **gatilho numérico** com contingência automática — não depende de
  alguém perceber que está dando errado.

---

## Números do planejamento

| | |
|---|---|
| Fases de roadmap | 4 *(mínimo exigido: 3)* |
| Riscos mapeados | 15 *(mínimo exigido: 5)* |
| Funcionalidades priorizadas | 13 · sendo 7 `Must`, 1 `Should`, 5 adiadas |
| Critérios de aceitação escritos | 40 |
| Portões de decisão (*gates*) | 4 |
| Duração do MVP | 8 semanas · 3 clientes-piloto |

---

## Fontes de pesquisa

- **PMI — Project Management Institute.** *PMBOK® Guide* — gerenciamento de riscos, ciclo de vida
  e governança. https://www.pmi.org
- **Schwaber, K.; Sutherland, J.** *The Scrum Guide* (2020) — entrega incremental e ciclos curtos.
  https://scrumguides.org
- **Conteúdo da disciplina** *Fundamentos de Gestão de Projetos* — visão de produto, MVP, roadmap,
  ciclo de vida, riscos e gestão de produtos com IA.
- **Maurya, A.** *Running Lean* — Lean Canvas e validação de hipóteses.
- **Ries, E.** *The Lean Startup* — ciclo construir–medir–aprender.

---

## Visualizar o board localmente

O arquivo [`artefatos/board.html`](artefatos/board.html) é autocontido — sem dependências
externas. Basta abri-lo em qualquer navegador. Ele acompanha o tema do sistema (claro ou escuro)
e possui folha de estilo de impressão para gerar PDF via `Ctrl + P`.
