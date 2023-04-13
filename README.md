# *Valuation* por fluxo de caixa descontado utilizando a simulação de monte carlo :

## Resumo

Quando se trata de obtenção do valor de mercado de companhias abertas, o método de fluxo de caixa descontado é a ferramenta mais difundida, a questão é que ele entrega, dada as variáveis financeiras da empresa, um valor único para mesma. O objetivo desse trabalho é conjugar a essa metodologia tradicional a simulação de monte carlo e dessa forma, ao invés de um valor único, apresentar uma distribuição de probabilidades para o valor da empresa. Tornando possível o conhecimento das probabilidades de ocorrência dos preços da ação quando determinados parâmetros são inseridos no modelo de avaliação. Com isso auxiliando a tomada de decisão sobre a realização de investimentos em um ambiente de incerteza. 

## Abstract

*When it comes to obtaining the market value of publicly-held companies, the discounted cash flow method is the most widespread tool, the question is that it delivers, given the financial variables of the company, a unique value for it. The objective of this work is to combine the Monte Carlo simulation with this traditional methodology and thus, instead of a single value, present a probability distribution for the value of the company. Making it possible to know the probabilities of occurrence of share prices when certain parameters are inserted in the valuation model. With that helping the decision-making on the realization of investments in an environment of uncertainty.*

## 1 - Introdução

Esse trabalho tem como objetivo aplicar a simulação de monte carlo no processo tradicional de avaliação de empresas por fluxo de caixa descontado, a fim de expressar o valor da empresa na forma de uma distribuição de probabilidades, ao invés de um valor único, e com isso expor a incerteza inerente as variáveis utilizadas na avaliação, deixando-a mais aderente a realidade.

O processo de avaliação utilizando a simulação de monte carlo, passa por definir qual distribuição de probabilidades melhor representa as variáveis utilizadas. Encontrada a distribuição que melhor se ajusta a variável estudada, o próximo passo é através das simulações extrapolar os possíveis valores futuros para os parâmetros utilizados na avaliação, e por consequência os possíveis valores para a companhia e suas respectivas probabilidades. 

O resultado esperado é encontrar na avaliação uma distribuição de probabilidades para o preço das ações que guarde semelhanças com os preços negociados em bolsa de valores, não necessariamente o valor central, mas características como a dispersão dos valores, e o formado da distribuição.

## 2 - Modelagem

## 2.1 – Processo de avaliação pelo fluxo de caixa descontado:

Segundo Póvoa (2012) *“O valor de uma companhia equivale ao somatório de todo o caixa gerado no médio-longo prazo, trazido a valor presente por uma taxa de desconto que representa o chamado retorno exigido pelo investidor”*. 

Para avaliar uma empresa através do método de fluxo de caixa descontado, são trazidos a valor presente os fluxos de caixa projetados para a companhia no futuro, alguns anos à frente e na perpetuidade, descontados pelo custo de capital. A dificuldade do método reside na projeção adequada desses fluxos de caixa e na determinação da taxa de desconto utilizada. (PÓVOA 2012)


$$Valor Presente = \sum_{t=1}^{n} \frac{FC_{t}}{(1+r)^{t}}  + \frac{FC_{n}(1+g_{p})}{(r_{p}-g_{p})(1+r)^{n}} $$


$FC_{t}$ - Fluxo de Caixa no ano t

$r$ - Taxa de desconto antes da perpetuidade.

$r_{p}$ - Taxa de desconto na perpetuidade.

$g_{p}$ - Taxa de crescimento na perpetuidade.

Pode ser observado que a equação que descreve o valor presente da empresa é composta de duas parcelas, a primeira representa os anos onde os fluxos de caixa futuros serão projetados, e a segunda representa a perpetuidade também chamado de valor contínuo (COPELAND, 2002), que é o valor limite da série de fluxos de caixa que crescem a taxa $g_{p}$ (taxa de crescimento na perpetuidade) e são descontados pela taxa  $r_{p}$ (taxa de desconto na perpetuidade).

Para se obter o valor da firma, os fluxos de caixa livre para a firma (FCFF – *Free Cash Flow to Firm*) projetados devem ser descontados pelo custo médio ponderado do capital (WACC).

