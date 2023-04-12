# Valuation_SMC
# *Valuation* pelo método de fluxo de caixa descontado utilizando a simulação de monte carlo :



1 - Introdução

2 - Modelagem

  2.1 – Processo de avaliação pelo fluxo de caixa descontado:

  2.2 – Modelagem do Fluxo de caixa livre.

  2.3 – Modelagem do custo do capital.

  2.4 – Modelagem dos parâmetros para perpetuidade.


3 - Aplicação e Resultados

4 - Conclusão

5 - Referências

## Resumo

## Abstract

## 1 - Introdução

Esse trabalho tem como objetivo aplicar a simulação de monte carlo no processo tradicional de avaliação de empresas por fluxo de caixa descontado, a fim de expressar o valor da empresa na forma de uma distribuição de probabilidades, ao invés de um valor único, e com isso expor a incerteza inerente as variáveis utilizadas na avaliação, deixando-a mais aderente a realidade.

O processo de avaliação utilizando a simulação de monte carlo, passa por definir qual distribuição de probabilidades melhor representa as variáveis utilizadas. Encontrada a distribuição que melhor se ajusta a variável estudada, o próximo passo é através das simulações extrapolar os possíveis valores futuros para os parâmetros utilizados na avaliação, e por consequência os possíveis valores para a companhia e suas respectivas probabilidades. 

O resultado esperado é encontrar na avaliação uma distribuição de probabilidades para o preço das ações que guarde semelhanças com os preços negociados em bolsa de valores, não necessariamente o valor central, mas características como a dispersão dos valores, e o formado da distribuição.

## 2 - Modelagem

## 2.1 – Processo de avaliação pelo fluxo de caixa descontado:

Segundo Póvoa (2012, p. 96) *“O valor de uma companhia equivale ao somatório de todo o caixa gerado no médio-longo prazo, trazido a valor presente por uma taxa de desconto que representa o chamado retorno exigido pelo investidor”*. 

Para avaliar uma empresa através do método de fluxo de caixa descontado, são trazidos a valor presente os fluxos de caixa projetados para a companhia no futuro, alguns anos à frente e na perpetuidade, descontados pelo custo de capital. A dificuldade do método reside na projeção adequada desses fluxos de caixa e na determinação da taxa de desconto utilizada. (PÓVOA 2012, p. 99)

$$Valor Presente = \sum_{t=1}^{n} \frac{FC_{t}}{(1+r)^{t}}  + \frac{FC_{n}*(1+g_{p})}{(r_{p}-g_{p})*(1+r)^{n}} $$


$FC_{t}$ - Fluxo de Caixa no ano t

$r$ - Taxa de desconto antes da perpetuidade.

$r_{p}$ - Taxa de desconto na perpetuidade.

$g_{p}$ - Taxa de crescimento na perpetuidade.

Pode ser observado que a equação que descreve o valor presente da empresa é composta de duas parcelas, a primeira representa os anos onde os fluxos de caixa futuros serão projetados, e a segunda representa a perpetuidade também chamado de valor contínuo (COPELAND, 2002, p.273), que é o valor limite da série de fluxos de caixa que crescem a taxa $g_{p}$ (taxa de crescimento na perpetuidade) e são descontados pela taxa  $r_{p}$ (taxa de desconto na perpetuidade).

Para se obter o valor da firma, os fluxos de caixa livre para a firma (FCFF – *Free Cash Flow to Firm*) projetados devem ser descontados pelo custo médio ponderado do capital (WACC).

$$Valor Da Firma = \sum_{t=1}^{n} \frac{FCFF_{t}}{(1+WACC)^{t}}\  + \frac{FCFF_{n}*(1+g_{p})}{(WACC_{p}-g_{p})*(1+WACC)^{n}}\  $$


O objetivo ao calcular o FCFF é encontrar o valor da firma (*Enterprise Value*), que é o somatório do valor da companhia, pertencente aos acionistas, e o valor da dívida, pertencentes aos credores (PÓVOA, 2012, p.50). Nesse trabalho o objetivo é encontrar o valor de mercado da companhia, ou seja, o valor pertencente aos acionistas.

***Valor de Mercado =  Valor da Firma - Valor da Dívida Líquida***
