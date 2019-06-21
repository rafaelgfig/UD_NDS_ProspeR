# Explorando e resumindo dados de empréstimos da Prosper por Rafael G. Figueira
------
<p>Esse relatório explora um conjunto de dados de empréstimos da Prosper, possuindo 113.937 empréstimos com 81 variáveis em cada um, incluindo valor, taxa de juros, status do pagamento, receita do mutuário, seu emprego atual, histórico do cartão de crédito, informações sobre seu último pagamento, entre outras.</p>

##### Bibliotecas
* dplyr
* gridExtra
* ggplot2
* tidyr
* purrr
* reshape2
* GGally

##### Carregamento dos dados
df <- read.csv('prosperLoanData.csv')

## Seção de Gráficos Univariados
<p>O conjunto de dados original possui 113937 linhas e 81 colunas.</p>

'''{r Dimensao dos dados}'''

<p>Foram escolhidas 15 variáveis julgadas mais interessantes para a minha análise.<br/> Sendo elas:</p>

* MemberKey
* LoanKey
* Term
* LoanStatus
* BorrowerAPR
* BorrowerRate
* ProsperScore
* ListingCategory..numeric.
* Occupation
* EmploymentStatus
* EmploymentStatusDuration
* StatedMonthlyIncome
* LoanOriginalAmount
* LoanOriginationDate
* MonthlyLoanPayment

Abaixo seguem algumas informações úteis sobre os dados.<br/>

'''{r Tipos dos dados}'''

'''{r Resumo estatistico}'''

<br/>Quantidade de NA's:
'''{r Verificando quantidade de NAs}'''

Visualizando distribuição das variáveis selecionadas.<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histograma_basico_das_colunas-1.png" width="672"><br/>
É possível ver que o histograma da variável *StatedMonthlyIncome* está totalmente concentrado em zero.

Analizando o resumo estatístico é possível ver que a variável contém alguns dados discrepantes.<br/>
'''{r Resumo estatistico StatedMonthlyIncome}'''

Os 10 valores mais altos da variável são:<br/>
'''{r Top 10 StatedMonthlyIncome}'''

Visualizando os dados sem 0.5% dos maiores valores.<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histograma_StatedMonthlyIncome_sem_0.5_porcento-1.png" width="672">

Omitindo 5% dos maiores valores:<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histograma_StatedMonthlyIncome_sem_5_porcento-1.png" width="672">

Nos gráficos abaixo podemos ver que a maioria dos empréstimo possuem valores arredondados, dando ênfase para empréstimos de 4.000, os posteriores tendem a ser múltiplos de 5.000.<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histogramas_LoanOriginalAmount-1.png" width="672">

<p>Abaixo é possível observar que é mais comum encontrar pessoas com poucos meses de emprego solicitando empréstimo do que em comparação com aqueles com muito tempo.</p>

Tempo em meses:<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histograma_EmploymentStatusDuration_sem_5_porcento-1.png" width="672">

Tempo em anos:<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histograma_EmploymentStatusDuration_sem_5_porcento_em_anos-1.png" width="672">

Distribuição dos status do emprego:<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_EmploymentStatus-1.png" width="672"><br/>
'''Porporcao'''<br/>
A grande maioria dos solicitantes de empréstimos está atualmente empregado de alguma forma. Apenas 0.7% dos mutuários são declaradamente desempregados.

O histograma da duração do empréstimo ficou muito espaçado por conta da coluna estar como tipo de valor inteiro, e como só há 3 variações de duração (12, 36 ou 60) dentro dessa coluna, é possível assumí-la como dado categórico e plotar como tal. <br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Alterado_Term_para_categorico_e_plotado-1.png" width="192">

Categorias mais selecionadas pelo mutuário:<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Alterado_ListingCategory_para_categorico_e_plotado-1.png" width="672"><br/>
Legenda das categorias:

0. Não disponível
1. Consolidação da dívida
2. Melhoria da casa
3. Negócios
4. Empréstimo pessoal
5. Uso do aluno
6. Automático
7. Outros 
8. Bebê e Adoção
9. Barco
10. Procedimento Cosmético
11. Anel de Noivado
12. Empréstimos Verdes
13. Gastos Domésticos
14. Grandes Compras
15. Médico / Odontológico
16. Motocicleta
17. VD
18. Impostos
19. Férias
20. Empréstimos do casamento


