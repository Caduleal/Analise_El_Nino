# Análise de Temperatura da Superfície do Mar (TSM / SST) e Fenômeno ENOS

Este repositório contém a análise exploratória, tratamento estatístico e visualizações gráficas da evolução da Temperatura da Superfície do Mar (TSM/SST).

---

## 🔍 Visão Geral e Principais Descobertas

O estudo foca na quantificação sistemática do aquecimento oceânico e na dinâmica do ciclo El Niño-Oscilação do Sul (ENOS), revelando alterações severas na normalidade térmica. As principais descobertas incluem:

- **Linha de Base Climatológica:** Definida como 1991–2020 (em alinhamento com as diretrizes da OMM), utilizando o conjunto de dados ERSST v5 (NOAA).
- **Taxa de Aquecimento Global:** Calculada entre $+0,16^\circ\text{C}$ e $+0,17^\circ\text{C}$ por década, em relação a uma média base de $18,30^\circ\text{C}$.
- **Assimetria de Massa Térmica ($\int \Delta T \, dt$):** Os dados atestam que os eventos de El Niño modernos acumulam exponencialmente mais energia latente na região do Pacífico Tropical (Niño 3.4) do que o resfriamento promovido pelas fases de La Niña.
- **Fenômeno da "Atenuação Fria":** A componente estritamente negativa das anomalias tem se suprimido a uma taxa de atenuação de $+0,05^\circ\text{C}$ por década.
- **Novo Patamar Térmico (2026):** O limite inferior ou patamar de "baixa" registrado nos anos recentes (até 2026) já rivaliza com os picos máximos históricos das décadas de 1980 e 1990.

---

## 🧮 Metodologia Analítica e Formulação Matemática

O núcleo da análise é suportado pelas seguintes rotinas matemáticas aplicadas às matrizes de temperatura:

1. **Cálculo da Anomalia Termodinâmica:**
   O desvio local é calculado em relação à linha de base climatológica específica daquele mês.
   $$\Delta T_{i,j,t} = T_{obs(i,j,t)} - \overline{T_{clima(i,j,m)}}$$

2. **Média Espacial Ponderada (Correção Geométrica):**
   Para mitigar a super-representação das altas latitudes nas projeções espaciais, a média global aplica uma ponderação pelo cosseno da latitude ($\theta$).
   $$W = \cos(\theta)$$
   $$\overline{\Delta T_{global}} = \frac{\sum (\Delta T_{i,j} \cdot \cos(\theta_i))}{\sum \cos(\theta_i)}$$

3. **Filtragem por Média Móvel (Sinal Multidecenal):**
   A assinatura interanual ruidosa foi suprimida aplicando médias móveis centradas, em especial de 5 anos (60 meses).
   $$\overline{\Delta T_{suave}}(t) = \frac{1}{60} \sum_{n=-29}^{30} \Delta T(t+n)$$

---

## Visualizações e Gráficos Gerados

As imagens e animações geradas durante a execução do projeto estão salvas no repositório:

### 1. Evolução Global da TSM (Animação)
Acompanhamento temporal da variação de temperatura ao longo dos anos.
<div align="center">

![Evolução Global TSM 2026](evolucao_global_tsm_2026.gif)

</div>

### 2. Série Temporal
Gráficos de linhas e dispersão mostrando as variações de temperatura.
<div align="center">

![Análise de TSM 1](newplot.png)
<br>
![Análise de TSM 2](newplot%20%281%29.png)

</div>

### 3. Anomalias
Análises comparativas e distribuições estatísticas.
<div align="center">

![Análise de TSM 3](newplot%20%282%29.png)
<br>
![Análise de TSM 4](newplot%20%283%29.png)

</div>

### 4. Anomalias e Tendências
<div align="center">

![Análise de TSM 5](newplot%20%284%29.png)
<br>
![Análise de TSM 6](newplot%20%285%29.png)

</div>

---

## Visão Geral e Explicação do Notebook

Abaixo consta a explicação sucinta de cada etapa do pipeline processado no Jupyter Notebook:

1. **Carregamento e Limpeza de Dados:**
   * Leitura das bases históricas ERSST v5 em formato multidimensional `NetCDF` (usando `xarray`).
   * Padronização de coordenadas e recortes latitudinais.
2. **Cálculo da Climatologia Base e Anomalia Espacial:**
   * Derivação da média climatológica para a linha de base de 1991–2020.
   * Aplicação da ponderação pelo cosseno da latitude ($\cos(\theta)$) para extração correta das médias regionais e globais.
3. **Massa Térmica Acumulada e Estatística:**
   * Cálculo da integral da massa térmica acumulada ($\int \Delta T \, dt$) segregando fases quentes e frias.
   * Aplicação de modelos de regressões lineares (método dos mínimos quadrados) para isolamento da inclinação secular e taxas de aquecimento.
4. **Visualizações Gráficas e Animações:**
   * Construção de arrays gráficos avançados, dual-axis plots e sombreamentos utilizando Plotly, evidenciando assimetrias e tendências de atenuação.
   * Geração e exportação de animações geográficas (`.gif`).

---

## Estrutura do Repositório

```
.
├── El_nino.ipynb                # Notebook com os códigos de análise
├── evolucao_global_tsm_2026.gif  # Animação gerada
├── newplot.png                   # Gráfico exportado
├── newplot (1).png               # Gráfico exportado
├── newplot (2).png               # Gráfico exportado
├── newplot (3).png               # Gráfico exportado
├── newplot (4).png               # Gráfico exportado
├── newplot (5).png               # Gráfico exportado
├── README.md                     # Documentação do projeto
└── .gitignore                    # Arquivos ignorados pelo Git
```

---

## Tecnologias Utilizadas

* **Linguagem:** Python
* **Manipulação de Dados:** Pandas, NumPy, Xarray
* **Visualização de Dados:** Plotly, Matplotlib, Seaborn
* **Ambiente de Desenvolvimento:** Jupyter Notebook / VS Code

> ⚠️ **Nota de Pendência:** Falta realizar redução de algarismos significativos nos resultados calculados.