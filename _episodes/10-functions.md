---
title: Functions Explained
teaching: 45
exercises: 15
questions:
- "Como posso escrever uma nova função em R?"
objectives:
- "Definir uma função que tem argumentos."
- "Retornar um valor desde a função."
- "Testar uma função."
- "Definir valores padrão para argumentos de função."
- "Explicar por que devemos dividir os programas em pequenas funções de propósito único."
keypoints:
- "Usar `function` para definir uma nova função em R."
- "Usar parâmetros para passar valores entre funções."
- "Carregar funções entre programas usando `source`."
source: Rmd
---




Se nós tivéssemos apenas um conjunto de dados para analisar, provavelmente seria mais rápido 
carregar o arquivo em uma planilha e usá-la para plotar estatísticas simples. Todavia, os
dados do gapminder são atualizados periodicamente, e talvez nós quiséssemos pegar essas novas
informações depois e recolocá-las na nossa análise de novo. Nós também poderíamos pegar dados 
similares de uma fonte diferente no futuro.

Nessa lição, nós aprenderemos como escrever uma função para que possamos repetir
várias operações com um único comando.

> ## O que é uma função?
>
> Funções juntam uma sequência de operações em um todo, preservando isso para um uso contínuo, funções tem como característica:
>
> * Um nome que possamos invocar e lembrar depois
> * Um alívio para a necessidade de lembrar operações individuais
> * Um conjunto definido de entradas e suas esperadas saídas
> * Ricas conexões para o grande meio de programação
>
> Como o bloco de construção básico da maioria das linguagens de programação,
> funções "constituem" programação "tanto quanto qualquer abstração. Se
> você escreveu uma função, você é um programador de computador.
{: .callout}

## Definindo uma função

Vamos abrir um novo arquivo script do R em `functions/` directory e chamá-lo de functions-lesson.R.


~~~
my_sum <- function(a, b) {
  the_sum <- a + b
  return(the_sum) 
}
~~~
{: .r}

Vamos definir uma função fahr_to_kelvin que converte temperaturas de Fahrenheit a Kelvin:


~~~
fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5 / 9)) + 273.15
  return(kelvin)
}
~~~
{: .r}

Nós definimos `fahr_to_kelvin` atribuindo-o à saída de `function`.  A lista
de nomes de argumentos estão contidos entre parênteses. Em seguida, o
[corpo]({{ page.root }}/reference/#function-body) da função--as declarações que são
executadas quando ele é executado--estão contidas dentro de chaves (`{}`). As declarações
no corpo são recuados por dois espaços. Isso torna o código mais fácil de ler, mas
não afeta o funcionamento do código.

Quando chamamos a função, os valores que passamos aos argumentos são assinalados às
variáveis para que possamos usá-las dentro de uma função. Dentro da função nós
usamos uma [return statement]({{ page.root }}/reference/#return-statement) para enviar o resultado de volta
para quem o pediu.

> ## Dica
>
> Uma característica única do R é que uma afirmação de retorno não é requerida.
> O R retorna automaticamente qualquer variável que está na última linha do corpo
> da função. Mas por clareza, nós vamos explicitamente definir
> a afirmação de retorno.
{: .callout}


Vamos tentar rodar nossa função.
Chamar a nossa função não é diferente de chamar qualquer outra função:


~~~
# freezing point of water
fahr_to_kelvin(32)
~~~
{: .r}



~~~
[1] 273.15
~~~
{: .output}


~~~
# boiling point of water
fahr_to_kelvin(212)
~~~
{: .r}



~~~
[1] 373.15
~~~
{: .output}

> ## Desafio 1
>
> Escreva uma função chamada `kelvin_to_celsius` que pega a temperatura em Kelvin
> e transforma em Celsius
>
> Dica: para converter de Kelvin para Celsius é só subtrair 273.15
>
> > ## Solução do Desafio 1
> >
> > Escreva uma função chamada `kelvin_to_celsius` que pega a temperatura em Kelvin
> > e transforma em Celsius
> >
> > 
> > ~~~
> > kelvin_to_celsius <- function(temp) {
> >  celsius <- temp - 273.15
> >  return(celsius)
> > }
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

## Combinando Funções

O real poder das funções está em mesclar e combinar as funções
em maiores para conseguir o efeito desejado.

Vamos definir duas funções que convertem a temperatura de Fahrenheit para
Kelvin, e Kelvin para Celsius:


~~~
fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5 / 9)) + 273.15
  return(kelvin)
}

