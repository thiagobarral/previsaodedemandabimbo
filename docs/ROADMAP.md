# Plano de evolução

Este documento separa as pendências do estudo histórico de uma futura implementação de previsão. As tarefas abaixo ainda não foram executadas.

## 1. Recuperar a execução original

- [ ] Recuperar os arquivos originais `.R` ou `.Rmd`, incluindo a chamada completa de ajuste.
- [ ] Registrar a versão de R, os pacotes e a saída de `sessionInfo()`, caso disponíveis.
- [ ] Confirmar o pacote que fornece `bigglm` e suas dependências no ambiente recuperado.
- [ ] Retirar caminhos locais fixos e documentar entradas, saídas e requisitos de memória.
- [ ] Preservar o PDF como relatório histórico e identificar qualquer reconstrução como uma nova implementação.

**Critério de conclusão:** outra pessoa consegue executar o fluxo documentado a partir dos dados autorizados e entender eventuais diferenças em relação ao resultado de 2020.

## 2. Definir uma previsão válida

- [ ] Definir o instante da decisão, o horizonte e a unidade de previsão, por exemplo cliente × produto × semana.
- [ ] Confirmar quais colunas existem no conjunto de teste da competição e quando cada informação fica disponível.
- [ ] Remover entradas indisponíveis no instante da previsão.
- [ ] Construir defasagens e agregações históricas usando somente semanas anteriores à semana prevista.
- [ ] Manter IDs necessários para formar históricos e tratar categorias novas com regras explícitas.
- [ ] Ajustar transformações somente no treino, preservando a separação temporal.

**Critério de conclusão:** nenhuma previsão utiliza vendas, devoluções ou demanda conhecidas apenas após o instante da decisão.

## 3. Comparar e validar

- [ ] Implementar uma referência simples com histórico disponível, como a demanda da última semana observada.
- [ ] Definir uma alternativa para clientes ou produtos sem histórico.
- [ ] Usar validação em janelas temporais sucessivas e reservar uma janela final.
- [ ] Comparar candidatos e baseline nas mesmas observações, com o mesmo protocolo.
- [ ] Medir RMSLE e analisar erros por produto, canal e faixa de demanda.
- [ ] Verificar a influência dos extremos e a necessidade de qualquer exclusão.
- [ ] Registrar parâmetros, volume de dados e resultados efetivamente calculados.

**Critério de conclusão:** os resultados são reproduzíveis, comparáveis e apresentados com seu período de avaliação e limitações.

## 4. Consolidar o portfólio

- [ ] Versionar código executável e instruções conferidas em ambiente limpo.
- [ ] Registrar dependências verificadas, por exemplo com `renv`.
- [ ] Adicionar verificações para cálculo da métrica e construção temporal das variáveis.
- [ ] Publicar gráficos e uma tabela de resultados gerados pela execução.
- [ ] Decidir a licença do código considerando a autoria e as condições dos materiais utilizados.
- [ ] Atualizar o README somente com funcionalidades e resultados comprovados.

A nova avaliação deve ser apresentada separadamente do RMSLE histórico de 0,0586998, pois a remoção de entradas indisponíveis altera o experimento.
