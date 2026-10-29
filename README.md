# Análise Estatística e Testes de Hipóteses Aplicados a Negócios com Python

## Visão geral

Este projeto reúne aplicações de **inferência estatística** para investigar hipóteses de negócio com Python. Os exemplos contemplam desempenho de campanhas de marketing, satisfação de clientes por região, associação entre planos e cancelamentos (churn), diferenças de comportamento de compra e análises exploratórias de scores de crédito.

O objetivo é demonstrar como formular hipóteses, selecionar testes estatísticos, interpretar estatísticas e valores-p e comunicar resultados com atenção às limitações dos dados.

> **Escopo:** projeto educacional e demonstrativo. Os exemplos são análises estatísticas, não uma avaliação causal de campanhas ou um modelo de concessão de crédito em produção.

## Objetivos

- Formular hipóteses nula (H₀) e alternativa (H₁).
- Distinguir testes paramétricos e não paramétricos e compreender erros dos tipos I e II.
- Aplicar testes apropriados a comparações de grupos e associações entre variáveis.
- Explorar dados tabulares, gerar visualizações e interpretar resultados de forma crítica.
- Conectar conceitos estatísticos a casos de marketing, experiência do cliente e serviços financeiros.

## Tecnologias utilizadas

- **Python** — análise e execução dos exemplos.
- **Pandas** — leitura e manipulação de tabelas.
- **NumPy** — operações numéricas e simulação de scores.
- **SciPy (`scipy.stats`)** — testes de hipóteses.
- **Matplotlib** — histogramas para comparação de distribuições.
- **Jupyter Notebook** — código, resultados e explicações no mesmo ambiente.

## Bases de dados

| Arquivo | Registros | Variáveis | Aplicação |
|---|---:|---|---|
| `case_teste_t_campanha.csv` | 1.500 | `customer_id`, `period`, `ticket` | Testes t independente e pareado |
| `nps_regioes.csv` | 300 | `region`, `nps` | ANOVA entre Sul, Sudeste e Nordeste |
| `case_teste_mann_whitney.csv` | Não fornecido neste conjunto de arquivos | `sistema`, `ticket` (conforme notebook) | Mann-Whitney entre Android e iOS |

Outros exemplos utilizam pequenos conjuntos de dados declarados diretamente no notebook ou valores simulados. **O arquivo `case_teste_mann_whitney.csv` é necessário para executar integralmente o notebook, mas não foi incluído entre os arquivos disponibilizados.**

## Métodos e casos estudados

| Teste | Questão investigada | Resultado registrado no notebook |
|---|---|---|
| **t de Student independente** | O ticket difere entre grupos independentes antes/depois de uma campanha? | t = -4,8475; p < 0,0001 |
| **t de Student pareado** | Há diferença em medições emparelhadas? | t = -20,1083; p < 0,0001 |
| **ANOVA de uma via** | O indicador NPS difere entre três regiões? | F = 14,1305; p ≈ 0,00000137 |
| **Qui-Quadrado de independência** | Plano contratado e churn estão associados? | χ² = 13,0166; p ≈ 0,001491 |
| **Mann-Whitney U** | As distribuições de ticket de Android e iOS diferem? | U = 23.295; p ≈ 0,01779 |
| **Wilcoxon pareado** | As notas de satisfação mudaram após atualização? | W = 0; p ≈ 0,001953 |
| **Kruskal-Wallis** | Os scores diferem entre níveis de escolaridade? | H = 17,8182; p ≈ 0,000135 |
| **Kolmogorov-Smirnov (duas amostras)** | Distribuições simuladas de scores de aprovados e negados diferem? | KS ≈ 0,7533; p ≈ 1,56 × 10⁻⁸³ em uma execução |

**Nota:** o teste KS utiliza `np.random.normal` sem semente fixa; seus resultados mudam entre execuções. Os valores da tabela refletem a saída registrada no notebook, não uma validação de modelo preditivo. O exemplo de Mann-Whitney depende de uma base ausente no material entregue.

## Principais resultados

### 1. Campanha de marketing e ticket

Na base fornecida, há 500 observações em cada período:

| Período | Ticket médio |
|---|---:|
| Antes (`before`) | 185,24 |
| Depois — amostra independente (`after_independent`) | 196,21 |
| Depois — amostra pareada (`after_paired`) | 198,87 |

O teste independente apresenta evidência estatística de diferença entre as médias; a média posterior independente é aproximadamente **5,9% maior** que a anterior. O teste pareado também aponta diferença estatisticamente significativa conforme o resultado do notebook.

**Limitação:** testes de significância não demonstram, isoladamente, que uma campanha *causou* o aumento. Para conclusões causais, são necessários desenho experimental ou controles adicionais. Na análise pareada, também é importante confirmar explicitamente o emparelhamento correto dos clientes.

### 2. NPS por região

A base possui 100 observações por região:

| Região | Média do indicador `nps` |
|---|---:|
| Sul | 58,96 |
| Sudeste | 65,27 |
| Nordeste | 55,97 |

A ANOVA apresentou **F = 14,1305** e **p ≈ 0,00000137**, fornecendo evidência de que pelo menos uma das médias regionais difere. O teste, sozinho, **não identifica quais pares de regiões diferem**; isso exigiria testes pós-hoc apropriados.

### 3. Churn e plano contratado

O teste Qui-Quadrado aplicado a uma tabela de contingência construída no notebook apresentou **χ² = 13,0166** e **p ≈ 0,001491**, indicando associação estatística entre o tipo de plano e o cancelamento no exemplo apresentado. Associação não implica causalidade.

### 4. Scores de crédito

Os exemplos de Kruskal-Wallis e Kolmogorov-Smirnov demonstram comparação entre grupos e distribuições. No caso do KS, os scores são **simulados**, não resultam de treinamento ou validação de um modelo real de crédito; portanto, o teste não comprova capacidade preditiva de um modelo de produção.

## Estrutura sugerida do repositório

```text
analise-estatistica-testes-hipoteses/
├── README.md
├── Testes_de_hipotese.ipynb
├── case_teste_t_campanha.csv
├── nps_regioes.csv
```

Para executar todos os exemplos, também é necessário adicionar `case_teste_mann_whitney.csv` à pasta ou adaptar a respectiva seção do notebook a uma fonte de dados disponível.

## Como executar

1. Clone o repositório e abra a pasta em seu ambiente de desenvolvimento.
2. Crie um ambiente virtual (recomendado).
3. Instale as bibliotecas:

   ```bash
   pip install numpy pandas scipy matplotlib notebook
   ```
4. Abra `Testes_de_hipotese.ipynb` com Jupyter Notebook ou VS Code.
5. Execute as células em ordem, mantendo os arquivos CSV no diretório de trabalho do notebook.