Distribuição das ocupações declaradas: <br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_Occupation-1.png" width="672"><br/>
A grande maioria declarou como "Outra" a ocupação ou declarou apenas como ocupação profissional, não sendo possível afirmar corretamente qual a ocupação mais comum. Das ocupações especificamente declaradas o programador de computador ficou em destaque.<br/>

Distribuição dos valores das parcelas:<br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Histogramas_MonthlyLoanPayment-1.png" width="672"><br/>
Vemos uma frequência altíssima de mutuários com valor de parcela próximo da casa dos 175, mas pelo gráfico não é possível ter muita precisão, por mais que seja determinado 1 de binwidth.

'''{r Top 3 MonthlyLoanPayment}'''<br/>
'''{r Proporcao}'''<br/>
Verificado que 2423 parcelas de mutuários têm exatamente 173.71 como valor. Representando 2.13% de todos os dados.

'''{r Resumo estatistico das parcelas 173.71}'''<br/>
Todos aqueles que solicitaram empréstimo de 4.000 para ser pago em 36 meses com APR de 0.358 tem o mesmo valor de parcela.<br/>
Foi verificado anteiormente que o valor mais solicitado é de 4.000 e a duração mais popular também é a de 36 meses, justificando a concentração anormal do valor da parcela com essa APR.

Foi verificado também alguns empréstimos com pagamento mensal programado com valor zerado, podendo ser erro no conjunto de dados ou existe a possibilidade do mutuário simplesmente não programar um valor para o pagamento mensal, obtendo assim o valor zero.<br/>
Nesse caso foi considerado a segunda possibilidade e os dados foram mantidos.<br/>
'''{r Resumo estatistico das parcelas 0}'''

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Alterado_LoanOriginationDate_para_data_e_plotado-1.png" width="672"><br/>
Ocorreu um aumento considerável de empréstimo a partir de 2013 e por alguma razão não há registros no começo de 2009 e final de 2008.

# Análise Univariada

### Qual é a estrutura do conjunto de dados?
São 113.937 empréstimos com 81 variáveis em cada um.<br/>
Visando uma exploração mais sucinta, foram escolhidas 15 variáveis de interesse, sendo elas:

* Duas variáveis identificadoras (MemberKey e LoanKey);
* Sete variáveis numéricas (BorrowerAPR, BorrowerRate, ProsperScore, EmploymentStatusDuration, StatedMonthlyIncome, LoanOriginalAmount e MonthlyLoanPayment);
* Uma variável cronológica (LoanOriginationDate);
* E cinco variáveis categóricas (Term, LoanStatus, ListingCategory..numeric., Occupation e EmploymentStatus)

A variável *ListingCategory..numeric.* está representada numéricamente, com a seguinte relação:

0. Não disponível
1. Consolidação da dívida
2. Melhoria da casa
3. Negócios
4. Empréstimo pessoal
5. Uso do aluno
6. Automático
7. Outros 
8. Bebê e Adoção
9. Barco
10. Procedimento Cosmético
11. Anel de Noivado
12. Empréstimos Verdes
13. Gastos Domésticos
14. Grandes Compras
15. Médico / Odontológico
16. Motocicleta
17. VD
18. Impostos
19. Férias
20. Empréstimos do casamento

Outras observações:

* A maioria dos empréstimos solicitados são de menos de 12000.
* Menos de 0.5% dos mutuários têm renda mensal acima de 25000, o mais comum é ganharem de 3200 a 6800.
* Normalmente os valores solicitados são múltiplos de 5000, com exceção aos empréstimos de 4000 que são os mais numerosos.
* Existem mutuários empregados por mais de 62 anos e os que não estão empregados. Em média estão 8 anos empregados.
* Apenas 0.7% dos mutuários são declaradamente desempregados.
* A duração do empréstimo mais solicitada é de 36 meses, em seguida de 60 meses e muito raramente 12 meses.
* Não há registros de empréstimos no final de 2008 e começo de 2009.

