---
name: clipping-ma-diario
description: Atualiza o clipping diário de M&A (newsletter + clipping) em português, com destaque IGC Partners
---

OBJETIVO
Atualizar o clipping diário de M&A (Fusões e Aquisições) da Isa, sócia/colaboradora da IGC Partners (boutique líder em sell-side no middle market brasileiro, fundada em 1997 por Dimitri Abudi e Daniel Milanez). O arquivo fica em /sessions/funny-brave-goodall/mnt/outputs/clipping-ma.html e tem DUAS partes que precisam ser atualizadas a cada run:
1) Uma **aba Newsletter** (página inicial) com 4 seções: Resumo, Mercado Brasileiro, Mercado Internacional, "O que a IGC deveria estar de olho"
2) Uma **aba Clipping completo** com 20-30 cards de notícias categorizadas

CONTEXTO
- Idioma: TUDO em português (traduzir notícias internacionais se necessário)
- Fontes tier 1 Brasil: Valor Econômico, Pipeline Valor, Brazil Journal, NeoFeed, Bloomberg Línea, Exame, Estadão, Folha, Capital Aberto, InfoMoney
- Fontes tier 1 Mundo: Bloomberg, Reuters, Financial Times, Wall Street Journal, The Economist, Barrons, CNBC
- Setores: Todos, com ênfase em middle market brasileiro, Tech/SaaS, Saúde, Varejo, Agro, Educação, Financeiro, Indústria, Energia
- Destaque IGC Partners: deals assessorados, clientes, sócios mencionados, concorrentes diretos (BR Partners, Seneca Evercore, RGS Partners, Vinci Partners, Manchester), setores-foco da IGC

PASSO A PASSO
1. Usar WebSearch com queries variadas para coletar notícias RECENTES (últimas 24h, ou 12h na execução das 18h):
   - "M&A fusões aquisições Brasil [mês ano]"
   - "aquisição [setor] Brasil 2026"
   - "Pipeline Valor M&A hoje"
   - "Brazil Journal aquisição [mês]"
   - "NeoFeed M&A deal"
   - "IGC Partners"
   - "global M&A deals [mês ano] Bloomberg Reuters"
   - "private equity buyout [mês ano]"
   - "McCormick Unilever Ares Hexagon" (rastrear follow-ups dos grandes deals)
2. Ler o arquivo atual: /sessions/funny-brave-goodall/mnt/outputs/clipping-ma.html
3. Fazer Edit nas seguintes partes do arquivo:

   a) Constante LAST_UPDATE → formato "DD/MM/AAAA HH:MM" (hora de Brasília)
   b) Constante HERO_DATE → formato "DIA-DA-SEMANA, DD DE MÊS DE AAAA" em maiúsculas (ex: "SEGUNDA, 20 DE ABRIL DE 2026")
   c) Array NEWS → 22-28 itens novos, estrutura preservada:
      { igc?: boolean, origin: "BR"|"GLOBAL", sectors: string[], source: string, title: string, summary: string, date: string, url: string }
      - 3-5 itens com igc: true
      - 10-15 itens BR (sem igc)
      - 8-12 itens GLOBAL (sem igc)
      - Setores permitidos: tech, saude, varejo, agro, financeiro, industria, logistica, educacao, energia
   d) Conteúdo da aba Newsletter (DOM estático no HTML) — atualizar com notícias do dia:
      - Hero: título-gancho + parágrafo com 3-4 fatos chave do dia
      - Seção 1 "Resumo do dia": 4 highlight-boxes (valores/indicadores) + 2-3 parágrafos de contexto
      - Seção 2 "Mercado brasileiro": 2 parágrafos narrativos + deal-list com 5-7 deals BR do dia
      - Seção 3 "Mercado internacional": 2 parágrafos narrativos + deal-list com 4-6 deals globais do dia
      - Seção 4 "O que a IGC deveria estar de olho": parágrafo de abertura + 5-6 watch-items (h4 + p curto) sobre leituras estratégicas/oportunidades/ameaças

4. NÃO MODIFICAR o CSS nem a estrutura da aba Clipping (igc-section, market-overview, news-grid)
5. Salvar e verificar que o HTML ainda é válido (tags fechadas, JavaScript sintaxe ok)

TOM DO CONTEÚDO EDITORIAL
- Analítico, como uma newsletter de markets research séria (Brazil Journal / Pipeline / Semafor Principals)
- Conexões entre notícias, não listas frias
- "O que a IGC deveria estar de olho" deve ser INSIGHT — não repetir notícias. Puxar implicações para sell-side, middle market, concorrência, setores onde IGC tem vantagem
- Usar <strong> para highlights e <em> para nuances

SAÍDA PARA O USUÁRIO
Mensagem curta com: data/hora, número de notícias (total + IGC), 2-3 highlights do dia, 1 ponto de atenção estratégico para a IGC.

CRITÉRIOS DE SUCESSO
- ≥ 20 notícias totais no array NEWS
- ≥ 3 notícias IGC
- Newsletter e Clipping ambos atualizados com conteúdo do dia
- Português em 100% do conteúdo
- URLs válidas apontando para a fonte original
- HTML válido