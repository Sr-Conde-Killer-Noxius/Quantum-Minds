

````markdown
# Estratégia Quantitativa Agro  
### Desafio Quant AI Itaú Asset 2025  

> Este repositório contém o plano de execução, os scripts de coleta de dados e a metodologia do projeto Estratégia Quantitativa Agro, desenvolvido para o Desafio Quant AI Itaú Asset 2025.

---

## 1. Visão Geral do Projeto  

O objetivo é desenvolver um portfólio quantitativo adaptativo focado nas principais empresas do setor agro listadas na B3 (produção, insumos, proteína animal e logística).  

A estratégia difere dos modelos clássicos (momentum e risco) ao incorporar fatores ambientais e macroeconômicos, tornando o portfólio sensível ao clima e capaz de antecipar riscos e otimizar retornos.  

Meta: obter retornos ajustados ao risco superiores aos benchmarks setoriais (Ibovespa e Índice Agro).  

---

## 2. Núcleo da Estratégia – Índice de Exposição ao Risco (IER)  

O IER é um score preditivo que converte dados ambientais em um indicador quantitativo de risco.  

### Fatores Externos Analisados
- Clima e Geografia: anomalias de precipitação, seca e temperatura (INMET, CHIRPS, ERA5, NOAA)  
- Satélite e Vegetação: NDVI e estresse hídrico (MODIS, Sentinel-2)  
- Hidrologia e Energia: níveis de reservatórios e disponibilidade hídrica (ANA, ONS)  
- Logística e Transporte: congestionamento portuário e tempo de escoamento da safra (ANTT, Antaq)  
- Macro e Commodities: preços de soja e milho, câmbio e juros (CEPEA, IPEA, Quandl, BCB)

````
### Metodologia de Cálculo

```diff
1. Padronização (Z-Score)
   z = (X - média) / desvio_padrão

2. Normalização (Função Logística)
   Score = 1 / (1 + EXP(-k*z))

3. Agregação (IER)
   IER = Σ (wᵢ * Scoreᵢ)

````

### Regras Operacionais – Gatilho de Defesa

O portfólio contém as 10 melhores empresas do período e é rebalanceado mensalmente.

| Nível de Risco | IER               | Ação Estratégica                          |
| -------------- | ----------------- | ----------------------------------------- |
| Baixo          | IER < 0,25        | Maximiza exposição aos ativos             |
| Moderado/Alto  | 0,25 ≤ IER < 0,75 | Reduz exposição a setores sensíveis       |
| Extremo        | IER ≥ 0,75        | Exclui ativos com risco ambiental elevado |

---

## 3. Estrutura do Repositório e Execução

A Fase 1 (Essencial) do projeto inclui cinco scripts principais:

| Etapa | Script                       | Descrição                                                             |
| ----- | ---------------------------- | --------------------------------------------------------------------- |
| 1     | Fatores_Externos.py          | Coleta dados macro e ambientais (BCB, IPEA, CEPEA, INMET, MODIS, ANA) |
| 2     | itau-asset.py                | Alternativo estável usando yfinance e bcb                             |
| 3     | visualizar_dados.py          | Geração de gráficos e análise exploratória                            |
| 4     | logins.py                    | Template de configuração com chaves de API                            |
| 5     | report_auto.py *(planejado)* | Geração automatizada de relatório e métricas                          |

### Fluxo de Execução

1. Coleta e estruturação dos dados
2. Backtest baseline (3 anos)
3. Implementação do IER
4. Backtest final com fator agro
5. Geração do relatório final

---

## 4. Tecnologias Utilizadas

* Linguagem: Python
* Análise e Backtesting: pandas, matplotlib, seaborn
* Coleta de Dados: requests, yfinance, python-bcb, ipeadatapy, quandl, cdsapi, earthengine-api
* Ambiente: VS Code + GitHub
* IA Generativa: Gemini e ChatGPT (utilizados na automação e documentação)

---

## 5. Sobre o Desafio Quant AI Itaú Asset 2025

**Objetivo:** propor, testar e apresentar uma estratégia quantitativa de investimento.
**Requisito:** uso de IA Generativa em pelo menos uma etapa (ideação, modelagem ou documentação).

### Entregas

* Relatório PDF (máx. 10 páginas)
* Factsheet visual
* Seção explicando o uso de IA

### Critérios de Avaliação

| Critério               | Peso |
| ---------------------- | ---- |
| Conceito da Estratégia | 20%  |
| Modelagem              | 20%  |
| Uso de IA Generativa   | 15%  |
| Backtest               | 15%  |
| Análise de Resultados  | 15%  |
| Conclusão              | 10%  |
| Apresentação do Robô   | 5%   |

---

**Ano:** 2025
**Instituição:** Itaú Asset Management – Desafio Quant AI
**Projeto:** Estratégia Quantitativa Agro