### Quais são os principais atributos de interesse deste conjunto de dados?
Os principais atributos de interesse são o montante original do empréstimo, renda declarada e razão pela qual solicitou o empréstimo. Quero entender quais são os perfís mais comuns de mutuários e suas motivações para solicitar os respectivos valores. Imagino que há uma correlação positiva de valor solicitado com a renda declarada ou talvez tempo de serviço.

### Quais outros atributos você acha que podem lhe auxiliar na investigação destes atributos de interesse?
Acho que todos os atributos selecionados apresentam certa importância, talvez as taxas de juros nem tanto, mas os demais certamente possuem valor para a análise, por conta disso que foram selecionados dentre os 81 possíveis.

### Você criou novas variáveis a partir dos atributos existentes no conjunto de dados?
Realizei apenas a criação de faixas de renda para conseguir expressar categoricamente as rendas dos mutuários.

### Dos atributos investigados, distribuições incomuns foram encontradas? Você aplicou operações nos dados para limpá-los, ajustá-los ou mudar a forma dos dados? Se sim, por quê?
As distribuições das variáveis _EmploymentStatusDuration_, _MonthlyLoanPayment_ e _StatedMonthlyIncome_ são assimétricas positivas com longas caudas.

Para _StatedMonthlyIncome_ só foram omitidos os valores mais altos (0.5% à 5%) para que a distribuição ficasse mais normal. Na análise bivariada foram removidos os 0.5% por distorcer muito as correlações e dispersões.

A _MonthlyLoanPayment_ mesmo omitido os valores mais altos ainda continua bastante assimétrica, ainda assim não achei necessário redimenssioná-la, já que estava interessado em ver a concentração incomum dos dados próximos ao 175.

Já _EmploymentStatusDuration_ é uma distribuição totalmente assimétrica positivamente. Com uma escala logarítmica ou de raiz ela normalizaria, mas não julguei necessário normalizá-la, apenas omiti 5% dos maiores valores para conseguir visualizar melhor os dados, e por ser um dado de tempo preferi que cada coluna representasse 1 mês ou 1 ano.

Na _ListingCategory_ há uma grande concentração dos dados da categoria 1, seguida da 0 e 7, ficando muito assimétrica a direita. Nessa distribuição foi usada uma escala logarítmica com base 10 no eixo _Y_ para visualizar melhor os dados. Por mais que eles tenham se aproximado, a distribuição ainda segue assimétrica, uma vez que foi escalonado o eixo _Y_ e não o _X_, já que está sendo contado os dados categóricos e não numéricos de fato.

Os dados da _LoanOriginationDate_ criam duas distribuições assimétricas negativamente por conta de terem dados faltantes em certo período, ainda que houvessem esses dados a distribuição certamente permaneceria assimétrica para a esquerda. Nesse caso também não foi escalonado por se tratar de dados cronológicos, então preferi manter a escala normal para visualizar melhor.

# Seção de Gráficos Bivariados
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Removido_0.5_porcento_do_StatedMonthlyIncome_e_criado_heatmap_de_corr-1.png" width="672">

Vemos que a *taxa APR* se relaciona com as demais colunas, salvo o *tempo empregado*. Ao que tudo indica, quanto maior o *Score*, menores são as *taxas APR*, e o mesmo ocorre com o *valor original do empréstimo*.

Assim como a *taxa APR*, o *Score* se relaciona com as demais, salvo o *tempo empregado*, mas no caso do *Score*, apenas a relação com a *taxa APR* que é negativa, o restante é positiva, por mais que sejam fracas, possivelmente uma é usada para a criação da outra.

O *valor original do empréstimo* tem forte relação com o *valor pago mensalmente*, uma vez que quanto maior o valor solicitado, maior será o valor da parcela, uma é praticamente derivada da outra.

