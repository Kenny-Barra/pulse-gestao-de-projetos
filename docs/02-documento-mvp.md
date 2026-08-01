# Documento de MVP · Pulse

**Artefato obrigatório da Parte Prática**
**Produto:** Pulse, plataforma de inteligência de atendimento com IA generativa
**Versão:** 1.0 · **Autor:** Kenedy Pereira · **Data:** Julho de 2026
**Status:** Aprovado para desenvolvimento (saída do *gate* G1)

---

## 1. Objetivo do MVP

Validar, em 8 semanas e com 3 clientes-piloto, a seguinte hipótese:

> **"Um líder de CX confia no ranking automático de temas gerado por IA a ponto de tomar uma
> decisão de priorização sem reler os tickets originais."**

Este é um MVP de **risco técnico e de valor**. Não busca escala, robustez corporativa nem
completude funcional. Busca uma resposta binária à hipótese acima.

---

## 2. Escopo negativo (o que o MVP **não** faz)

Declarar o que fica de fora é tão importante quanto declarar o que entra: é a trava formal contra
o *scope creep* (risco R13).

- ❌ Não responde nem redige respostas de tickets
- ❌ Não avalia desempenho individual de atendentes *(restrição ética permanente, não temporária)*
- ❌ Não escreve de volta no *helpdesk* (integração é somente leitura)
- ❌ Não processa áudio ou ligações telefônicas
- ❌ Não suporta idiomas além de português e inglês
- ❌ Não possui SSO/SAML, app mobile ou API pública
- ❌ Não faz previsão de churn nem análise de causa-raiz automática

---

## 3. Lista de funcionalidades, prioridade e critérios de aceitação

**Legenda de prioridade (MoSCoW):**
`Must` = sem isso não há MVP · `Should` = importante, entra se houver folga · `Could` = desejável,
adiado · `Won't` = explicitamente fora desta versão

---

### 🔴 F1 · Ingestão de dados

| | |
|---|---|
| **Prioridade** | Must · RICE 63,3 |
| **Épico** | Fundação de dados |
| **Estimativa** | 3 semanas |

**História de usuário**
> Como **analista de CX**, quero conectar minha fonte de tickets ao Pulse para que a análise use
> meus dados reais sem trabalho manual de exportação.

**Critérios de aceitação**
- [ ] **CA1.1:** Dado um arquivo CSV com as colunas `id`, `data`, `canal`, `texto`, quando eu faço o upload, então o sistema valida o esquema e informa erros por linha antes de processar.
- [ ] **CA1.2:** O sistema processa um arquivo de até **50.000 registros** sem falhar, com barra de progresso visível.
- [ ] **CA1.3:** Dado que informei minhas credenciais do Zendesk, quando a conexão é estabelecida, então o sistema importa os tickets dos últimos 90 dias em modo **somente leitura**.
- [ ] **CA1.4:** Registros duplicados (mesmo `id`) são detectados e ignorados, com contagem exibida no relatório de importação.
- [ ] **CA1.5:** Se a importação falhar na metade, o sistema mantém o que já foi processado e permite retomar sem duplicar.

---

### 🔴 F2 · Normalização e anonimização de PII

| | |
|---|---|
| **Prioridade** | Must · RICE 95,0 |
| **Épico** | Fundação de dados |
| **Estimativa** | 2 semanas |
| **Origem** | Requisito legal (LGPD), mitigação do risco **R03** |

**História de usuário**
> Como **DPO do cliente**, quero garantir que nenhum dado pessoal identificável saia do ambiente
> para o provedor de IA, para que o uso do produto esteja em conformidade com a LGPD.

**Critérios de aceitação**
- [ ] **CA2.1:** CPF, CNPJ, e-mail, telefone, número de cartão e CEP são mascarados **antes** de qualquer chamada ao LLM.
- [ ] **CA2.2:** A taxa de detecção de PII em um conjunto de teste rotulado é **≥ 98%** de recall.
- [ ] **CA2.3:** O texto original permanece armazenado de forma criptografada e é exibido apenas ao usuário autenticado do próprio cliente.
- [ ] **CA2.4:** Existe log de auditoria registrando cada envio ao LLM, com a versão do sanitizador aplicada.
- [ ] **CA2.5:** Nenhuma chamada ao LLM ocorre se o sanitizador falhar. O comportamento padrão é **bloquear**, nunca prosseguir.

---

### 🔴 F3 · Clusterização automática de temas

| | |
|---|---|
| **Prioridade** | Must · RICE 35,0 |
| **Épico** | Motor de inteligência |
| **Estimativa** | 6 semanas |
| **Risco associado** | **R01**: é a funcionalidade que carrega o maior risco técnico do projeto |

**História de usuário**
> Como **analista de CX**, quero que o sistema agrupe automaticamente as interações em temas
> nomeados, para que eu não precise taguear manualmente.

