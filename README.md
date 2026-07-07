# Panorama das exportações brasileiras (2025) | ETL com Power Query e Python + Dashboard Power BI

## 📌 Sobre o Projeto

Análise de **1,7M registros** do fluxo de mercadorias exportadas pelo Brasil em 2025, identificando padrões sobre a dinâmica logística e especialização regional.

**Stack:**
- **Power BI + Power Query** → Transformação, modelagem e visualização
- **Python (pandas)** → Validação de encoding e consistência dos dados
- **Google Colab** → Ambiente de desenvolvimento

**Entregas:**
- Dashboard
- KPIs (Ticket Médio, Peso Médio)
- Insights estratégicos
- Notebooks com validações

---
## 📊 Dashboard

| Visão Geral | Análise Regional | Modal de Transporte |
|-------------|------------------|---------------------|
| ![Visão Geral](../images/dashboard-geral.png) | ![Análise Regional](../images/dashboard-estados.png) | ![Modal](../images/dashboard-vias.png) |

---

## 📊 Principais Insights

### 1. Especialização regional dos estados

- **SP** lidera em **receita** (US$ 71 Bi), com volume relativamente baixo → exportação de produtos industrializados e de alto valor agregado (açúcares, óleos, carnes processadas)

- **MG** e **PA** lideram em **volume** (207 Bi e 190 Bi kg) e se destacam em receita (US$ 46 Bi e US$ 24 Bi) → commodities pesadas (minério, soja) de baixo valor unitário, mas altíssimo peso

- **Rio de Janeiro (RJ)** ocupa a **segunda posição em receita** (US$ 49 Bi) e **terceira em volume** (116 Bi kg), com destaque para a exportação de petróleo e derivados, equilibrando valor e peso

**💡Insight:** O Brasil transporta em duas velocidades:

---

### 2. Modal aéreo: pouco peso, muito valor

- O modal **aéreo** transporta apenas **~1% do peso total** das exportações mas responde por **~6,5% do valor total** (US$ 23 Bi)

**💡Insight:** Produtos de altíssimo valor agregado (eletrônicos, medicamentos, partes de aeronaves) utilizam o modal aéreo, onde o custo do frete é compensado pelo valor da mercadoria. Isso revela uma **oportunidade** para ampliar o uso do modal aéreo em cadeias produtivas de alto valor.

---

### 3. Ticket médio por país

- **Irã** apresenta o maior ticket médio (US$ 6,5 Mi por operação), seguido por China (US$ 3,4 Mi) e Argélia (US$ 1,8 Mi)

**💡Insight:** Países com ticket médio alto e volume baixo realizam operações pontuais de produtos de alto valor agregado → oportunidade para diversificação sem aumentar volume físico

---

### 4. Concentração da receita e volume na China

- A **China** responde por **~30% da receita total** de exportação (US$ 100 Bi)
- Também concentra **~52,54% do volume total** exportado (0,45 Tri kg)

**💡Insight:** O Brasil apresenta uma **forte dependência estrutural do mercado chinês**, especialmente para commodities. Uma eventual retração da demanda chinesa impactaria significativamente a balança comercial brasileira, indicando a necessidade de investigação da viabilidade de uma **diversificação de mercados**.

---

## 🔗**Notebook com Validações Disponível:** [`notebooks/validador_comex.ipynb`](link)

---

## 🔗 Acesso aos Dados

A tabela FATO (`EXP_2025.csv`) **não está incluída** (~1,7 GB). Baixe em:

👉 [Comex Stat - MDIC](https://comexstat.mdic.gov.br/) (ano: 2025 | tipo: exportação)

**Tabelas auxiliares** (NCM, UF, VIA, PAIS) disponíveis em `data/tabelas-auxiliares/`.

---

## 📐 Modelo de Dados (Star Schema)

### Relacionamentos (1:N)
| Tabela (1) | Coluna (PK) | Tabela (N) | Coluna (FK) |
|------------|-------------|------------|-------------|
| dim_pais | CO_PAIS | fato_exportacoes | CO_PAIS |
| dim_uf | Sigla | fato_exportacoes | SG_UF_NCM |
| dim_ncm | Código NCM | fato_exportacoes | CO_NCM |
| dim_via | Via | fato_exportacoes | CO_VIA |

---

## 🔄 Tratamentos Realizados no Power Query

**1. Ajuste do cabeçalho da `dim_uf`**
- Problema: Cabeçalho na 2ª linha do CSV
- Solução: Remoção da 1ª linha + promoção do novo cabeçalho

**2. Conversão da coluna `CO_NCM`**
- Problema: Códigos com zero à esquerda eram perdidos (0101 virava 101)
- Solução: Conversão para **texto** (fato e dimensão)

----

## 👩‍💻 Autora

Sofia Fernandes Job Junqueira