Por fim o *tempo empregado* não se relaciona com praticamente nenhum das demais, apenas possuindo uma relação muito fraca com a *renda declarada*.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Pairsplot_das_variaveis_numericas-1.png" width="1152"><br/>
Os gráficos de dispersão estão em geral bem poluídos, menos do valor original do empréstimo com o valor pago mensalmente por terem forte correlação.<br/> É necessário olhar mais de perto para tentar entender as relações.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Densidade_LoanOriginalAmount_por_Score-1.png" width="1152"><br/>

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_LoanOriginalAmount_por_Score-1.png" width="1152"><br/>
Com os gráficos de densidade e boxplot é possível ver com mais clareza a relação do Score com o valor original do empréstimo. <br/>
Mutuários com pouca pontuação dificilmente conseguem solicitar empréstimos com valores mais altos, se concentrando nos valores mais baixos, na medida que a pontuação aumenta, a distribuição fica mais uniforme, indicando que mutuários com alto Score conseguem solicitar com mais facilidade valores altos. Por mais que o valor mediano oscile, é possível observar que a maioria dos valores solicitados cresce junto ao Score.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_LoanOriginalAmount_por_EmploymentStatus-1.png" width="1152"><br/>
Como esperado pessoas empregadas tendem a ter maiores valores de empréstimo, já as aposentadas, desempregadas, não declaradas e que trabalham parcialmente, tendem a ter empréstimos menores.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Dispersao_LoanOriginalAmount_por_BorrowerAPR-1.png" width="672"><br/>
Empréstimos mais altos normalmente tem taxa APR menor, acho que ninguém quer pedir um valor alto com altas taxas ainda.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Dispersao_ProsperScore_por_BorrowerAPR-1.png" width="672"><br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_ProsperScore_por_BorrowerAPR-1.png" width="672"><br/>
A correlação entre a taxa APR e o Score fica clara no boxplot, mutuários com baixa pontuação precisam de taxas maiores para compensar o risco do empréstimo, o que não ocorre com quem tem alta pontuação, obtendo assim as melhores taxas.  

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Dispersao_StatedMonthlyIncome_por_LoanOriginalAmount-1.png" width="672">

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_StatedMonthlyIncome_por_LoanOriginalAmount-1.png" width="1152">

'''Resumo_estatistico_StatedMonthlyIncome_por_LoanOriginalAmount-1.png'''<br/>
Com o gráfico de dispersão é possível ver a correlação entre a renda declarada e o valor do empréstimo, mas ainda é muito poluido, por conta disso optei pelo boxplot com fatiamento de 2.500 das rendas, assim ficou muito mais claro a relação das duas e como rendas baixas de fato têm em sua maioria empréstimos menores.

Através dos resumos estatísticos observamos que rendas inferiores à 7.500 realizaram empréstimos de no máximo 25.000. A média também vai aumentando gradativamente conforme a renda sobe, demonstrando assim a relação entre as duas variáveis.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_EmploymentStatusDuration_por_StatedMonthlyIncome-1.png" width="672"><br/>
Achei que houvesse uma leve correlação entre o tempo de serviço e a renda mensal, mas vendo a dispersão desses dados não parece haver. <br/>
A correlação de Pearson entre as duas variáveis resultou em 0.11, o que já seria bem fraco, agora com o gráfico é visível que o tempo de serviço não se relaciona com ela.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_ListingCategory..numeric._por_LoanOriginalAmount_COUNT-1.png" width="1152"><br/>
Vemos que algumas categorias contêm empréstimos menores do que outras, como por exemplo a 13 (gastos domésticos) em comparação com a 1 (consolidação de dívida). Empréstimos com procedimentos cosméticos (número 10) além de serem poucos, não ultrapassam 15 mil.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_Occupation_por_LoanOriginalAmount-1.png" width="576">

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_Occupation_por_StatedMonthlyIncome-1.png" width="576"><br/>
Fiquei curioso quanto a distribuição de salários e valor do empréstimo solicitado das profissões declaradas.<br/>
Como demonstrado acima, pessoas que ganham mais tendem a solicitar um valor maior de empréstimo, e agora podemos ver também que estudantes normalmente são os que têm as menores rendas mensais e consequentemente os menores empréstimos.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Dispersao_LoanOriginationDate_por_LoanOriginalAmount-1.png" width="672"><br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Diespersao_LoanOriginationDate_por_LoanOriginalAmount_c_corte_alto-1.png" width="672"><br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Dispersao_LoanOriginationDate_por_LoanOriginalAmount_c_corte_baixo-1.png" width="672"><br/>
Vemos que o tempo não é um fator determinante para o valor do empréstimo, todavia, a partir de 2011 não foram mais realizados empréstimos menores que 2000, e somente depois de 2013 que foram realizados empréstimos acima de 25000.<br/> 
É interessante visualizar as linhas horizontais, demonstrando que realizam mais empréstimos com valores redondos do que quebrados, nesse caso sendo mais comum de 500 em 500. <br>
Além disso ainda é ver novamente o período curiosiamente sem empréstimos.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_LoanOriginalAmount_por_Term-1.png" width="672"><br/>
Por último um boxplot da quantidade de parcelas com o valor solicitado para confirmar que mais parcelas são para os empréstimos maiores e o inverso para empréstimos menores.