kelvin_to_celsius <- function(temp) {
  celsius <- temp - 273.15
  return(celsius)
}
~~~
{: .r}

> ## Desafio 2
>
> Defina a função que converte diratamente de Fahrenheit para Celsius, 
> reutilizando as duas funções acima (ou usando as funções que preferir).
>
>
> > ## Solução Desafio 2
> >
> > Vamos definir uma função que calcula o Produto Interno Bruto de uma nação a partir 
>> dos dados disponíveis no nosso conjunto de dados.
> >
> >
> > 
> > ~~~
> > fahr_to_celsius <- function(temp) {
> >   temp_k <- fahr_to_kelvin(temp)
> >   result <- kelvin_to_celsius(temp_k)
> >   return(result)
> > }
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}


We're going to define
a function that calculates the Gross Domestic Product of a nation from the data
available in our dataset:


~~~
# Takes a dataset and multiplies the population column
# with the GDP per capita column.
calcGDP <- function(dat) {
  gdp <- dat$pop * dat$gdpPercap
  return(gdp)
}
~~~
{: .r}

Nós definimos calcGDP ao assinalar a saída da função. A lista dos nomes dos argumentos
está contida dentro dos parênteses. Depois, o corpo da função - as afirmações executadas 
quando você chama a função - está contida dentro das chaves ({}).

Nós dividimos as afirmações dentro do corpo por dois espaços. Isso deixa o código mais
fácil de entender, mas não afeta seu modo de operação.

Quando nós chamamos a função, os valores que passamos a ela são assinalados para os argumentos, 
que se tornam variáveis dentro do corpo da função.

Dentro da função, nós usamos a função return para retornar o resultado. A função de retorno
é opcional: o R vai automaticamente retornar os resultados qualquer que seja o comando executado na última linha da função.



~~~
calcGDP(head(gapminder))
~~~
{: .r}



~~~
[1]  6567086330  7585448670  8758855797  9648014150  9678553274 11697659231
~~~
{: .output}

Isso não é muito informativo. Vamos adicionar mais argumentos para que possamos extrair informações por ano e por país.


~~~
# Takes a dataset and multiplies the population column
# with the GDP per capita column.
calcGDP <- function(dat, year=NULL, country=NULL) {
  if(!is.null(year)) {
    dat <- dat[dat$year %in% year, ]
  }
  if (!is.null(country)) {
    dat <- dat[dat$country %in% country,]
  }
  gdp <- dat$pop * dat$gdpPercap

  new <- cbind(dat, gdp=gdp)
  return(new)
}
~~~
{: .r}

Se você já está escrevendo essas funções em um script do R separado(uma boa ideia!), 
você pode carregar essas funções para a nossa sessão do R usando a função source.


~~~
source("functions/functions-lesson.R")
~~~
{: .r}

OK, agora tem muitas coisas acontecendo com essa função. Em português claro, 
a função agora subdivide os dados por ano, se o argumento year não estiver vazio, 
depois ele subdivide o resultado por país se o argumento country não estiver vazio.
Após tudo isso, ele calcula o PIB para quaisquer subconjuntos que surgem depois dessas
operações dos dois passos anteriores. A função adiciona o PIB como uma nova coluna 
para os dados subdivididos e retorna isso como o resultado final. Você pode ver que a 
saída final é muito mais informativa que um vetor de números.

Vamos ver o que acontece quando especificamos um ano:


~~~
head(calcGDP(gapminder, year=2007))
~~~
{: .r}



~~~
       country year      pop continent lifeExp  gdpPercap          gdp
