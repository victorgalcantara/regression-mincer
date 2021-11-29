# regression-mincer
A study of mincer earnings regression with data from Brazilian demographic samples (PNAD-c).

Este estudo foi realizado como um dos trabalhos para a disciplina de Estatística e Data Science para Ciências Sociais no Instituto de Estudos em Sociologia e Política (IESP/UERJ), ministrado pelos professores Rogério Jerônimo Barbosa e Carlos Antônio Ribeiro.

## Introdução de Rojério Barbosa: Estudando os “retornos educacionais” no Brasil
No final da década de 1950, surge, entre os economistas norte-americanos, uma nova abordagem para compreender a relação entre o trabalho e os salários auferidos no mercado: a Teoria do Capital Humano. Segundo suas hipóteses, as capacidades produtivas dos indivíduos seriam uma espécie de “ativo” ou “capital”; mas que, diferentemente do capital físico (máquinas e meios de produção em geral), seria algo incorporado e indissociável da própria pessoa: eventuais talentos e habilidades inatas, conhecimentos adquiridos ao longo da vida, a saúde física e mental etc.

Em princípio, o capital humano seria algo bastante abstrato e geral: toda e qualquer característica que tornasse uma pessoa mais produtiva. No entanto, os proponentes dessa teoria acabaram enfatizando os atributos e característica que são passíveis de modificação, intervenção ou investimento ao longo da vida: como, por exemplo, educação formal, cursos de qualificação, experiência no trabalho (on-the-job training) etc. Assim, adquirir mais anos de estudo seria entendido como um “investimento” nas capacidades produtivas. E então sugeriram aqueles economistas: assim como o lucro poderia ser entendido como o retorno pelo investimento feito em capital físico; os salários e rendimentos do trabalho poderiam ser compreendidos como retorno1 pelo investimento em “capital humano” – isto é, uma espécie de recompensa pela produtividade aumentada.

Essa teoria se tornou alvo de muitas críticas por parte das Ciências Sociais, por individualizar os determinantes das desigualdades e desconsiderar aspectos “não produtivos” que determinam os salários (como desigualdades de gênero, raça e outros tipos). Além disso, a teoria supõe que os conhecimentos adquiridos se traduziriam em mais produtividade (o que é plausível...) e essa se converteria automaticamente em remuneração (o que não é tão plausível, se compreendermos que os mercados são imperfeitos e há mecanismos discriminatórios que podem alterar os padrões de retornos para certos grupos).

