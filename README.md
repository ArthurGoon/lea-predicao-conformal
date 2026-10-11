# Predição conformal: intervalos de predição para a demanda de bicicletas

**Atividade em grupo — Laboratório de Estatística Aplicada · UFSCar · 2026/2**
Docente: Prof. Helton Graziadei

Dupla: **Arthur Pereira Gon** (RA 811464) · **Isabella Viana Bambirra** (RA 811753)

---

## Entrega

| Arquivo | Conteúdo |
|---|---|
| [`atividade-conformal.qmd`](atividade-conformal.qmd) | Documento Quarto com o código e as respostas das Tarefas 1 a 5, da Seção 7 (opcional) e da Seção 8 (extensão) |
| [`atividade-conformal.html`](atividade-conformal.html) | Relatório renderizado, autocontido (baixar e abrir no navegador) |

## Pergunta

Como construir intervalos de predição de 90% para o número de bicicletas alugadas por hora com cobertura garantida, sem supor normalidade nem variância constante dos erros? E essa garantia vale dentro de cada faixa horária, ou só na média?

## Dados

A base de cada grupo é definida por $(\sum_j \text{RA}_j) \bmod 4 + 1$. Para esta dupla, $(811464 + 811753) \bmod 4 + 1 = 2$: base **Bikeshare** (pacote `ISLR2`), com **8.645 horas** de aluguel de bicicletas em Washington, D.C. A resposta é `bikers` (bicicletas alugadas por hora) e os subgrupos são quatro faixas horárias: madrugada, dia, pico (16-19h) e noite. As variáveis `casual` e `registered` foram excluídas porque somam exatamente a resposta.

## Métodos

Divisão treino/calibração/teste de 40/30/30, nível $\alpha = 0{,}10$ e 50 repetições com sementes fixas.

| Método | Descrição |
|---|---|
| Clássico (lm) | Intervalo de predição da regressão linear (supõe erros normais e homoscedásticos) |
| Conformal (lm) | *Split conformal* com escore $\lvert Y - \hat\mu(X) \rvert$ e $\hat\mu$ = regressão linear |
| Conformal (floresta) | O mesmo, com $\hat\mu$ = floresta aleatória (`ranger`) |
| Conformal normalizado | Escore $\lvert Y - \hat\mu(X) \rvert / \hat\sigma(X)$, com $\hat\sigma$ ajustado nos resíduos *out-of-bag* do treino (Seção 7) |
| Mondrian (floresta) | Quantil conformal calculado separadamente em cada faixa horária (Seção 8) |

## Resultados

Médias de 50 repetições.

| Método | Cobertura global | Madrugada | Dia | Pico | Noite | Comprimento médio |
|---|---:|---:|---:|---:|---:|---:|
| Clássico (lm) | 0,890 | 0,993 | 0,843 | 0,753 | 0,996 | 250 |
| Conformal (lm) | 0,898 | 0,995 | 0,854 | 0,769 | 0,997 | 259 |
| Conformal (floresta) | 0,900 | 0,999 | 0,869 | 0,762 | 0,969 | 181 |
| Conformal normalizado | 0,899 | 0,949 | 0,887 | 0,818 | 0,935 | 138 |
| Mondrian (floresta) | 0,902 | 0,901 | 0,903 | 0,904 | 0,900 | 168 |

Os métodos conformais atingem a cobertura nominal de 90% na média, como garante a teoria. Com a floresta aleatória, os intervalos ficam cerca de 30% mais curtos que com a regressão linear. A garantia, porém, é marginal: com largura fixa, o intervalo cobre quase todas as horas da madrugada e só ~77% das horas de pico, quase sempre subestimando a demanda. O escore normalizado reduz o comprimento médio em 24% e melhora o pico, mas não chega a 90%. A calibração por faixa horária (Mondrian) atinge ~90% em todas as faixas e mantém intervalos mais curtos, em média, que a calibração global.

## Reprodução

Requisitos: R (≥ 4.3) e Quarto, ou RStudio, Positron ou VS Code com a extensão Quarto.

```r
install.packages(c("ISLR2", "ranger", "dplyr", "tidyr", "ggplot2", "knitr", "rmarkdown"))
```

```bash
quarto render atividade-conformal.qmd
```

Todas as etapas aleatórias usam sementes fixas, de modo que a renderização reproduz exatamente os números do relatório. A execução completa leva alguns minutos.