12 Afghanistan 2007 31889923      Asia  43.828   974.5803  31079291949
24     Albania 2007  3600523    Europe  76.423  5937.0295  21376411360
36     Algeria 2007 33333216    Africa  72.301  6223.3675 207444851958
48      Angola 2007 12420476    Africa  42.731  4797.2313  59583895818
60   Argentina 2007 40301927  Americas  75.320 12779.3796 515033625357
72   Australia 2007 20434176   Oceania  81.235 34435.3674 703658358894
~~~
{: .output}

Ou, para um país específico:


~~~
calcGDP(gapminder, country="Australia")
~~~
{: .r}



~~~
     country year      pop continent lifeExp gdpPercap          gdp
61 Australia 1952  8691212   Oceania  69.120  10039.60  87256254102
62 Australia 1957  9712569   Oceania  70.330  10949.65 106349227169
63 Australia 1962 10794968   Oceania  70.930  12217.23 131884573002
64 Australia 1967 11872264   Oceania  71.100  14526.12 172457986742
65 Australia 1972 13177000   Oceania  71.930  16788.63 221223770658
66 Australia 1977 14074100   Oceania  73.490  18334.20 258037329175
67 Australia 1982 15184200   Oceania  74.740  19477.01 295742804309
68 Australia 1987 16257249   Oceania  76.320  21888.89 355853119294
69 Australia 1992 17481977   Oceania  77.560  23424.77 409511234952
70 Australia 1997 18565243   Oceania  78.830  26997.94 501223252921
71 Australia 2002 19546792   Oceania  80.370  30687.75 599847158654
72 Australia 2007 20434176   Oceania  81.235  34435.37 703658358894
~~~
{: .output}

Ou os dois:


~~~
calcGDP(gapminder, year=2007, country="Australia")
~~~
{: .r}



~~~
     country year      pop continent lifeExp gdpPercap          gdp
72 Australia 2007 20434176   Oceania  81.235  34435.37 703658358894
~~~
{: .output}

Vamos passar pelo corpo da função:


~~~
calcGDP <- function(dat, year=NULL, country=NULL) {
~~~
{: .r}

Aqui nós adicionamos dois argumentos, year e country. Nós os colocamos como argumentos default
usando a função Null usando o operador = na definição. Isso significa que esses argumentos vão 
pegar esses valores a não ser que o usuário especifique de maneira diferente.


~~~
  if(!is.null(year)) {
    dat <- dat[dat$year %in% year, ]
  }
  if (!is.null(country)) {
    dat <- dat[dat$country %in% country,]
  }
~~~
{: .r}

Aqui, verificamos se cada argumento adicional é definido como nulo, e sempre que eles 
não são nulos irão sobrepor o conjunto de dados armazenado pelo argumento não nulo.
Fazemos isso para que nossa função seja mais flexível para mais tarde. Podemos pedir para calcular o GDP para:

 * Conjunto de dados inteiro;
 * Um único ano;
 * Um único país;
 * Uma única combinação de ano e país.

Ao usar% em%, também podemos dar vários anos ou países a esses argumentos.

> ## Dica: PASSANDO O VALOR
>
> As funções no R, criam ópias para que possam operar dentro do corpo de uma função.
> Quando modificamos o dado dentro da função estamos modificando a cópia do conjunto de dados armazenado, 
> não a variável original que demos como o primeiro argumento.
> Isso é chamado de "pass-by-value" e torna o código de escrita muito mais seguro: você sempre pode ter certeza de que, 
> independentemente das mudanças que fizer no corpo da função, fique dentro do corpo da função.

{: .callout}

> ## Dica: ESCOPO DA FUNÇÃO
>
> Outro conceito importante é o escopo: quaisquer variáveis ou funções que você criar ou modificar dentro do corpo de uma
> função só existem para o tempo de vida da execução da função. Quando chamamos calcGDP, as variáveis dat, gdp e new só 
> existem dentrodo corpo da função. 
> Mesmo que tenhamos variáveis do mesmo nome em nossa sessão R interativa,elas não são modificadas de forma alguma 
> ao executar uma função.
{: .callout}


~~~
  gdp <- dat$pop * dat$gdpPercap
  new <- cbind(dat, gdp=gdp)
  return(new)
}
~~~
{: .r}