Nesse exercício, vamos temporariamente suspender a crítica para uma finalidade didática específica: tentar entender um dos pilares importantes da Teoria do Capital Humano, a famosa “equação de salários” ou “[equação minceriana](https://en.wikipedia.org/wiki/Mincer_earnings_function)”. Essa última expressão remete ao seu proponente, o economista polonês radicado nos EUA, Jacob Mincer. O modelo de Mincer parte da ideia de que o capital humano poderia ser, em larga medida, capturado por duas variáveis relacionadas aos conhecimentos dos trabalhadores: (1) a escolaridade (medida na forma de anos de estudo), e (2) experiência de trabalho (medida como anos dispendidos no mercado de trabalho). Ambas as variáveis explicariam grande parte dos rendimentos do trabalho e manteriam com ele uma associação positiva: quanto maior a escolaridade e/ou a experiência também maiores seriam os rendimentos.

De acordo com Mincer, os principais aspectos da relação entre educação formal, experiência e rendimentos podem ser captados pela seguinte equação:

log( 𝑦𝑖)=𝛽0+𝛽1𝑆𝑖+𝛽2𝑋𝑖+𝛽3𝑋𝑖2+𝜖𝑖

Nessa equação temos:
log(𝑦𝑖) representa o logaritmo da renda do trabalho (𝑦𝑖) do indivíduo 𝑖
𝑆𝑖 é a quantidade de anos de estudo do indivíduo 𝑖
𝑋𝑖 é a quantidade de anos de experiência no mercado de trabalho do indivíduo 𝑖
𝑋𝑖2 é a mesma variável de anos de experiência acima, mas elevada ao quadrado
𝜖𝑖 é o termo de erros aleatórios do indivíduo 𝑖

E, com respeito aos parâmetros, temos:
𝛽0 o é intercepto
𝛽1 o é coeficiente de inclinação da variável educação (essa é a medida dos “retornos à educação”)
𝛽2 o é coeficiente de inclinação da variável experiência
𝛽3 o é coeficiente de inclinação da variável experiência ao quadrado

Neste exercício, estimamos o modelo de Mincer usando os dados da PNAD Contínua, a pesquisa amostral domiciliar do IBGE, que investiga características socioeconômicas e do mercado de trabalho.

### Anos de escolarização

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/anos-est-2019.png"/>

Com o gráfico de barras acima podemos observar uma concentração de pessoas com 13 anos de estudo, o que corresponde ao Ensino Médio completo, uma parcela significativa com 17 anos de estudo, o que corresponde ao Ensino Superior completo, e grupos minoritários com 6 e 10 anos de estudo, o que corresponde, respectivamente, ao Ensino Fundamental incompleto e completo.

É importante lembrar que estamos trabalhando com um recorte da amostra com pessoas com renda e idade entre 18-64 anos. Portanto, os anos de escolaridade representados no gráfico não refletem os níveis de escolaridade alcançado pela população.

### Idade

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/pnad-idade-2019.png"/>

Com o gráfico de barras acima podemos observar uma concentração de pessoas entre 24 e 50 anos, o que corresponde à uma parcela da população em idade ativa, com uma tendência à redução de pessoas com idade acima de 50 anos. Como a idade é uma variável métrica contínua, podemos representar também por um histograma com faixas etárias.

### Experiência

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/pnad-exp-2019.png"/>

O gráfico de barras acima representa a frequência de observações nos determinados anos de experiência, que foi calculado em função da idade, dos anos de estudo e de uma constante 6. Compreende-se que a experiência é igual a idade menos os anos de estudo e a constante 6. Indivíduos com 18 anos de idade e 16 anos de estudo, por exemplo, teriam experiência menor que zero. Pela impossibilidade lógica de uma pessoa ter menor que zero anos de experiência, computou-se todos os valores negativos como zero. Já indivíduos com 64 anos e 16 anos de estudo teriam 42 anos de experiência, enquanto que os com 0 anos de estudos teriam 58 anos de experiência. No limite, portanto, temos que a experiência pode variar de 0 - 58 anos em nosso recorte da amostra. Os casos com experiência até 35 anos são mais frequentes, enquanto que há uma tendência de decrescimento da frequência de casos com mais de 35 anos de experiência. Podemos inferir, por exemplo, que essa tendência acompanha o decrescimento da população com idade superior à 50 anos, como observamos no gráfico relativo à idade.

### Renda

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/ln-renda.png"/>

O histograma acima representa a frequência de casos com o logarítmo natural de determinada renda, ou em outras palavras a renda logaritmizada. Note que o log é uma operação inversa da exponencial, e portanto comprime a distância entre os casos, ao invês de atenuar. O log de 1000 na base 10, por exemplo, é 3, ou em outras palavras, 10 elevado a 3 é 1000.  Os casos com renda logaritmizada igual a 5 correspondem à base do log natural (e = 2.71) elevada a 5, ou 143.48. Nessa mesma lógica, os casos com log da renda em 10 corresponde à 20.589.11.

A transformação logarítmica é frequentemente usada para corrigir a assimetria de variáveis, como renda e população, que têm um pequeno número de observações com valores positivos extremamente grandes ou pequenos e muito distantes da concentração. Com a renda logaritmizada, as distâncias entre as observaçoes são comprimidas, fazendo com que o enviesamento/assimetria (skewness) seja eliminado e a distribuição seja mais próxima de uma distribuição normal.

## Análises bivariadas
### Escolarização e renda

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/media-renda-escol.png"/>

O gráfico de dispersão acima representa as observações dada a escolaridade e a renda. Em geral, a variável a ser explicada (dependente) é colocada no eixo vertical (y), no sentido de que está em função de outras variáveis que podem ser explicativas. Embora fosse esperado uma correlação entre escolaridade e renda, não é muito perceptível essa informação no gráfico. Podemos observar em um grau moderado que há mais casos com renda elevada conforme aumenta a escolaridade. Vemos ainda que a variável escolaridade é métrica discreta e reflete seu comportamento no gráfico, com pontos de observação aglomerados que se aproximam graficamente de linhas verticais.

#### com log natural da Renda

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/me-lnrenda-escol.png"/>

O gráfico acima representa a média da renda logaritmizada em função da escolaridade. Complicado, não é? Mas podemos observar aqui que a função logaritmo da renda opera apenas como uma compressão das distâncias entre os casos. Vemos acima que a relação entre o log(renda) e escolaridade é exatamente igual à da renda, conforme o gráfico anterior. A diferença está no eixo vertical (y), em que podemos ver a maior proximidade entre as rendas, o que não interfere na análise de correlação.

### Idade e renda

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/me-renda-idade.png"/>

Agora com a idade podemos observar uma tendência relativamente diferente. Assim como com a escolaridade, há uma relação positiva entre renda e idade. No entanto, vemos também que é uma relação não linear, pois o crescimento da renda permanece quase constante até 40 anos, quando começa a crescer cada vez menos até se estabilizar. É um crescimento parecido com o comportamento de uma curva logarítmica.

### Experiência e renda

<img src="https://github.com/victorgalcantara/regression-mincer/blob/main/assets/me-renda-exp.png"/>

Agora com a experiência vemos outro comportamento na relação com a renda, mas ainda muito distante de ser um comportamento próximo de uma aleatoriedade que indique a possibilidade de independência. Vemos que há uma relação entre renda e experiência, que é igual à uma parábola: positiva até aprox. 12 anos, com estabilidade até aprox. 32 anos e queda deste ponto em diante. Se lembrarmos da análise univariada da experiência, teremos que as faixas com menor experiência são os mais jovens ou adultos com muitos anos de estudos. Conforme vimos no gráfico anterior, essa faixa etária está em crescimento constante de renda até atingir um pico de estabilização, o que vemos também refletido na experiência (uma vez que está em função da idade menos anos de estudo e menos a constante 6). A queda aqui representada para pode estar associada aos casos de pessoas mais idosas que não acessaram a escola e, portanto, possuem menor anos de estudo.