# Análise Bivariada

### Discuta sobre alguns dos relacionamentos observados nesta parte da investigação. Como os atributos de interesse variaram no conjunto de dados?
Um dos pontos mais importante - se não o mais importante - é a pontuaçao do mutuário. Mutuários com alta pontuação conseguem empréstimos com menores juros, e menores juros possibilitam empréstimos maiores.

Pessoas com rendas maiores tendem a ter empréstimos maiores, assim como pessoas desempregadas, apostentadas ou com trabalho parcial tendem a ter empréstimos menores, isso é algo intuitivo, mas que se mostrou ser verdade através da análise gráfica.

Os estudantes são os que conseguem os menores empréstimos, porque também são os que têm as menores rendas. Vida de estudante não é fácil.

Existe um furo nos dados ao redor do começo de 2009 em que não foram realizados empréstimos, mas não sei se é um erro dos dados ou um período sem operação da empresa. Ademais, a partir de 2011 a Prosper não realizou mais empréstimos abaixo de 2.000 e foi só depois de 2013 que foram realizados empréstimos acima de 25.000, talvez a demanda tenha sido grande a ponto deles possibilitarem tais valores.

Achava que o tempo empregado iria se relacionar com alguma outra variável, mas analisando graficamente e pela correlação de pearson, o tempo de serviço não tem peso para entender os perfis dos mutuários.

### Você observou algum relacionamento interessante entre os outros atributos (os que não são de interesse)?
Não tinha tanto interesse nas taxas do empréstimo, mas foi demonstrado que ela se relaciona bem com as outras variáveis, o que faz sentido, uma vez que os mutuários não vão solicitar grandes empréstimos com altas taxas, a tendencia é que se tiverem boas taxas eles vão solicitar valores maiores.

### Qual foi o relacionamento mais forte encontrado?
O relacionamento mais forte - tirando é claro o valor das parcelas com o valor do empréstimo - foi o da pontuação com as taxas APR. Entendo que pessoas com baixa pontuação são um investimento mais arriscado, o que acaba elevando as taxas para compensar o risco, o que não ocorre com pessoas de alta pontuação. Pessoas com 11 de pontuação conseguem empréstimos com taxas de 0.1, enquanto que os que tem 1 de pontuação conseguem empréstimos na faixa de 0.35 de taxa.

# Seção de Gráficos Multivariados

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_LoanAmount_APR_e_Score-1.png" width="960"><br/>
Podemos ver a distribuição do Score baixo nas taxas mais altas, enquanto que no eixo do valor isso não ocorre, mas na medida que os juros ficam mais altos, o valor tende a diminuir.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_LoanAmount_APR_e_MonthlyIncome-1.png" width="960"><br/>
Interessante visualizar que pessoas com rendas altas não necessariamente solicitam empréstimos altos, mas as com rendas baixas certamente não solicitam altos empréstimos.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_LoanDate_LoanAmount_e_Score-1.png" width="960"><br/>
Aqui temos um gráfico curioso que mostra o período em que foi implementado o sistema de Score, talvez essa lacuna seja o intervalo necessário para implementar o novo mecanismo. É possível ver um pequeno ajuste do algorítmo em relação as pontuações,os scores mais baixos se concentraram na parte mais baixa.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_LoanDate_APR_e_Score-1.png" width="960"><br/>
Nesse gráfico ficou claro os ajustes do sistema de pontuação. No começo houveram poucas pontuações baixas, mas com o passar do tempo ele foi ajustando, até mesmo ocorrendo saltos maiores de taxas. 

