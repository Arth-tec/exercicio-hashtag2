# 1-importar a base de dados
# plotly -> trabalhar com graficos 
# !pip install pandas numpy openpyxl nbformat ipykernel plotly

 import pandas as pd

 tabela = pd.read_csv("cancelamentos.csv")

# 2-visualizar a base de dados
    #entender quais informaçoes eu tenho disponiveis
    #procurar entender os problemas da base de dados

# colunas inuteis - infromaçoes que nao te ajuda, te atrapalha
 tabela = tabela.drop(columns="CustomerID")

 display(tabela)

# 3-corrigir a base de dados

# informaçoes vazias ou no formato errado

 tabela = tabela.dropna() # nan - not a number - informaçoes vazias (deleta elas)

 display(tabela.info()) # mostra as informaçoes da tabela

# 4- analise dos cancelamentos (quantos cancelaram, quantos nao cancelaram)

 display(tabela["cancelou"].value_counts())

# em porcentagem = normalizado

 display(tabela["cancelou"].value_counts(normalize=True))

# 5- analise da causa dos cancelamentos dos clientes(como as colunas impactam no cancelamento) 
 import plotly.express as px

#para cada coluna da nossa tabela
for coluna in tabela.columns:
    #cria o grafico
    grafico = px.histogram(tabela, x=coluna, color="cancelou")
    #exibe o grafico
    grafico.show()

#causa de cancelamento 

#todos os clientes de contrato mensal, cancelaram
    #vamos dar desconto nos contratos anuais e trimestrais
#todos os clientes com mais de 20 dias de atraso cancaelaram o serviço
    #criar um sistema de cobraça dos clientes que com  10 dias de atraso a gente conversa com ele
#todos os clientes que ligaram mais de 4 vz no call center cancelou
    #criar um alerta para um cliente que ligou mais de 2x para o callcenter

#analisar se eu resolver esses problemas, quanto cai o cancelamento

#duracao do contrato nao pode ser mensal

 tabela = tabela[tabela["duracao_contrato"]!="Monthly"]

#atrasos só podem ser até 20 dias

 tabela = tabela[tabela["dias_atraso"]<=20]

#ligaçoes no call center só pode ser de até 4 ligaçoes

 tabela = tabela[tabela["ligacoes_callcenter"]<=4]


 display(tabela["cancelou"].value_counts(normalize=True))