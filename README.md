# Laboratório de Estatística Aplicada — DEs/UFSCar

Atividades do grupo **Arthur Gon (RA 811464)** e **Isabela Viana (RA 811753)**.
Prof. Helton Graziadei.

| Atividade | Tema | Arquivos |
|---|---|---|
| [`atividade-conformal/`](atividade-conformal/) | Quantificando incertezas com predição conformal (base 2: Bikeshare) | `.qmd` respondido (Tarefas 1–5, Seção 7 opcional e Seção 8 extra com Mondrian CP), `.html` renderizado, slides |

## Como reproduzir

Requisitos: R (≥ 4.3) e Quarto (ou RStudio/Positron/VS Code com a extensão Quarto).

```r
install.packages(c("ISLR2", "ranger", "dplyr", "tidyr", "ggplot2", "knitr", "rmarkdown"))
```

```bash
quarto render atividade-conformal/atividade-conformal.qmd
```

Todas as etapas aleatórias usam sementes fixas, então o `.html` gerado reproduz exatamente os números do relatório.

## Estrutura

```
atividade-conformal/
├── atividade-conformal.qmd     # entrega: RAs + Tarefas 1–5 + Seção 7 (opcional) + Seção 8 (extra: Mondrian CP)
├── atividade-conformal.html    # entrega: relatório renderizado (autocontido)
└── material-aula/
    ├── slides.pdf                          # slides da aula
    └── atividade-conformal-original.qmd    # enunciado original, sem alterações
```