Um exemplo disso são as linhas horizontais na mesma cor de Score. Esse provavelmente foi o período que mais se basearam no score para estimar as taxas. <br/>
Depois o algorítmo ficou mais uniforme, sem grandes saltos, só que ainda assim é evidente que pontuações baixas possuem maiores taxas.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Densidade_LoanOriginalAmount_StatedMonthlyIncome_e_EmploymentStatus-1.png" width="960"><br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_LoanOriginalAmount_StatedMonthlyIncome_e_EmploymentStatus-1.png" width="960"><br/>
Intuitivamente o gráfico mostra - apesar de muito poluido - que mutuários normalmente possuem rendas altas e grandes empréstimos quando estão empregados, seja o tempo todo ou meio período. Ainda assim vemos que mutuários com baixa renda ainda conseguem realizar empréstimos relativamente alto, obtendo um gráfico de densidade mais uniforme do que em comparação com o das rendas.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Facet_LoanOriginalAmount_StatedMonthlyIncome_EmploymentStatus_e_Score-1.png" width="1152"><br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Distribuicao_LoanDate_LoanAmount_e_EmploymentStatus-1.png" width="960"><br/>
Com o gráfico dividido em score dá pra ver que existem muitos casos sem Score. Como já tinha visto anteriormente que o Score foi implementado após a lacuna, decidi ver como está distribuido os status do emprego ao longo do tempo. Para minha surpresa vi que houve período sem categoria, outro indisponível e depois o uso do termo "Full-time" que posteriormente foi substituido pelo "Employed". O termo "Other" também parece ter sido utilizado de fato só após 2011.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Densidade_LoanOriginalAmount_StatedMonthlyIncome_e_ListingCategory-1.png" width="960"><br/>
A linha 5 está mais a esquerda do que as demais, o que faz sentido uma vez que corresponda aos empréstimos dos estudantes - anteriormente verificados como menores rendas -, os valores dos empréstimos dessa categoria também estão concentrados nos valores mais baixos, não seguindo a tendencia das outras categorias. Mais uma vez vemos a tendencia dos dados demonstrando que vida de estudante não é fácil.<br/>
A linha 1 (consolidação de dívida) segue sobressalente no gráfico de valor do empréstimos, pois é a categoria mais popular para empréstimos altos, com a concentração nos valores redondos.

<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_APR_StatedMonthlyIncome.bucket_e_Score-1.png" width="960"><br/>
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Boxplot_LoanOriginalAmount_StatedMonthlyIncome.bucket_e_Score-1.png" width="960	"><br/>
Esse ficou interessante, pois as taxas pelo score seguem a mesma tendência ao longo das faixas de rendas, mas isso não ocorre com o valor do empréstimo. Por mais que já tenha sido visto que a renda tenha correlação com o valor solicitado, não esperava que o score tivesse essa tendencia nas rendas de até 2.500.<br/>
Ao que pude interpretar do gráfico, mutuários com renda baixa dificilmente têm empréstimos acima de 7.000, independente do score, ou seja, mutuários com grande pontuação tendem a fazer grandes empréstimos, salvo aqueles com renda inferiror à 2.500.<br/>
Conforme a renda vai subindo, o score tende a se relacionar mais com o valor do empréstimo.

# Análise Multivariada

### Discuta sobre os relacionamentos observados nesta parte da investigação. Quais atributos que fortaleceram os demais na observação das variáveis de interesse?
Ficou bem mais evidente com a coloração do Score nos gráficos a relação das taxas com os valores dos empréstimos. Comprovando novamente que baixos scores estão associados a altas taxas e aos empréstimos menores.

Podemos ver também que pessoas desempregadas e/ou com baixas rendas ainda solicitam empréstimos normalmente, claro, sendo limitados aos valores mais baixos em comparação daqueles com alta renda, todavia, o fato de estar desempregado não impede que façam empréstimos como os demais.

Na análise de densidade dos tipos de empréstimos com os valores, a gente observa novamente que vida de estudante não é fácil, pois empréstimos com a categorização de alunos possuem as menores rendas e os menores valores.

### Interações surpreendentes e/ou interessantes foram encontradas entre os atributos?
Acho que os gráficos mais interessantes são os cronológicos, pois é possível observar a variação do sistema ao longo do tempo, as mudanças de terminologia do status do emprego, a implementação do sistema do score assim como seu ajuste em relação as taxas e valores.

