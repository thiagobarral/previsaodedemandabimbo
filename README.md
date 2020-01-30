# Previsão de demanda Grupo Bimbo

O Grupo Bimbo realizou uma competição através do kaggle para previsão de demanda dos seus produtos no México.
O data set disponibilizado continha algumas informações sobre a venda dos produtos, como descrito abaixo no dicionário dos dados.
No total tinham 9 semanas de dados disponibilizados no data set, então as semanas 3, 4, 5, 6, 7 e 8 foram utilizados como treinamento para o modelo e a semana 9 para teste e avaliaçõa.
A avaliação se deu por meio do Root Mean Squared Logarithmic Error (RMSLE).

Segue abaixo o link com todas as informações da competição e o data set necessário para avaliação.
https://www.kaggle.com/c/grupo-bimbo-inventory-demand

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
