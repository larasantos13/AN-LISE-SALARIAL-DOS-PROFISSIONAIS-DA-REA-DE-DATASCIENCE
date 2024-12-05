# DASHBOARD

1. Cálculo da Média Salarial (media_salarial_usd)

    media_salarial_usd = data['salary_in_usd'].mean()
	
Objetivo: Calcular a média dos salários em dólares americanos (salary_in_usd). A média salarial é uma métrica importante para avaliar o valor médio pago aos profissionais de ciência de dados em dólares. Esse valor é útil para a análise geral de salários no mercado, além de servir de referência para outros cálculos, como a faixa salarial.

2. Cálculo da Faixa Salarial (faixa_salarial)
   
  faixa_salarial = 'Baixo' if media_salarial_usd <= 50000 else ('Médio' if media_salarial_usd <= 100000 else 'Alto')

Objetivo: Classificar a média salarial em três faixas: "Baixo", "Médio" ou "Alto".
   Este cálculo permite categorizar a média salarial e facilitar a visualização para o usuário. Dependendo da faixa salarial, o dashboard pode fornecer insights sobre o mercado de trabalho em termos de remuneração. 
  	Baixo: Salários até 50.000 USD.
  	Médio: Salários entre 50.000 e 100.000 USD.
  	Alto: Salários acima de 100.000 USD.


3. Cálculo do Total de Funcionários (total_funcionarios)

   total_funcionarios = data.shape[0]

Objetivo: Calcular o total de funcionários na base de dados. O número total de funcionários é uma métrica chave para entender a amplitude dos dados e fornecer uma visão geral do tamanho do mercado de trabalho. Esse número também pode ser usado como referência para calcular a distribuição de funcionários em outras métricas.

4. Agrupamentos para Gráficos e Tabelas

4.1 Média Salarial por Localização (media_salarial_por_local)

  media_salarial_por_local = data.groupby('company_location')['salary_in_usd'].mean().reset_index()

Objetivo: Calcular a média salarial por localização de empresa (ex.: cidades ou países). A média salarial por localização ajuda a identificar quais regiões pagam mais ou menos, o que pode ser crucial para profissionais que desejam se mover para uma região com salários mais altos. Isso também fornece insights sobre como as localizaçõeafetam o mercado de trabalho e a competitividade dos salários.

4.2 Média Salarial por Tipo de Contrato (media_salarial_por_contrato)
  
  media_salarial_por_contrato = data.groupby('employment_type')['salary_in_usd'].mean().reset_index()

Objetivo: Calcular a média salarial por tipo de contrato (ex.: tempo integral, tempo parcial, contrato temporário). Diferentes tipos de contrato podem oferecer diferentes níveis salariais. Contratos permanentes (full-time) geralmente oferecem salários mais altos e benefícios melhores, enquanto contratos temporários podem ser mais baixos. Este cálculo permite comparar essas diferenças.

4.3 Média Salarial por Nível de Experiência (media_salarial_por_experiencia)
  
  media_salarial_por_experiencia = data.groupby('experience_level')['salary_in_usd'].mean().reset_index()

Objetivo: Calcular a média salarial por nível de experiência (ex.: iniciante, intermediário, sênior). Este cálculo mostra como a experiência de um profissional impacta seu salário. Profissionais mais experientes tendem a ganhar mais, então a análise da média salarial por nível de experiência pode fornecer insights sobre as expectativas salariais em diferentes estágios de carreira.


4.4 Contagem de Funcionários por Tipo de Contrato (funcionarios_por_contrato)

  funcionarios_por_contrato = data['employment_type'].value_counts().reset_index()
  funcionarios_por_contrato.columns = ['employment_type','count']

Objetivo: Contabilizar o número de funcionários por tipo de contrato (ex.: tempo integral, tempo parcial, etc.). A distribuição de funcionários por tipo de contrato ajuda a entender o mercado de trabalho em termos de preferências contratuais. Isso pode indicar, por exemplo, se a maioria dos profissionais está em contratos de tempo integral ou se há um aumento no trabalho freelance ou temporário.

4.5 Contagem de Funcionários por Nível de Experiência (funcionarios_por_experiencia)

  funcionarios_por_experiencia = data['experience_level'].value_counts().reset_index()
  funcionarios_por_experiencia.columns = ['experience_level','count']
 
Objetivo: Contabilizar o número de funcionários por nível de experiência. Por que fazer isso: Esse cálculo oferece uma visão sobre a distribuição de funcionários no mercado de trabalho em termos de experiência. Isso ajuda a visualizar se há uma predominância de iniciantes, intermediários ou sêniores nas vagas de ciência de dados.


4.6 Contagem de Funcionários por Tamanho de Empresa (funcionarios_por_tamanho)

  funcionarios_por_tamanho = data['company_size'].value_counts().reset_index()
  funcionarios_por_tamanho.columns = ['company_size','count']

Objetivo: Contabilizar o número de funcionários por tamanho de empresa (ex.: pequeno, médio, grande). Por que fazer isso: O tamanho da empresa pode influenciar tanto o salário quanto o tipo de contrato oferecido. Empresas grandes tendem a oferecer mais benefícios, enquanto empresas pequenas podem ter um ambiente mais flexível ou intimista. Esse cálculo permite entender o perfil das empresas que contratam na área de ciência de dados.


5. Gráfico de Distribuição Salarial (figura_distribuicao_salarial)

    figura_distribuicao_salarial = px.histogram(data,x='salary_in_usd',nbins=30,title="Distribuição Salarial")

Objetivo: Criar um histograma para visualizar a distribuição dos salários no conjunto de dados. A distribuição salarial fornece uma visão detalhada sobre como os salários estão distribuídos na base de dados. Isso ajuda a identificar padrões, como a existência de picos de salários (talvez uma concentração de salários em um valor específico) ou caudas longas, que podem indicar salários muito baixos ou muito altos.

6. Gráficos de Boxplot

Os gráficos de boxplot são utilizados para mostrar a dispersão dos salários em diferentes categorias (localização, nível de experiência e tamanho da empresa):
    figura_boxplot_local = px.box(data,x='company_location',y='salary_in_usd',title="Boxplot Salarial por Localização")
    figura_boxplot_experiencia = px.box(data,x='experience_level',y='salary_in_usd',title="Boxplot Salarial por Nível de Experiência")
    figura_boxplot_tamanho = px.box(data,x='company_size',y='salary_in_usd',title="Boxplot Salarial por Tamanho de Empresa")

Objetivo: Mostrar a variação salarial (mínimo, 1º quartil, mediana, 3º quartil, máximo) dentro de diferentes categorias (localização, experiência, tamanho da empresa). O boxplot é útil para entender a dispersão dos salários e identificar possíveis outliers (salários muito acima ou abaixo da média). Ele fornece uma visão clara das variações salariais em diferentes segmentos.

Dataset utilizado: https://www.kaggle.com/datasets/brsahan/data-science-job
