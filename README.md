# Laboratório de Estatística Aplicada — DEs/UFSCar

Atividades em grupo da disciplina Laboratório de Estatística Aplicada (Prof. Helton Graziadei).

**Grupo:** Arthur Gon (RA 811464) e Isabela Viana (RA 811753).

## Atividades

| Pasta | Tema | Relatório |
|---|---|---|
| [`atividade-conformal/`](atividade-conformal/) | Quantificando incertezas com predição conformal | [`atividade-conformal.html`](atividade-conformal/atividade-conformal.html) |

---

## Predição conformal — base 2 (Bikeshare)

A base de cada grupo é definida por $(\sum_j \text{RA}_j) \bmod 4 + 1$. Para este grupo, $(811464 + 811753) \bmod 4 + 1 = 2$, ou seja, a base **Bikeshare** (`ISLR2`): número de bicicletas alugadas por hora em Washington, D.C. (8.645 horas), com intervalos de predição de 90%.

**Principais resultados**

| | |
|---|---|
| Dados | Resposta assimétrica e fortemente heteroscedástica: desvio-padrão de 24 bicicletas na madrugada contra 150 no pico (16-19h). |
| Clássico × conformal | Os três métodos ficam perto de 90% de cobertura; com floresta aleatória, o conformal gera intervalos ~30% mais curtos que com regressão linear. |
| 50 repetições | Cobertura média dos métodos conformais ≈ 90%, como prevê a teoria; o intervalo clássico fica quase sempre um pouco abaixo. |
| Cobertura por subgrupo | A garantia é marginal: ~100% na madrugada e só ~77% no pico. |
| Seção 7 (opcional) | Escore normalizado: comprimento médio 24% menor e cobertura no pico de 76% → 82%. |
| Seção 8 (extensão do grupo) | Mondrian CP (calibração por faixa horária): ~90% em todas as faixas, com intervalos mais curtos em média. |

**Arquivos**

```
atividade-conformal/
├── atividade-conformal.qmd     # documento-fonte: código e respostas
├── atividade-conformal.html    # relatório renderizado (autocontido, abre em qualquer navegador)
└── material-aula/
    ├── slides.pdf                          # slides da aula
    └── atividade-conformal-original.qmd    # enunciado original, sem alterações
```

Para ler o relatório, baixe o `.html` e abra no navegador (o GitHub mostra só o código-fonte do arquivo).

## Como reproduzir

Requisitos: R (≥ 4.3) e Quarto (ou RStudio, Positron ou VS Code com a extensão Quarto).

```r
install.packages(c("ISLR2", "ranger", "dplyr", "tidyr", "ggplot2", "knitr", "rmarkdown"))
```

```bash
quarto render atividade-conformal/atividade-conformal.qmd
```

Todas as etapas aleatórias usam sementes fixas, então a renderização reproduz exatamente os números do relatório. Na base Bikeshare, a execução completa leva alguns minutos.
