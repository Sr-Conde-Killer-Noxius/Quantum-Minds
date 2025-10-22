# Estratégia Quantitativa Agro - Desafio Quant AI Itaú Asset 2025

[cite_start]Este repositório contém o plano de execução, os scripts de coleta de dados e a metodologia para o desenvolvimento da "Estratégia Quantitativa Agro" [cite: 3][cite_start], um projeto submetido por Willian Luiz da Silva [cite: 2, 64, 124] [cite_start]para o **Desafio Quant AI Itaú Asset 2025**[cite: 1, 63, 123].

## 1. Visão Geral do Projeto

[cite_start]O objetivo principal é desenvolver um portfólio de ações inovador e adaptativo, focado nas principais empresas do setor agro listadas na B3 (incluindo produção, insumos, proteína animal e logística)[cite: 69, 130].

[cite_start]A estratégia se diferencia dos modelos clássicos (que focam apenas em momentum e risco) [cite: 70] [cite_start]ao incorporar uma camada crítica de **fatores externos e ambientais**[cite: 70, 130]. [cite_start]O objetivo é tornar o portfólio "clima-sensível" [cite: 71][cite_start], capaz de antecipar riscos [cite: 70] [cite_start]e otimizar retornos com base em condições ambientais, logísticas e macroeconômicas[cite: 71, 130].

[cite_start]A meta é obter retornos ajustados ao risco superiores aos benchmarks do setor: o Ibovespa e o índice setorial agro[cite: 74, 131, 133].

## 2. A Estratégia: O Índice de Exposição ao Risco (IER)

[cite_start]O núcleo da estratégia é o **Índice de Exposição ao Risco (IER)**[cite: 82, 85, 135]. [cite_start]Este é um score preditivo que transforma dados ambientais brutos em um indicador de risco quantificável[cite: 81, 135].

### Fatores Externos Analisados

[cite_start]O IER é alimentado por um conjunto diversificado de dados[cite: 141]:

* [cite_start]**Clima e Geografia:** Anomalias de precipitação, seca e temperatura (Fontes: INMET, CHIRPS, ERA5, NOAA)[cite: 83, 142].
* [cite_start]**Satélite e Vegetação:** Índices de vegetação (NDVI) e estresse hídrico para monitorar a saúde das culturas (Fontes: MODIS, Sentinel-2)[cite: 83, 142].
* [cite_start]**Hidrologia e Energia:** Níveis de reservatórios e disponibilidade hídrica (Fontes: ANA, ONS)[cite: 83, 143].
* [cite_start]**Logística e Transporte:** Congestionamento em portos e tempo de escoamento da safra (Fontes: ANTT, Antaq)[cite: 83, 143].
* [cite_start]**Macro e Commodities:** Variações de preços de commodities (Soja, Milho) e câmbio (Fontes: CEPEA, Quandl, IPEA, Banco Central)[cite: 83, 144].

### Metodologia de Cálculo (3 Etapas)

[cite_start]O IER é calculado seguindo três etapas[cite: 87, 136]:

1.  [cite_start]**Padronização (Z-Score):** O valor atual de cada fator ($X$) é comparado à sua distribuição histórica para medir o desvio padrão[cite: 89, 137].
    * [cite_start]*Fórmula:* $\mathbf{z} = \frac {(X- \text{MÉDIA}(\text{RANGE}))}{\text{DESVPAD.P}(\text{RANGE})}$[cite: 90, 91].
2.  [cite_start]**Normalização (Função Logística):** O Z-Score é então transformado em um score limitado entre 0 (baixo risco) e 1 (alto risco)[cite: 86, 93, 138].
    * [cite_start]*Fórmula:* $\mathbf{Score} = \frac{1}{(1 + \text{EXP}(-k*z))}$[cite: 95].
3.  [cite_start]**Agregação (IER):** O IER final é o somatório ponderado ($w_i$) dos scores normalizados de cada fator[cite: 98, 99, 139].
    * [cite_start]*Fórmula:* $\mathbf{IER} = \sum (\mathbf{w}_i * \mathbf{Score}_i)$[cite: 100].

### Regras Operacionais (O Gatilho de Defesa)

[cite_start]O portfólio, composto pelas 10 melhores empresas do período, é rebalanceado mensalmente[cite: 78, 146]. [cite_start]O IER funciona como um "gatilho de defesa" [cite: 79, 147] que ajusta a alocação de ativos:

* [cite_start]**Risco Baixo ($IER < 0,25$):** O portfólio maximiza a exposição aos ativos selecionados para capturar ganhos em cenários favoráveis[cite: 115, 151].
* [cite_start]**Risco Moderado/Alto ($0,25 \le IER < 0,75$):** A exposição a setores afetados (ex: logística) é reduzida[cite: 111, 150].
* [cite_start]**Risco Extremo ($IER \ge 0,75$):** Ações de empresas diretamente expostas ao risco identificado (ex: seca severa) são excluídas ou têm seu peso drasticamente reduzido para proteger o portfólio[cite: 107, 108, 149].