**Critérios de aceitação**
- [ ] **CA3.1:** Dado um conjunto de 10.000 tickets, o sistema gera entre **8 e 30 temas** distintos, sem exigir taxonomia prévia.
- [ ] **CA3.2:** A precisão da classificação, avaliada por especialista humano em amostra de 200 tickets, é **≥ 80%**.
- [ ] **CA3.3:** Cada tema recebe um rótulo em linguagem natural com no máximo 8 palavras, compreensível sem contexto técnico.
- [ ] **CA3.4:** Tickets que não se encaixam em nenhum tema vão para "Não classificados", que não pode exceder **15%** do total.
- [ ] **CA3.5:** O reprocessamento do mesmo conjunto produz temas equivalentes (estabilidade ≥ 85% de sobreposição).
- [ ] **CA3.6:** O processamento de 10.000 tickets conclui em **menos de 20 minutos**.

---

### 🔴 F4 · Painel de temas priorizados

| | |
|---|---|
| **Prioridade** | Must · RICE 90,0 |
| **Épico** | Entrega de valor |
| **Estimativa** | 3 semanas |

**História de usuário**
> Como **head de CX**, quero ver os temas ordenados por criticidade, para saber onde focar sem
> analisar tudo.

**Critérios de aceitação**
- [ ] **CA4.1:** Os temas são exibidos em ranking calculado por **volume × tendência × sentimento**, com a fórmula visível ao usuário.
- [ ] **CA4.2:** Cada tema apresenta: nome, volume absoluto, % do total, variação vs. período anterior e sentimento médio.
- [ ] **CA4.3:** É possível filtrar por período, canal e faixa de sentimento; os filtros persistem ao navegar.
- [ ] **CA4.4:** A tendência é sinalizada visualmente (▲ crescendo / ▼ caindo / ▬ estável) com o percentual.
- [ ] **CA4.5:** O painel carrega em **menos de 3 segundos** para bases de até 100.000 tickets.
- [ ] **CA4.6:** Clicar em um tema abre o detalhe com as evidências (F5).

---

### 🔴 F5 · Evidência rastreável

| | |
|---|---|
| **Prioridade** | Must · RICE 112,5 · **maior prioridade relativa do MVP** |
| **Épico** | Confiança |
| **Estimativa** | 2 semanas |
| **Risco associado** | **R02**: é a principal mitigação de produto contra alucinação |

**História de usuário**
> Como **head de CX**, quero ver os trechos reais que sustentam cada tema, para confiar no insight
> antes de levá-lo à diretoria.

**Critérios de aceitação**
- [ ] **CA5.1:** Todo tema exibe de **3 a 5 citações literais** extraídas dos tickets originais.
- [ ] **CA5.2:** Cada citação possui link direto para o ticket completo na fonte (quando integrado) ou para o registro importado.
- [ ] **CA5.3:** As citações são **verbatim**: o sistema não parafraseia nem edita o texto original.
- [ ] **CA5.4:** Se o modelo não encontrar evidência suficiente, o tema é marcado como **"baixa confiança"** e não entra no resumo executivo.
- [ ] **CA5.5:** Em auditoria manual de 50 temas, **100%** das citações pertencem de fato ao tema declarado.

---

### 🔴 F6 · Resumo executivo semanal

| | |
|---|---|
| **Prioridade** | Must · RICE 64,0 |
| **Épico** | Entrega de valor |
| **Estimativa** | 3 semanas |

**História de usuário**
> Como **head de CX**, quero receber toda segunda-feira um resumo com os temas críticos e o que
> fazer sobre eles, para começar a semana com prioridades definidas.

**Critérios de aceitação**
- [ ] **CA6.1:** O resumo é enviado por e-mail toda segunda às 8h (horário configurável).
- [ ] **CA6.2:** Contém no máximo **5 temas**, cada um com: título, volume, tendência, 1 citação e 1 ação sugerida.
- [ ] **CA6.3:** Cada ação sugerida é específica e executável (ex.: *"Revisar o texto do passo 3 do cadastro, porque 340 tickets citam confusão nesse ponto"*), nunca genérica.
- [ ] **CA6.4:** Todo conteúdo gerado por IA é **rotulado como tal** no corpo do e-mail.
- [ ] **CA6.5:** O e-mail é legível em cliente mobile e possui link para o painel completo.
- [ ] **CA6.6:** Temas marcados como "baixa confiança" (CA5.4) são excluídos do resumo.

---

### 🔴 F7 · Feedback do usuário sobre o tema

| | |
|---|---|
| **Prioridade** | Must · RICE 89,3 |
| **Épico** | Calibração |
| **Estimativa** | 1 semana |

**História de usuário**
> Como **analista de CX**, quero corrigir temas mal classificados, para que o sistema melhore e eu
> sinta que tenho controle sobre ele.

**Critérios de aceitação**
- [ ] **CA7.1:** Cada tema oferece as ações **"tema correto"**, **"tema incorreto"** e **"mesclar com..."**.
- [ ] **CA7.2:** O feedback é registrado com usuário, data e tema, e alimenta o conjunto de calibração.
- [ ] **CA7.3:** Temas mesclados permanecem unificados nos processamentos seguintes.
- [ ] **CA7.4:** Existe painel interno mostrando a taxa de aprovação dos temas por cliente, que é a métrica de acompanhamento do risco **R01**.

