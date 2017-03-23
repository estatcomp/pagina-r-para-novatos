---
title: Vectorization
teaching: 10
exercises: 15
questions:
- "Como eu posso operar todos elementos de um vetor de uma só vez?"
objectives:
- "Compreender operações com vetores no R."
keypoints:
- "Usar operações com vetores ao invés de loops."
source: Rmd
---



A maior parte das funções no R são vetorizadas, o que significa que a função
vai operar todos os elementos de um vetor de uma só vez, sem que seja necessario 
operarcada elemento do vetor de forma individual. Isto faz com que o código seja 
mais consiso, fácil de ler e menos sujeito ao erro.



~~~
x <- 1:4
x * 2
~~~
{: .r}



~~~
[1] 2 4 6 8
~~~
{: .output}

A multiplicação foi feita em cada elemento do vetor.

Nós também podemos somar dois vetores:


~~~
y <- 6:9
x + y
~~~
{: .r}



~~~
[1]  7  9 11 13
~~~
{: .output}

Cada elemento de `x` foi somado ao elemento correspondente em `y`:


~~~
x:  1  2  3  4
    +  +  +  +
y:  6  7  8  9
---------------
    7  9 11 13
~~~
{: .r}


> ## Desafio 1
>
> Vamos tentar o seguinte desafio na coluna `pop` do conjunto de dados `gapminder`.
>
> Faça uma nova coluna no cojunto de dados `gapminder` que
> contenha a população em milhões de indivíduos.
> Cheque o início e o fim do conjunto de dados para ter certeza
> de que funcionou.
>
> > ## Solução do Desafio 1
> >
> > Vamos tentar o seguinte desafio na coluna `pop` do conjunto de dados `gapminder`.
> >
> > Faça uma nova coluna no cojunto de dados `gapminder` que
> > contenha a população em milhões de indivíduos.
> > Cheque o início e o fim do conjunto de dados para ter certeza
> > de que funcionou.
> >
> > 
> > ~~~
> > gapminder$pop_millions <- gapminder$pop / 1e6
> > head(gapminder)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >       country year      pop continent lifeExp gdpPercap pop_millions
> > 1 Afghanistan 1952  8425333      Asia  28.801  779.4453     8.425333
> > 2 Afghanistan 1957  9240934      Asia  30.332  820.8530     9.240934
> > 3 Afghanistan 1962 10267083      Asia  31.997  853.1007    10.267083
> > 4 Afghanistan 1967 11537966      Asia  34.020  836.1971    11.537966
> > 5 Afghanistan 1972 13079460      Asia  36.088  739.9811    13.079460
> > 6 Afghanistan 1977 14880372      Asia  38.438  786.1134    14.880372
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}


> ## Desafio 2
>
> Em um unico gráfico, plotar a população, 
> em milhares, contra anos, para todos os paises. Não se preocupe em
> identificar cada país.
>
> Repita esta exercício somente para a China, India e
>Indonesia. Novamente, não se preocupe em identificar cada país.
>
> > ## Solução do Desafio 2
> >
> > Relembre suas técnicas plotando a população, em milhões, contra anos.
> >
> > 
> > ~~~
> > ggplot(gapminder, aes(x = year, y = pop_millions)) +
> >  geom_point()
> > ~~~
> > {: .r}
> > 
> > <img src="../fig/rmd-09-ch2-sol-1.png" title="plot of chunk ch2-sol" alt="plot of chunk ch2-sol" style="display: block; margin: auto;" />
> > 
> > ~~~
> > countryset <- c("China","India","Indonesia")
> > ggplot(gapminder[gapminder$country %in% countryset,],
> >        aes(x = year, y = pop_millions)) +
> >   geom_point()
> > ~~~
> > {: .r}
> > 
> > <img src="../fig/rmd-09-ch2-sol-2.png" title="plot of chunk ch2-sol" alt="plot of chunk ch2-sol" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}


Operadores de comparação, operadores lógicos e muitas outras funções também são
vetorizadas:


**Vetores de Comparação**


~~~
x > 2
~~~
{: .r}



~~~
[1] FALSE FALSE  TRUE  TRUE
~~~
{: .output}

**Operadores lógicos**

~~~
a <- x > 3  # or, for clarity, a <- (x > 3)
a
~~~
{: .r}



~~~
[1] FALSE FALSE FALSE  TRUE
~~~
{: .output}

> ## Dica: algumas funções úteis para operadores lógicos
>
> `any()` vai retornar `TRUE` se *any (qualquer)* elemento de um vetor for `TRUE`
> `all()` vai retornar `TRUE` se *all (todos)* todos os elementos do vetor forem `TRUE`
{: .callout}

A maior parte das funções também operam com elementos individuais de um vetor:

**Funções**

~~~
x <- 1:4
log(x)
~~~
{: .r}



~~~
[1] 0.0000000 0.6931472 1.0986123 1.3862944
~~~
{: .output}

Operações vetorizadas também funcionam com elementos individuais em matrizes:


~~~
m <- matrix(1:12, nrow=3, ncol=4)
m * -1
~~~
{: .r}



~~~
     [,1] [,2] [,3] [,4]
