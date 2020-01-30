# Previsão de demanda Grupo Bimbo

O Grupo Bimbo (https://www.grupobimbo.com), se esforça para atender a demanda diária dos consumidores por produtos frescos de panificação nas prateleiras de mais de 1 milhão de lojas ao longo das suas 45.000 lojas em todo o México.
Atualmente, os cálculos diários de estoque são realizados por funcionários de vendas de entregas diretas, que devem, sozinhos, prever a necessidade de estoque dos produtos e demanda com base em suas experiências pessoais em cada loja. Como alguns pães têm uma vida útil de uma semana, a margem aceitável para o erro é pequena.
Neste projeto de aprendizado de máquina, eu desenvolvi um modelo para prever a demanda de estoque com base nos dados
históricos de vendas. Isso fará com que os consumidores dos mais de 100 produtos de panificação não fiquem olhando para as prateleiras vazias, além de reduzir o valor gasto com reembolsos para os proprietários de lojas com produtos
excedentes impróprios para venda. Para a construção desse projeto, utilizei a linguagem
R e os datasets disponíveis no Kaggle em: https://www.kaggle.com/c/grupo-bimbo-inventory-demand
A avaliação se deu por meio do Root Mean Squared Logarithmic Error (RMSLE).

Esse projeto foi realizado como avaliação para o curso de formação de cientista de dados da Data Science Academy.

Dicionário:
Semana — Week number (From Thursday to Wednesday)
Agencia_ID — Sales Depot ID
Canal_ID — Sales Channel ID
Ruta_SAK — Route ID (Several routes = Sales Depot)
Cliente_ID — Client ID
NombreCliente — Client name
Producto_ID — Product ID
NombreProducto — Product Name
Venta_uni_hoy — Sales unit this week (integer)
Venta_hoy — Sales this week (unit: pesos)
Dev_uni_proxima — Returns unit next week (integer)
Dev_proxima — Returns next week (unit: pesos)
Demanda_uni_equil — Adjusted Demand (integer) (This is the target you will predict)

The evaluation metric for this competition is Root Mean Squared Logarithmic Error.