## 3. Estrutura do Repositório e Execução

[cite_start]Este repositório contém os artefatos da **Fase 1 (Essencial)** do plano de execução, que foca em desenvolver, testar e documentar a estratégia para cumprir os requisitos do desafio[cite: 9, 12].

[cite_start]O plano de desenvolvimento é dividido em cinco scripts sequenciais[cite: 20]:

1.  [cite_start]**Coleta e Estruturação de Dados:** Busca de dados de APIs (ações, clima, macro) [cite: 23] [cite_start]e organização em banco local (Parquet/SQLite)[cite: 24].
2.  [cite_start]**Backtest de Baseline:** Execução de um backtest de referência (últimos 3 anos) sem o IER, usando critérios tradicionais[cite: 28, 29].
3.  [cite_start]**Implementação da Lógica Agro (IER):** O "coração do projeto"; script que aplica a metodologia (Z-Score, logística, agregação) para calcular o IER[cite: 31, 32].
4.  [cite_start]**Backtest Final com Fator Agro:** Refaz o backtest integrando o IER como o "gatilho de defesa" [cite: 33, 35] [cite_start]e aplicando as regras de rebalanceamento[cite: 36].
5.  [cite_start]**Geração Automatizada do Relatório:** Script final que utiliza os resultados do Passo 4 (gráficos, métricas) para montar o relatório[cite: 39].

### Scripts Principais no Repositório

* `Fatores_Externos.py`: Implementação principal da **Etapa 1**. Coleta dados macro e ambientais de múltiplas fontes, incluindo BCB (Câmbio, Selic), IPEA (IPCA), CEPEA (Milho), Quandl (Soja Futuro), INMET (Estações), Google Earth Engine (CHIRPS, MODIS NDVI), Open-Meteo (ERA5) e ANA (Nível de Rios).
* `itau-asset.py`: Script alternativo (V21) para a **Etapa 1**, focado em garantir a coleta de dados usando *proxies* estáveis via `yfinance` (para IAGRO, S&P GSCI e Soja) e a biblioteca `bcb` (para IPCA e ICC Agro). Este script gera o arquivo `indices_agro.xlsx`.
* `visualizar_dados.py`: Script auxiliar para análise exploratória e visualização dos dados coletados. Ele lê o arquivo `indices_agro.xlsx` e gera gráficos de evolução temporal, correlação (heatmap) e volatilidade.
* `logins.py`: Arquivo de configuração (template) para armazenar as chaves de API necessárias para a coleta de dados (ex: Quandl e Copernicus CDS).

## 4. Tecnologias Utilizadas (Core)

* [cite_start]**Linguagem Principal:** Python[cite: 16].
* **Análise de Dados e Backtesting:** Pandas, Matplotlib, Seaborn.
* **Coleta de Dados (APIs):** `requests`, `yfinance`, `python-bcb`, `ipeadatapy`, `quandl`, `cdsapi` (Copernicus) e `earthengine-api` (Google Earth Engine).
* [cite_start]**Ambiente e Versão:** VS Code [cite: 15] [cite_start]e GitHub[cite: 17].
* [cite_start]**IA Generativa:** Gemini e ChatGPT foram usados como ferramentas de apoio para acelerar a criação de scripts, depuração e a escrita do relatório, cumprindo um requisito chave do desafio[cite: 18, 154].

## 5. Sobre o Desafio Quant AI Itaú Asset 2025

* [cite_start]**Objetivo do Desafio:** Propor, testar e apresentar uma estratégia de investimento quantitativa[cite: 154].
* [cite_start]**Requisito Obrigatório:** O uso de Inteligência Artificial Generativa em ao menos uma etapa do processo (ideação, modelagem, documentação, etc.)[cite: 154, 162].
* [cite_start]**Entrega Final:** Um relatório em PDF de até 10 páginas [cite: 156][cite_start], um Factsheet visual [cite: 160] [cite_start]e uma seção obrigatória detalhando o uso de IA Generativa[cite: 162].
* [cite_start]**Critérios de Avaliação:** O projeto é avaliado com base em: Conceito da Estratégia (20%) [cite: 167][cite_start], Modelagem (20%) [cite: 168][cite_start], Uso de IA Generativa (15%) [cite: 169][cite_start], Backtest (15%) [cite: 170][cite_start], Análise dos Resultados (15%) [cite: 171][cite_start], Conclusão (10%) [cite: 172] [cite_start]e Apresentação do Robô (5%)[cite: 173].