[1,]   -1   -4   -7  -10
[2,]   -2   -5   -8  -11
[3,]   -3   -6   -9  -12
~~~
{: .output}


> ## Dica: multiplicação com elementos individuais x multiplicação matricial
>
> Muito importante: o operador `*` realiza a multiplicação com elementos individuais!
> Para uma multiplicação matricial, nós temos que usar o operador `%*%`:
>
> 
> ~~~
> m %*% matrix(1, nrow=4, ncol=1)
> ~~~
> {: .r}
> 
> 
> 
> ~~~
>      [,1]
> [1,]   22
> [2,]   26
> [3,]   30
> ~~~
> {: .output}
> 
> 
> 
> ~~~
> matrix(1:4, nrow=1) %*% matrix(1:4, ncol=1)
> ~~~
> {: .r}
> 
> 
> 
> ~~~
>      [,1]
> [1,]   30
> ~~~
> {: .output}
>
> Para saber mais sobre álgebra matricial, veja [Quick-R reference
> guide](http://www.statmethods.net/advstats/matrix.html)
{: .callout}


> ## Desafio 3
>
> Dada a seguinte matriz:
>
> 
> ~~~
> m <- matrix(1:12, nrow=3, ncol=4)
> m
> ~~~
> {: .r}
> 
> 
> 
> ~~~
>      [,1] [,2] [,3] [,4]
> [1,]    1    4    7   10
> [2,]    2    5    8   11
> [3,]    3    6    9   12
> ~~~
> {: .output}
>
> Escreva o que você acha que vai acontecer se você rodar:
>
> 1. `m ^ -1`
> 2. `m * c(1, 0, -1)`
> 3. `m > c(0, 20)`
> 4. `m * c(1, 0, -1, 2)`
>
> Você obteve os resultados esperados? Senão, consulte o painel de ajuda!
>
> > ## Solução do Desafio 3
> >
> > Dada a seguinte matriz:
> >
> > 
> > ~~~
> > m <- matrix(1:12, nrow=3, ncol=4)
> > m
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >      [,1] [,2] [,3] [,4]
> > [1,]    1    4    7   10
> > [2,]    2    5    8   11
> > [3,]    3    6    9   12
> > ~~~
> > {: .output}
> >
> >
> > Escreva o que você acha que vai acontecer se você rodar:
> >
> > 1. `m ^ -1`
> >
> > 
> > ~~~
> >           [,1]      [,2]      [,3]       [,4]
> > [1,] 1.0000000 0.2500000 0.1428571 0.10000000
> > [2,] 0.5000000 0.2000000 0.1250000 0.09090909
> > [3,] 0.3333333 0.1666667 0.1111111 0.08333333
> > ~~~
> > {: .output}
> >
> > 2. `m * c(1, 0, -1)`
> >
> > 
> > ~~~
> >      [,1] [,2] [,3] [,4]
> > [1,]    1    4    7   10
> > [2,]    0    0    0    0
> > [3,]   -3   -6   -9  -12
> > ~~~
> > {: .output}
> >
> > 3. `m > c(0, 20)`
> >
> > 
> > ~~~
> >       [,1]  [,2]  [,3]  [,4]
> > [1,]  TRUE FALSE  TRUE FALSE
> > [2,] FALSE  TRUE FALSE  TRUE
> > [3,]  TRUE FALSE  TRUE FALSE
> > ~~~
> > {: .output}
> >
> {: .solution}
{: .challenge}


> ## Desafio 4
>
> Nós estamos interessados em saber a soma da
> seguinte sequência de frações:
>
> 
> ~~~
>  x = 1/(1^2) + 1/(2^2) + 1/(3^2) + ... + 1/(n^2)
> ~~~
> {: .r}
>
> Isto seria tedioso demais e impossível de se escrever para valores muito altos
> de n. Use a vetorização para calcular x quando n=100. Qual é a soma quando
> n=10,000?
>
> > ##  Solução do Desafio 4
> >
> > Nós estamos interessados em saber a soma da
> > seguinte sequência de frações:
> >
> > 
> > ~~~
> >  x = 1/(1^2) + 1/(2^2) + 1/(3^2) + ... + 1/(n^2)
> > ~~~
> > {: .r}
> >
> > Isto seria tedioso demais e impossível de se escrever para
> > valores muito altos de n.
> > Use a vetorização para calcular x, quando n=100?
> > Qual é a soma quando n=10,000?
> >
> > 
> > ~~~
> > sum(1/(1:100)^2)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 1.634984
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > sum(1/(1:1e04)^2)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 1.644834
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > n <- 10000
> > sum(1/(1:n)^2)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 1.644834
> > ~~~
> > {: .output}
> >
> > Nós também podemos obter os mesmos resultados usando uma função:
> > 
> > ~~~
> > inverse_sum_of_squares <- function(n) {
> >   sum(1/(1:n)^2)
> > }
> > inverse_sum_of_squares(100)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 1.634984
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > inverse_sum_of_squares(10000)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 1.644834
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > n <- 10000
> > inverse_sum_of_squares(n)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 1.644834
> > ~~~
> > {: .output}
> >
> {: .solution}
{: .challenge}