$$Valor Da Firma = \sum_{t=1}^{n} \frac{FCFF_{t}}{(1+WACC)^{t}}\  + \frac{FCFF_{n}(1+g_{p})}{(WACC_{p}-g_{p})(1+WACC)^{n}}\  $$


O objetivo ao calcular o FCFF é encontrar o valor da firma (*Enterprise Value*), que é o somatório do valor da companhia, pertencente aos acionistas, e o valor da dívida, pertencentes aos credores (PÓVOA, 2012). Nesse trabalho o objetivo é encontrar o valor de mercado da companhia, ou seja, o valor pertencente aos acionistas.

***Valor de Mercado =  Valor da Firma - Valor da Dívida Líquida***


### 2.2 – Modelagem do Fluxo de caixa livre.

O fluxo de caixa livre para a firma (FCFF – *Free Cash Flow to Firm*) abrange todo o fluxo de caixa da empresa a ser distribuído a todos os detentores de direito da empresa, acionistas e credores, sob a forma de juros e dividendos. Conforme Póvoa (2012), o cálculo do FCFF se estrutura da seguinte forma:

| FCFF                                                           
|-------------------------------------------------------------|
| = Lucro Operacional depois de impostos EBIT(1-t)            |
| -(Investimento físico - Depreciação = Investimento Líquido) |
| - Variação da necessidade de Capital de Giro                |
| + Todos os itens não-caixa da DRE, ex-depreciação           |
| - Partes estatutárias, ex-acionistas                        |
| = FCFF                                                      |

*Fonte: Póvoa (2012)*

O cálculo do FCFF parte do Lucro Operacional, antes do resultado financeiro e impostos, e a partir dele são subtraídos os impostos a serem pagos, o investimento líquido, a variação da necessidade de capital de giro em seguida são somados todos os itens não-caixa contabilizados na DRE, depois é subtraído o pagamento de partes estatutárias, excluindo acionistas, por fim o resultado é o fluxo de caixa livre para a firma.

Aqui o fluxo de caixa livre será modelado partindo da distribuição de probabilidades da receita projetada, que é encontrada a partir do produto da receita inicial pela distribuição de probabilidades da variação anual da receita. O resultado operacional depois de impostos é obtido, multiplicando a receita projetada pela margem operacional e subtraindo do resultado a taxa de impostos incidente. O reinvestimento líquido é representado como um percentual da receita, e é apresentada também como uma distribuição de probabilidades. A diferença entre o EBIT(1-t) e a taxa de reinvestimento resulta finalmente na distribuição de probabilidades do fluxo de caixa livre para a firma.

| FCFF                                                           
|-------------------------------------------------------------|
| = Receita x Margem Operacional x (1- taxas)                 |
| = Lucro Operacional depois de impostos EBIT(1-t)            |
|  - Taxa de reinvestimento                                   |
| = FCFF                                                      |

### 2.3 – Modelagem do custo do capital.

As empresas usam para financiar suas atividades e projetos, o capital próprio, que é o capital dos sócios (acionistas), e o capital de terceiros que é obtido através da emissão de dívidas como empréstimos e financiamentos bancários ou a emissão de debêntures.

O Custo do Capital Próprio ($K_{cp}$) é o retorno exigido pelos sócios da empresa sobre o capital dispendido para a compra de suas participações. 

O $K_{cp}$  pode ser estimado através do modelo CAPM (*Capital Asset Pricing Model*), onde o retorno exigido pelo investidor, para aquele ativo, tem como base o ativo livre de risco ($R_{f}$) , que será considerado igual a taxa pré-fixada de 5 anos, mais um percentual (β - Beta) do prêmio de risco histórico do mercado de ações, que é a diferença entre o retorno esperado para o mercado de ações e o retorno do ativo livre de risco. (SAMANEZ, 2009)

$$ K_{cp}=R_{f}+β(R_m-R_f)$$

O beta (β), formalmente, representa o coeficiente angular de uma regressão, que visa quantificar o grau da variação de determinado ativo em função da variação de outro ativo. (PÓVOA, 2012)

