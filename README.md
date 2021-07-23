# Data-Analysis

![dataanalytics_1193397784](https://cio.com.br/wp-content/uploads/2018/05/dataanalytics_1193397784.jpg)

# <span style="color:blue">MINICURSO ANÁLISE DE DADOS COM PYTHON</span>

# <span style="color:blue">Desafio:</span>
### <span style="color:blue">Você trabalha em uma grande empresa de cartão de crédito e o diretor da empresa percebeu que o número de clientes que cancelam seus cartões tem aumentado significativamente, causando prejuízos enormes para a empresa.</span>
- O que fazer para evitar isso ? 
- Como saber quais pessoas têm maior tendência a cancelar o cartão ?

# <span style="color:blue">O que temos a nossa disposição:</span>

- Temos 1 base de dados com informações dos clientes, tanto clientes atuais quanto clientes que cancelaram o cartão;
  
# <spam style="color:blue">Referências:</spam>
- Kaggle: 
  (https://www.kaggle.com/sakshigoyal7credit-card-customers)
- MINICURSO ANÁLISE DE DADOS COM PYTHON - Instrutor Lira (https://pages.hashtagtreinamentos.com/minicurso-analisededados-python?blog=1n4033rer&video=3dep762tr)
- Instrutor Lira - Canal Hashtag Programação (https://www.youtube.com/channel/UCafFexaRoRylOKdzGBU6Pgg)


# <spam style="color:blue">Tecnologias utilizadas:</spam>

- Fedora 34 (https://getfedora.org/)
- Anaconda (https://www.anaconda.com/)
- Jupyter Notebook (https://jupyter.org/)

# <span style="color:blue">Passos:</span>

- Passo 1 - Importar a base de dados
- Passo 2 - Visualizar e tratar essa base de dados
- Passo 3 - Analisar, olhar sua base de dados
- Passo 4 - Construir uma análise para identificar o motivo pelo qual os clientes estão cancelando o cartão de crédito

# <span style="color:blue">Codificação:</span>

## <span style="color:blue">Primeiro: Importando a base de dados.</span>
~~~python

'''
Função (encoding) - Trata a saída para conseguir ler as características da língua,
como acentos. No caso (latin1), refere-se a língua Portuguesa
''' 
import pandas as pd
tabela_dados = pd.read_csv('ClientesBanco.csv', encoding = 'latin1')
display(tabela_dados)

~~~

## <span style="color:blue">Segundo: Tratando a base de dados.</span>

~~~python
''' 
Tratando a base de dados
Comando para excluir coluna obsoleta -> tabela_dados = tabela_dados.drop('CLIENTNUM', axis=1)
OBS: (axis) = 1 -> Exclui coluna, neste caso a coluna (CLIENTNUM) / igual a 2 -> Exclui linha
'''
tabela_dados = tabela_dados.drop('CLIENTNUM', axis=1)
display(tabela_dados)

~~~
## <span style="color:blue">2.1: Procurar por informações vazias na base de dados.</span>

~~~python
'''
Procurar por informações vazias na base de dados
'''
display(tabela_dados.info())

~~~

## <span style="color:blue">2.2: Tratando as informações vazias.</span>

~~~python
'''
Na análise anterior a categoria Cartão, possui uma linha faltando, ou seja, um valor faltando,
como falta uma linha dentro de dez mil linhas, a solução é excluir essa linha, pois ela irá a-
penas atrapalhar a análise.

Codigo que vai excluir todas as linhas, que tenham pelo menos um valor vazio
agora todas as categorias possuirão 10126 linhas, pois só uma linha está fal-
tando em uma categoria (categoria Cartão)
'''
tabela_dados = tabela_dados.dropna()
display(tabela_dados.info())
~~~

## <span style="color:blue">2.3: Descrição de algumas informações da base de dados.</span>

~~~python
'''
Agora vamos descrever algumas informações da tabela, como por exemplo, média de idade, como
é que estão distribuídos os dependentes, número máximo, número mínimo de dependentes, dentre
outras informções.

count -> Quantidade de itens (Linhas)
mean -> Média
std -> Desvio padrão
min -> Mínimo
max -> Máximo
Exemplo: Na coluna (idade)
count -> Possui 10126 itens
mean -> Diz que a média dos clientes possui 46 anos ou menos
std -> Desvio padrão da amostra da coluna
min -> Idade mínima de 26 anos
25% -> Diz que 25% dos clientes possui de 41 anos a baixo
50% -> Diz que 50% dos clientes possui de 46 anos a baixo
72% -> Diz que 72% dos clientes possui de 52 anos a baixo
max -> Idade máxima de 73 anos

1 - describe -> Méto da bilioteca Pandas, que faz toda essa análise descritiva
2 - OBS -> Funciona APENAS com colunas com números (int ou float)
3 - A função (round) delimita quantas casas decimais aparecerão depois da vígula
'''
display(tabela_dados.describe().round(1))

~~~

# <span style="color:blue">Terceiro: Análise da base de dados.</span>

## <span style="color:blue">3.1: Análise de quantos clientes permanecem com o cartão e quantos cancelaram o cartão.</span>

~~~python
'''
Avaliação de quantos clientes continuam com cartão e quantos cancelaram o cartão
1 - Selecionar a coluna, neste caso a coluna (Categoria)
2 - Contar os valores da coluna, no caso da coluna (Categoria), quantos são clientes,
    quantos cancelaram, ou seja, não sao mais clientes; par isso usa-se a função do 
    pandas (value_counts())
3 - Mostrar o perentual, utilisa-se a função do pandas (normalize = True), ela mostra-
    rá o quanto do todo equivale aquele valor da coluna (cliente / cancelado)
'''
quant_por_categoria = tabela_dados['Categoria'].value_counts()
display(quant_por_categoria)

quant_por_categoria_perc = tabela_dados['Categoria'].value_counts(normalize = True).round(2)
display(quant_por_categoria_perc)
~~~

## <span style="color:blue">3.2: Descobrir o motivo dos cancelamentos.</span>

~~~python
'''
DESCOBRIR O MOTIVO DOS CANCELAMENTOS!!!!
Dentre as várias formas utilizaremos essa:
Observar a comparação entre clientes e cancelados em cada uma das colunas, para ver
se essa informação retorna algum insight novo.
Para isso vamos exibir as informações em um gŕafico, vamos importar a biblioteca do pyhton
(plotly)e sua ferramenta (express). Para isso, primeiro no jupyter notebook temos que insta-
lar essa biblioteca, com o seguinte comando: !pip3 install --upgrade plotly
'''
import plotly.express as px
grafico_quant_por_categoria = px.histogram(tabela_dados, x = 'Idade', color = 'Categoria')
grafico_quant_por_categoria.show()
~~~

## <span style="color:blue">3.3: Análise de todas as colunas, sempre comparando clientes e não clientes.</span>

~~~python
'''
1 - Para cada coluna dentro da tabela de dados
2 - 'coluna' -> Variável criada pelo programador, poderia ser qualquer nome, é nela que ficará armazenada as colunas;
3 - 'tabela_dados' -> Variável criada pelo programador para receber os valores da tabela.
4 - Comando que mostrará apenas os nomes das colunas da base de dados.
'''
for coluna in tabela_dados:
    print(coluna)
~~~

## <span style="color:blue">3.4: Gráficos de todas as colunas da tabela.</span>

~~~python
'''
 Agora vamos analisar todas as colunas, com a mesma premiça, clientes e não clientes,
 ou seja, os que permanecem clientes e os que cancelaram o serviço, o cartão.
 Para isso utilisa-se a estrutura (FOR).
 OBS -> Toda vez que se faz um (for) dentro de uma tabela ele percorrerá APENAS as co-
 lunas. 
        Para o (for) percorrer as linhas tem que usar o (.index). Exemplo:
        for linha in tabela.index:

- Para cada coluna dentro da tabela de dados
- 'coluna' -> Variável criada pelo programador, poderia ser qualquer nome, é nela que ficará armazenada as colunas
- 'tabela_dados' -> Variável criada pelo programador para receber os valores da tabela
'''
for coluna in tabela_dados:
    grafico_quant_por_categoria = px.histogram(tabela_dados, x = coluna, color = 'Categoria')
    grafico_quant_por_categoria.show()
~~~

## <span style="color:blue">3.5: Deletando os gráficos de colunas que não geram informações úteis.</span>

~~~python
'''
Tratando a base de dados
Comando para excluir coluna obsoleta -> tabela_dados = tabela_dados.drop('CLIENTNUM', axis=1)
OBS: (axis) = 1 -> Exclui coluna / igual a 2 -> Exclui linha
Colunas excluídas que não geram gráficos úteis
'''
tabela_dados = tabela_dados.drop(['Idade', 'Educação', 'Estado Civil', 'Faixa Salarial Anual','Meses como Cliente'], axis=1)
tabela_dados = tabela_dados.drop(['Inatividade 12m', 'Limite', 'Limite Consumido', 'Mudanças Transacoes_Q4_Q1'], axis=1)
tabela_dados = tabela_dados.drop(['Mudança Qtde Transações_Q4_Q1', 'Sexo', 'Dependentes', 'Limite Disponível', 'Taxa de Utilização Cartão'], axis=1)
display(tabela_dados)

~~~

## <span style="color:blue">3.6: Gerando gráficos úteis.</span>

~~~python
for coluna in tabela_dados:
    grafico_quant_por_categoria = px.histogram(tabela_dados, x = coluna, color = 'Categoria')
    grafico_quant_por_categoria.show()
~~~

# <span style="color:blue">Quarto: Motivos que explicam os cancelamentos do produto pelos clientes à partir da análise dos gráficos.</span>

   - Me parece que quanto mais produtos contratados um cliente possui, menor a chance dele cancelar o produto;
   - Quanto mais transações e quanto maior seu valor, menor a chance do cliente cancelar o produto;
   - Quanto maior a quantidades de contatos, maior a chance do cliente cancelar o produto.
