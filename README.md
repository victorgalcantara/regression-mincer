# regression-mincer
A study of mincer earnings regression with data from Brazilian demographic samples (PNAD-c).

Este estudo foi realizado como um dos trabalhos para a disciplina de Estatística e Data Science para Ciências Sociais no Instituto de Estudos em Sociologia e Política (IESP/UERJ), ministrado pelos professores Rogério Jerônimo Barbosa e Carlos Antônio Ribeiro.

### Introdução de Rojério Barbosa: Estudando os “retornos educacionais” no Brasil
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