O beta mede risco de uma empresa em relação ao risco sistemático (não diversificável) de mercado. No Brasil, usamos como índice de referência para o mercado acionário o índice Bovespa (IBOV), então o beta calculado para as ações das empresas abertas brasileiras é a relação entre a variação da cotação dessas ações em relação as variações da cotação do IBOV.

Nesse trabalho será utilizado o ERP (Equity Risk Premium), que é a diferença entre o retorno esperado para o mercado de ações e o retorno do ativo livre de risco, calculado pela FGV-EESP Centro de estudos quantitativos em finanças.

O custo do capital de terceiros, ou custo da dívida, é a taxa de juros a ser paga sobre os financiamentos e empréstimos tomados. Essa taxa de juros é composta pela taxa livre de risco somada ao prêmio de risco exigido pelo financiador. O prêmio de risco reflete o risco de não pagamento da dívida (ASSAF NETO, 2019). O prêmio de risco utilizado será o divulgado pela ANBIMA para os ratings A, AA e AAA , que será representado por uma distribuição triangular, com o valor mínimo igual a taxa do rating AAA , médio AA e máximo A.

$$K_{d} = R_{f} + Spread Da Empresa $$

O pagamento de juros sobre a dívida contempla um benefício fiscal, dado que é dedutível do lucro tributável. Então o custo efetivo seria dado pela equação abaixo:

$$K_{d} = (R_{f} + Spread Da Empresa)(1-t) $$

O custo de capital resultante da composição entre capital próprio e capital de terceiros é chamado Custo Médio Ponderado do Capital (CMPC, ou WACC, do inglês *Weighted Averange Cost of Capital*). O WACC é igual à soma dos retornos médios dessas fontes de recursos, ponderadas pela participação de cada uma no financiamento total. (SAMANEZ, 2009)

$$WACC= K_{cp}\frac{E}{(D+E)}\ + K_{d}(1-t)\frac{D}{(D+E)}$$

$E$ - Equity ,Capital Próprio

$D$ - Dívidas ,Capital de Terceiros

### 2.4 – Modelagem dos parâmetros para perpetuidade.

Para a taxa de desconto na perpetuidade ($WACC_{p}$) será utilizada a mesma distribuição do $WACC$ para os anos iniciais da projeção. Já o crescimento na perpetuidade($g_{p}$) será representado pela distribuição de probabilidades para o crescimento anual do PIB nominal.

## 3 - Aplicação e Resultados

O modelo de valuation descrito na seção anterior foi aplicado sobre os dados financeiros da empresa LOJAS RENNER. Os dados foram extraídos diretamente do site de R.I. da empresa, depois foram consolidados no arquivo .CSV utilizado nesse trabalho.

No pré-processamento dos dados foi aplicado um corte dos valores nos percentis maiores que 90% e menores que 10% no parâmetro de variação da receita, esse tratamento foi dado com o objetivo de retirar os valores de baixíssima probabilidade de ocorrência, como os observados na pandemia do COVID-19. Quando esse tratamento não é realizado observou-se que os valores médios na avaliação da empresa não são alterados drasticamente, porém a variância da distribuição de valores obtida fica muito mais alta do que a observada nos preços negociados em bolsa.

O passo seguinte foi descobrir qual distribuição de probabilidades se ajustaria melhor as variáveis, para isso foi utilizada a biblioteca Fitter. 
Após encontrar a distribuição mais ajustada, são gerados mil dados simulados a serem utilizados no cálculo do valuation da empresa. Esse procedimento foi realizado nas variáveis de determinação do fluxo de caixa (variação da receita, margem EBIT, taxa de impostos sobre o EBIT, e taxa de reinvestimento), nas variáveis utilizadas no cálculo do custo do capital (percentual de dívida na composição do capital e Equity risk premium), e para o PIB, que serve de representação do crescimento na perpetuidade.

Para o spread de crédito foram utilizadas as taxas publicadas na ANBIMA e foi gerada uma distribuição triangular a partir dos valores dos ratings A, AA e AAA.