Finalmente, calculamos o GDP em nosso novo subconjunto e criamos um novo quadro de dados com essa coluna adicionada. 
Isso significa que quando chamamos a função mais tarde, podemos ver o contexto para os valores retornados do GDP,
o que é muito melhor do que em nossa primeira tentativa onde temos um vetor de números.

> ## DESAFIO 3
>
> Teste sua função do GDP calculando o GDP para Nova Zelândia em 1987. Como este diferem do GDP de Nova Zelândia em 1952?
>
> > ## Solução Desfaio 3
> >
> > GDP da Nova Zelândia em 1987: 65050008703
> >
> > GDP da Nova Zelândia em 1952: 21058193787
> {: .solution}
{: .challenge}


> ## Desafio 4
>
> A função de colar pode ser usada para combinar texto, por exemplo:
>
> 
> ~~~
> best_practice <- c("Write", "programs", "for", "people", "not", "computers")
> paste(best_practice, collapse=" ")
> ~~~
> {: .r}
> 
> 
> 
> ~~~
> [1] "Write programs for people not computers"
> ~~~
> {: .output}
>
>  Escreva uma função chamada fence que leva dois vetores como argumentos, chamados 
> text e wrapper, e devolva o texto com o wrapper:
>
> 
> ~~~
> fence(text=best_practice, wrapper="***")
> ~~~
> {: .r}
>
> *Nota:*a função colar tem um argumento chamado 'sep', que especifica o separador entre texto. 
> O padrão é um espaço: "". O padrão para colar não é "" espaço.

>
> > ## Solução Desafio 4
> >
>>  Escreva uma função chamada fence que leva dois vetores como argumentos, chamados 
>> 'text' e 'wrapper', e devolva o texto com o wrapper:
> >
> > 
> > ~~~
> > fence <- function(text, wrapper){
> >   text <- c(wrapper, text, wrapper)
> >   result <- paste(text, collapse = " ")
> >   return(result)
> > }
> > best_practice <- c("Write", "programs", "for", "people", "not", "computers")
> > fence(text=best_practice, wrapper="***")
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] "*** Write programs for people not computers ***"
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Dica
>
> R tem alguns aspectos únicos que podem ser explorados ao realizar operações mais complicadas. 
> Não estaremos escrevendo nada que exija o conhecimento desses conceitos mais avançados. 
> No futuro, quando você estiver confortável escrevendo funções em R, você pode aprender mais 
> lendo o R Manual de Linguagem ou o capítulo de programação em R Avançada, 
> por Hadley Wickham. Para contexto, R usa a terminologia "ambientes" em vez de quadros.

{: .callout}

[man]: http://cran.r-project.org/doc/manuals/r-release/R-lang.html#Environment-objects
[chapter]: http://adv-r.had.co.nz/Environments.html
[adv-r]: http://adv-r.had.co.nz/


> ## Dica: Testando e Documentando
>
> É importante testar as funções e documentá-las: a documentação ajuda 
> você e outros a entender qual é a finalidade de sua função e como usá-la,
> e é importante certificar-se de que sua função realmente faça o que você acha que ela faz.

>
> Quando você começar pela primeira vez, seu fluxo de trabalho provavelmente será muito parecido com isto:
>
>  1. Escrever uma função
>  2. Partes do comentário da função para documentar seu comportamento
>  3. Carregar no arquivo de origem
>  4. Experimente para se certificar de que ele se comporta como você espera
>  5. Faça as correções de bugs necessárias
>  6. Salve e Repita

>
> A documentação formal para funções, escrita em arquivos .Rd, é transformada na 
> documentação que você vê nos arquivos de ajuda. O pacote roxygen2 permite que
> os codificadores R escrevam a documentação ao lado do código de função e, em seguida, 
> processe-o nos arquivos .Rd apropriados. Você vai querer mudar para este método mais
> formal de escrever documentação quando você começar a escrever projetos R mais complicados.

>
> Testes automatizados podem ser escritos usando o pacote [testthat][] .
{: .callout}

[roxygen2]: http://cran.r-project.org/web/packages/roxygen2/vignettes/rd.html
[testthat]: http://r-pkgs.had.co.nz/tests.html

