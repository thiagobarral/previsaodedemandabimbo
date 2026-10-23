# Previsão de demanda | Grupo Bimbo

Estudo de regressão em R para estimar a demanda ajustada de produtos de panificação, utilizando dados históricos da competição **Grupo Bimbo Inventory Demand**, do Kaggle.

> **Status:** estudo acadêmico documentado em relatório. Os scripts-fonte e o ambiente original ainda não estão disponíveis neste repositório. O resultado histórico abaixo não representa uma validação de previsão de semanas futuras.

## Problema de negócio

Produtos perecíveis exigem equilíbrio entre disponibilidade e excesso de estoque. Estimar a demanda pode apoiar o planejamento de abastecimento e ajudar a reduzir rupturas e desperdício.

Este projeto explora esse problema com dados do Grupo Bimbo. Não houve implantação operacional nem mensuração de redução de custos; esses são benefícios potenciais da aplicação.

## Visão geral

| Item | Descrição |
| --- | --- |
| Autor | Thiago Barral |
| Contexto | Avaliação da formação de Cientista de Dados da Data Science Academy |
| Relatório original | Janeiro de 2020 |
| Linguagem | R |
| Modelo documentado | Regressão linear com `bigglm` |
| Variável-alvo | `Demanda_uni_equil` — demanda ajustada em unidades |
| Separação temporal | Semanas 3 a 8 para treinamento; semana 9 para avaliação |
| Métrica | Root Mean Squared Logarithmic Error (RMSLE); menor é melhor |

## Relatório

📄 **[Ler a análise original em PDF](Projeto2.pdf)**

O relatório contém código exibido, análise exploratória, decisões de preparação dos dados e a saída da avaliação. Ele foi preservado como registro histórico; as limitações identificadas na revisão estão descritas abaixo.

## Dados

Fonte: [Grupo Bimbo Inventory Demand — Kaggle](https://www.kaggle.com/c/grupo-bimbo-inventory-demand).

A execução documentada leu **74.180.464 registros** do arquivo `train.csv`, com aproximadamente 3,2 GB em disco. Essa escala exige planejamento de memória, especialmente quando são criadas cópias dos dados.

Os dados não estão versionados neste repositório. Consulte as condições de acesso e uso na página da competição antes de obtê-los.

### Dicionário de variáveis

| Variável | Descrição |
| --- | --- |
| `Semana` | Número da semana, de quinta-feira a quarta-feira |
| `Agencia_ID` | Identificador do depósito de vendas |
| `Canal_ID` | Identificador do canal de vendas |
| `Ruta_SAK` | Identificador da rota de distribuição |
| `Cliente_ID` | Identificador do cliente |
| `Producto_ID` | Identificador do produto |
| `Venta_uni_hoy` | Unidades vendidas na semana |
| `Venta_hoy` | Valor das vendas na semana, em pesos |
| `Dev_uni_proxima` | Unidades devolvidas na semana seguinte, conforme a descrição original |
| `Dev_proxima` | Valor das devoluções na semana seguinte, em pesos |
| `Demanda_uni_equil` | Demanda ajustada em unidades; variável-alvo |
| `NombreCliente` | Nome do cliente, em tabela auxiliar |
| `NombreProducto` | Nome do produto, em tabela auxiliar |

## Metodologia documentada

1. **Leitura e seleção inicial:** carregamento com `data.table::fread` e exclusão de `Venta_hoy`, `Dev_proxima` e `Ruta_SAK`.
2. **Exploração:** correlações na semana 3 e análise das devoluções por semana; exclusão de `Agencia_ID` e `Cliente_ID` com base na correlação observada.
3. **Separação temporal:** semanas 3 a 8 para treino e semana 9 reservada para avaliação.
4. **Tratamento de extremos:** manutenção de linhas com `Dev_uni_proxima < 25` na semana 3, `< 30` na semana 4 e `< 20` nas semanas 5 a 8. O conjunto de avaliação não recebeu esses filtros.
5. **Modelagem:** regressão com `Canal_ID`, `Producto_ID`, `Venta_uni_hoy` e `Dev_uni_proxima`; remoção de `Semana` antes do ajuste.
6. **Avaliação:** previsões negativas substituídas por zero e cálculo do RMSLE na semana 9.

Pacotes carregados no relatório: `data.table`, `dplyr`, `DataExplorer`, `ggplot2`, `biglmm` e `Metrics`. Essa lista descreve a execução histórica; não substitui um ambiente com versões verificadas.

## Resultado histórico e interpretação

| Experimento | Conjunto de avaliação | RMSLE registrado |
| --- | --- | --- |
| Regressão linear documentada | Semana 9 do arquivo de treino | **0,0586998** |

**Esse número foi transcrito do relatório e não foi recalculado nesta revisão.** Não é uma pontuação confirmada no conjunto de teste da competição.

A separação por semanas é útil, mas não basta para garantir uma previsão válida: também é necessário que todas as entradas estejam disponíveis no momento da decisão. O experimento usa vendas e devoluções associadas à própria observação avaliada. Para antecipar demanda de uma semana futura, essas informações podem ainda não existir, caracterizando risco de vazamento de informação.

Assim, o resultado deve ser interpretado como uma avaliação retrospectiva com essas entradas, e não como evidência de desempenho operacional de previsão antecipada.

## Limitações técnicas

- **Disponibilidade temporal das variáveis:** uma nova versão deve definir o horizonte de previsão e usar apenas informações conhecidas antes dele, como históricos defasados.
- **Identificadores numéricos:** a fórmula exibida não mostra conversão dos IDs em categorias. Códigos de produto e canal não devem receber uma interpretação quantitativa sem justificativa.
- **Seleção por correlação:** baixa correlação linear de um identificador numérico não demonstra ausência de informação preditiva.
- **Tratamento de extremos:** os limites por semana precisam de justificativa e análise de sensibilidade; valores altos podem ser eventos reais de demanda.
- **Comparação de modelos:** não há baseline nem comparação de algoritmos documentados.
- **Reprodutibilidade:** faltam scripts executáveis, versões dos pacotes e registro do ambiente. A linha de ajuste do modelo aparece cortada no PDF, impedindo sua recuperação integral por simples transcrição.
- **Validação:** há uma única semana de avaliação; faltam janelas temporais adicionais e análise de erros por segmento.

## Como consultar e reproduzir

**Para consultar:** abra o [relatório original](Projeto2.pdf); não é necessário instalar R.

**Para executar:** a reprodução integral ainda depende da recuperação dos arquivos originais `.R` ou `.Rmd` e do ambiente utilizado. Não há comando de treinamento disponível nesta versão.

O plano de evolução está em **[docs/ROADMAP.md](docs/ROADMAP.md)**.

## Estrutura atual

```text
.
├── README.md          # Apresentação, metodologia e limitações
├── Projeto2.pdf       # Relatório original de 2020
└── docs/
    └── ROADMAP.md     # Pendências para reprodução e evolução
```

## Autoria e referências

- **Thiago Barral** — [GitHub](https://github.com/thiagobarral) · [LinkedIn](https://www.linkedin.com/in/thiago-barral-data-expert)
- Projeto desenvolvido como avaliação da formação de Cientista de Dados da **Data Science Academy**.
- Dados e contexto: [competição Grupo Bimbo Inventory Demand](https://www.kaggle.com/c/grupo-bimbo-inventory-demand).

O repositório ainda não declara uma licença de código. As condições dos dados devem ser consultadas separadamente na fonte.