---

### 🟡 F8 · Exportação e compartilhamento

| | |
|---|---|
| **Prioridade** | Should · RICE 54,0 |
| **Épico** | Entrega de valor |
| **Estimativa** | 1 semana |

**História de usuário**
> Como **head de CX**, quero exportar o relatório, para levá-lo à reunião de diretoria.

**Critérios de aceitação**
- [ ] **CA8.1:** Exportação do painel em PDF preservando ranking, gráficos e citações.
- [ ] **CA8.2:** Exportação dos temas em CSV com todas as métricas.
- [ ] **CA8.3:** Envio do resumo para um canal do Slack via *webhook* configurável.

---

### 🔵 Adiados: fora do MVP

| ID | Funcionalidade | Prioridade | Destino | Motivo do adiamento |
|---|---|---|---|---|
| F9 | Alertas de anomalia em tempo real | Could · RICE 15,0 | Fase 2 | Depende de *baseline* histórico que só existe após meses de uso |
| F10 | Chat conversacional com os dados | Won't · RICE 3,0 | Fase 3 | Alto custo, valor não comprovado; resolve consulta, não priorização |
| F11 | Previsão de churn por tema | Won't | Fase 3 | Exige dado de cancelamento e histórico longo |
| F12 | Análise de causa-raiz automática | Won't | Fase 3 | Exige cruzamento com dados de produto ainda indisponíveis |
| F13 | SSO/SAML e trilha de auditoria corporativa | Won't | Fase 3 | Exigência de contas *enterprise*, ausentes no piloto |

---

## 4. Resumo de priorização

| Prioridade | Qtd. | Funcionalidades | Esforço total |
|---|---|---|---|
| 🔴 **Must** | 7 | F1, F2, F3, F4, F5, F6, F7 | **20 semanas/dev** |
| 🟡 **Should** | 1 | F8 | 1 semana/dev |
| 🔵 **Could / Won't** | 5 | F9 a F13 | adiado |

**Capacidade da Fase 1:** 3 desenvolvedores × 8 semanas = 24 semanas/dev.
**Alocação:** 20 semanas em Must + 1 em Should + **3 semanas (12,5%) de reserva de contingência**
para os riscos R01 e R06.

### Matriz Valor × Esforço

```
   ALTO   │  F5 ●    F4 ●              │  F3 ●
  VALOR   │  F7 ●    F6 ●              │
          │  F2 ●                      │  F1 ●
          ├────────────────────────────┼───────────────────
          │  F8 ●                      │  F10 ●   F11 ●
   BAIXO  │                            │  F9  ●
  VALOR   │                            │
          └────────────────────────────┴───────────────────
              BAIXO ESFORÇO                ALTO ESFORÇO
              ── FAZER PRIMEIRO ──          ── AVALIAR ──
```

**Leitura:** F5, F4, F7 e F2 são alto valor e baixo esforço, então entram primeiro. F3 é alto valor
e alto esforço, mas é **o núcleo do produto**, então começa em paralelo já na semana 1 por carregar
o maior risco. F9, F10 e F11 têm baixo valor relativo e alto esforço, e foram adiados sem
hesitação.

---

## 5. Definição de Pronto (*Definition of Done*)

Uma funcionalidade só é considerada concluída quando:

1. Todos os critérios de aceitação estão verificados e assinados pelo PM;
2. Existe teste automatizado cobrindo o caminho principal e ao menos um caminho de erro;
3. **Se a funcionalidade envolve IA:** possui métrica de qualidade medida contra conjunto de teste
   rotulado, com resultado registrado (não basta "funcionar");
4. O custo de inferência por operação foi medido e está dentro do teto definido;
5. A funcionalidade foi validada com ao menos 1 usuário de cliente-piloto;
6. Documentação de uso atualizada.

---

## 6. Critérios de sucesso do MVP (*gate* G2)

| Critério | Meta | Como será medido |
|---|---|---|
| Precisão da classificação | ≥ 80% | Amostra de 200 tickets avaliada por especialista |
| Utilidade dos temas principais | ≥ 4 de 5 úteis | Avaliação declarada pelo líder de CX |
| Tempo até o primeiro insight (TTFI) | < 30 min | Telemetria: do cadastro ao primeiro tema visualizado |
| Planos de ação executados | ≥ 3 por piloto/mês | Registro compartilhado com o cliente |
| Retenção semanal do usuário primário (W4) | ≥ 60% | Telemetria de acesso |
| Custo de inferência | ≤ R$ 25 / 1.000 tickets | Painel interno de custo |
| Intenção de compra | ≥ 2 de 3 pilotos | Entrevista de encerramento do piloto |

**Regra de decisão em G2:**
- **Todos os critérios atingidos** → avançar para a Fase de Entrega.
- **Precisão entre 60% e 80%** → iterar dentro da Fase de Validação (até 4 semanas adicionais).
- **Precisão < 60%** → pivotar a abordagem técnica (taxonomia assistida ou *fine-tuning*).
- **Precisão alta, mas ação executada = 0** → o problema é de valor, não técnico: retornar à
  Descoberta.