Já para a taxa livre de risco e para o beta, foram utilizados os valores correntes. Para a taxa livre de risco foi escolhida a taxa pré-fixada com maturidade de cinco anos, e o beta foi calculado utilizando as variações de preço de mercado de LOJAS RENNER e do IBOV nos últimos cinco anos.
No cálculo do valor da firma as distribuições de probabilidades obtidas foram utilizadas para projetar os valores de fluxo de caixa e taxa de desconto para os próximos cinco anos, e na perpetuidade o PIB nominal é utilizado para projeção do crescimento. Obtendo o seguinte resultado:

**---------- ENTERPRISE VALUE --------**


O valor presente médio da firma é igual a R$ 25.85

O desvio padrão é igual a R$ 15.87

O valor no percentil 5% é igual a R$ 7.32

O valor no percentil 50% é igual a R$ 22.88

O valor no percentil 95% é igual a R$  56.14


Para a obtenção do valor de mercado para o acionista, a dívida líquida deve ser subtraída do valor da firma. Obtendo o seguinte resultado:

**---------- EQUITY VALUE --------**

O valor presente médio de mercado é igual a R$ 26.95

O desvio padrão é igual a R$ 15.87

O valor no percentil 5% é igual a R$ 8.42

O valor no percentil 50% é igual a R$ 23.98

O valor no percentil 95% é igual a R$  57.24

Quando é feito o ajuste da distribuição de probabilidade do crescimento na perpetuidade para uma distribuição triangular, com o limite mínimo de 4%, a média de 6% e o limite máximo de 8%, ao invés de usar diretamente a distribuição, obtemos um valor de desvio padrão mais parecido com os valores negociados em bolsa nos últimos cinco anos. Como abaixo:

**---------- EQUITY VALUE --------** 

O valor presente médio de mercado é igual a R$ 20.92

O desvio padrão é igual a R$ 9.35

O valor no percentil 5% é igual a R$ 8.15

O valor no percentil 50% é igual a R$ 19.81

O valor no percentil 95% é igual a R$  37.45



**---------- Distribuição dos preços negociados em bolsa --------** 

O valor presente médio de mercado é igual a R$ 33.29

O desvio padrão é igual a R$ 8.87

O valor no percentil 5% é igual a R$ 20.18

O valor no percentil 50% é igual a R$ 33.74

O valor no percentil 95% é igual a R$  47.91


Comparando essa última avaliação o preço atual (Fechamento de 11/04/2023), chegamos as seguintes conclusões:

**----COMPARATIVO ENTRE O VALUATION E O PREÇO NEGOCIADO EM BOLSA DE VALORES----**

Preço atual da ação: R$ 16.9

Preço justo médio: R$ 20.92

Up-side com relação ao preço justo médio: 23.8 %

Percentil do preço atual com relação a distribuição do preço justo: 36.1 %

## 4 - Conclusão

Com a utilização da simulação de monte carlo foi possível a obtenção de uma distribuição de probabilidades para o preço da ação e não apenas um único preço justo. Com isso distinguir, se o preço negociado, agora, em bolsa de valores está caro ou barato, fica mais fácil. Além disso, permite estimar qual seria a probabilidade esperada para a negociação naquele preço específico. Ajudando na tomada de decisão nesse ambiente cheio de incertezas.

## 5 - Referências

ASSAF NETO, Alexandre. **Valuation: métricas de valor & avaliação de empresas.** 2. ed. São Paulo: Atlas, 2019.

COPELAND, Tom; KOLLER, Tim; MURRIN, Jack. **Avaliação de Empresas: valuation.** 3.ed. São Paulo: Makron Books, 2002

PÓVOA, Alexandre. **Valuation: como precificar ações.** Rio de Janeiro: Elsevier, 2012.

SAMANEZ, Carlos Patrício. **Engenharia Econômica.** São Paulo: Pearson Prentice Hall, 2009.

Marcos Oliveira, Luiz Neto. **Simulação de Monte Carlo e Valuation: uma abordagem estocástica** REGE - Revista de Gestão, Vol.19,2012,https://doi.org/10.5700/rege474.

---

Aluno: Alvaro Augusto Silva Junior

Matrícula: 211.101.129
