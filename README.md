# A/B Test de Estratégias de Prevenção à Fraude

Projeto de portfólio que transforma uma experiência histórica de análise de risco e fraude, originalmente realizada com Excel, em um fluxo analítico reproduzível em Python.

## Objetivo

Comparar uma estratégia antifraude de referência (**A**) com uma estratégia proposta (**B**), avaliando o equilíbrio entre:

- redução de fraude/chargeback;
- aprovação de pedidos;
- falsos positivos (bloqueio indevido);
- falsos negativos (fraude aprovada);
- impacto financeiro estimado.

## Contexto histórico

O projeto foi inspirado em análises operacionais realizadas em uma operação de risco e crédito em 2016–2017. Um relatório histórico de Charge Back, referente a dezembro de 2016 a março de 2017, registra ataques específicos em bandeiras de cartões com alto valor aquisitivo e aponta problemas de parametrização de ferramentas, falhas humanas e comunicação como fatores associados ao aumento de casos.

A proposta aqui é demonstrar como um raciocínio de prevenção à fraude feito originalmente com Excel pode ser reestruturado com Python, pandas e métricas estatísticas.

## Dados públicos do repositório

Por segurança e confidencialidade, **nenhum dado histórico real contendo dados pessoais ou operacionais é publicado neste repositório**.

O arquivo `data/dataset_publico_sintetico.csv` é **sintético**, criado apenas para reproduzir uma estrutura plausível de análise e permitir que o notebook seja executado por terceiros.

As bases históricas reais podem ser utilizadas apenas em ambiente privado/autorizado para análises adicionais.

## Metodologia

O notebook executa uma comparação retrospectiva das duas políticas sobre a mesma população sintética. Isso é melhor descrito como uma **avaliação A/B retrospectiva de políticas**, e não como um experimento online randomizado.

### Estratégia A — referência

Bloqueia quando ocorre pelo menos uma das condições:

- score >= 0,92;
- sinal de ataque;
- valor >= R$ 5.000 e velocidade >= 3.

### Estratégia B — proposta

Bloqueia quando ocorre pelo menos uma das condições:

- score >= 0,90;
- sinal de ataque;
- valor >= R$ 3.500 e velocidade >= 2;
- recorrência de IP >= 5 e recorrência de e-mail >= 3.

Os limiares acima são **regras demonstrativas do projeto sintético**, não regras históricas atribuídas à empresa.

## Métricas

- Approval Rate
- Block Rate
- False Positive Rate (FPR)
- False Negative Rate (FNR)
- Precision
- Recall
- F1-score
- TP, TN, FP e FN
- impacto financeiro estimado

Para o impacto financeiro do exemplo, são usadas premissas explícitas e editáveis:

- custo de FN = 80% do valor do pedido;
- custo de FP = 10% do valor do pedido, como margem perdida estimada.

Esses percentuais são **hipóteses didáticas**, não perdas históricas reais.

## Resultado do exemplo sintético

Na execução atual do dataset público, a estratégia B reduz a taxa de falsos negativos e aumenta a detecção de fraude, mas também aumenta a taxa de falsos positivos e reduz a aprovação. Com as premissas financeiras didáticas adotadas, o custo total estimado também muda. Esses resultados são ilustrativos e não devem ser apresentados como resultados da operação histórica.

## Estrutura

```text
ab-test-antifraude/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── dataset_publico_sintetico.csv
│   └── README.md
├── notebooks/
│   └── ab_test_antifraude.ipynb
└── docs/
    └── metodologia.md
```

## Competências demonstradas

`Python` · `Pandas` · `NumPy` · `Scikit-learn` · `Statsmodels` · `Data Analytics` · `A/B Testing` · `Fraud Prevention` · `Risk Analysis` · `Confusion Matrix` · `FPR/FNR` · `Business Metrics`

## Próximas evoluções

1. Incorporar uma base de desfecho posterior confiável.
2. Calibrar os limiares com validação fora da amostra.
3. Separar regras de bloqueio de regras de revisão manual.
4. Incluir custo real de chargeback, margem e custo operacional.
5. Avaliar estabilidade das regras por período, canal e produto.