O que me surpreendeu bastante foi a última plotagem, demonstrando que nas rendas até 2.500 o score não se relaciona com o valor solicitado - ainda que as taxas se comportem igual as demais faixas de renda -, o score começa a se relacionar mais na medida que as rendas vão subindo.

#### Opcional: Modelos foram criados usando este conjunto de dados? Discuta sobre os pontos fortes e as limitações do seu modelo.
Não realizei criação de modelo até o momento, talvez no futuro o faça, ainda que não haja muitas relações lineares.

------

# Gráficos Finais e Sumário

### Primeiro Gráfico
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Primeiro_Grafico-1.png" width="960">

### Descrição do Primeiro Gráfico
Existe uma clara relação entre o Score e o valor solicitado, sendo possível observar que empréstimos altos normalmente são obtidos pelos scores mais altos. <br/>
Na primeira faixa de renda o score não se relaciona com o valor solicitado, mas também não há grandes empréstimos nessa faixa, na medida em que a renda e o valor do empréstimo aumentam, o score se relaciona mais.<br/>
Ainda que sutíl, nesse gráfico é possível ver os valores dos quartis concentrados nos empréstimos redondos, normalmente de 5.000 em 5.000. Também há concentração incomum nos valores de 4.000, principalmente na primeira faixa de renda.

### Segundo Gráfico
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Segundo_Grafico-1.png" width="960">

### Descrição do Segundo Gráfico
Existe o período sem o sistema de Score, a lacuna sem empréstimos seguida de alguns pouquíssimos e depois a implementação inicial do sistema. Fica claro os ajustes realizados ao longo do tempo, chegando a 2014 com uma relação mais suave entre os scores e as taxas. <br/>
Após esses ajustes, o valor do empréstimo ficou mais relacionado com o score e também foram permitidos os empréstimos acima de 25.000 no mesmo período.

### Terceiro Gráfico
<img src="https://raw.githubusercontent.com/rafaelgfig/UD_NDS_ProspeR/master/plots/Terceiro_Grafico-1.png" width="960">

### Descrição do Terceiro Gráfico
Mutuários desempregados possuem uma concentração bem maior nas rendas baixas - o que é esperado - mas isso não os impede de realizar empréstimos como os demais, ainda que eles fiquem concentrados nos empréstimos inferiores à 7.500.

------

# Reflexão
Comecei selecionando 15 das 81 colunas disponíveis dentro do conjunto de dados originais, pois é relativamente grande se comparado com os outros disponibilizados pela Udacity. Para conseguir analizar dentro do tempo hábil, foi necessário realizar esse filtro inicial. <br/>
Selecionei as colunas que achei mais interessantes para tentar entender os perfís das pessoas que solicitam empréstimos, mas ao longo da análise algunas delas não foram utilizadas. <br/>
As variáveis identificadores foram úteis apenas para verificar alguma inconsistência nos dados relacionado ao mesmo mutuário ou empréstimo. <br/>
A taxa APR engloba a outra taxa, por conta disso acabei me baseando só na APR ao invés de olhar as duas, não precisaria ter selecionado a outra.<br/>
Por fim, só fui observar as relações das variáveis ao longo do tempo no final, acho que isolando as variáveis em faixas de anos eu poderia ter uma correlação mais clara delas, pois sofreram ajustes ao longo dos anos e isso atrapalha algumas análises gerais.

Pensei que o tempo empregado iria ter algum peso na hora de solicitar um empréstimo, determinar o score ou algo do gênero. No fim essa variável não se relacionava com nenhuma outra.

Ao decorrer da análise pude ver que o Score tinha grande importância pois se relacionava fortemente com as taxas e um pouco com o valor do empréstimo, então meu foco mudou um pouco para ela.

Os dados são limitados ao ano de 2014, então atualmente (2019) o sistema de Score deve ter muito mais peso do que antes, pois houve um claro ajuste desse sistema. Olhar para as variáveis que compõe o Score certamente ajudaria entender os perfís dos mutários e isso poderia talvez auxiliar na criação de propostas ou propagandas direcionadas.

Não possuia muito conhecimento prévio sobre o tipo de dados desse conjunto. Ficou claro que o conhecimento sobre o negócio e saber elaborar as perguntas certas é determinante para uma boa análise.
