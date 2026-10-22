# Metodologia

## Pergunta de negócio

Uma nova estratégia de prevenção à fraude consegue reduzir eventos fraudulentos/CBK sem gerar bloqueios excessivos de pedidos legítimos?

## Unidade de análise

Cada linha representa um pedido.

## Resultado real x decisão

`resultado_real` é o desfecho usado para avaliação no dataset público sintético. `decisao_a` e `decisao_b` são decisões produzidas pelas duas políticas.

No uso das bases históricas reais, essa distinção precisa ser preservada. Um pedido "liberado após análise de risco" não deve ser chamado de legítimo confirmado se não houver desfecho posterior que confirme isso.

## A/B retrospectivo

As duas estratégias são aplicadas à mesma população para comparar suas políticas de decisão. Como não houve randomização real de tráfego em produção, o estudo não deve ser apresentado como um A/B Test online causal.

Para a comparação pareada das decisões A e B, o notebook usa o teste de McNemar, adequado para observar diferenças entre classificações pareadas na mesma população.

## Métricas

- **TP:** fraude bloqueada.
- **TN:** legítimo aprovado.
- **FP:** legítimo bloqueado.
- **FN:** fraude aprovada.
- **FPR:** FP / (FP + TN).
- **FNR:** FN / (FN + TP).
- **Recall:** TP / (TP + FN).
- **Precision:** TP / (TP + FP).

## Impacto financeiro

O exemplo público usa custos hipotéticos editáveis. Em um projeto corporativo, esses custos devem ser substituídos por valores reais: perda média por fraude, custo do chargeback, margem, custo de atendimento, custo de revisão manual e valor esperado do cliente.

## Limitações

- O dataset publicado é sintético.
- Os resultados publicados não representam desempenho histórico real.
- As regras A e B são demonstrativas.
- Sem desfecho posterior completo, bases históricas de pedidos liberados não permitem afirmar que todos são legítimos confirmados.
- Resultados retrospectivos não equivalem automaticamente a causalidade de um experimento online.
