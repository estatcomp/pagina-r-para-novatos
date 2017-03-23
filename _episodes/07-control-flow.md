---
title: Controle de Fluxo
teaching: 45
exercises: 20
questions:
- "Como tomar decisões condicionadas aos dados no R?"
- "Como posso repetir operações no R?"
objectives:
- "Escrever comandos condicionais com `if()` e `else()`."
- "Escrever e entender `for()` loops."
keypoints:
- "Use `if` e `else` para fazer escolhas."
- "Use `for` para repetir operações."
source: Rmd
---



Muitas vezes quando estamos programando queremos controlar o fluxo de nossas ações. Isto pode ser feito definindo ações (comandos) para ocorrer apenas quando uma condição ou um conjunto de condições forem satisfeitas. Uma outra alternativa é definir um conjunto de ações para ocorrer determinado número de vezes. Vale ressaltar que o R utiliza da língua inglesa para seus comandos, assim, a condição "se" é descrita como "if".

Existem várias maneiras de se controlar o fluxo no R. Para sentenças que são condicionadas, as abordagens mais utilizadas são as seguintes:


~~~
# if
if (condição é verdadeira) {
  executar ação
}

# if ... else
if (condição é verdadeira) {
  executar ação
} else {  # se a condição for falsa,
  executar ação alternativa
}
~~~
{: .r}

Digamos, por exemplo, que queremos que o R mostre uma mensagem se uma variável x tem um valor em particular:


~~~
# amostre um número aleatório de uma distribuição de Poisson
# com média (lambda) 8

x <- rpois(1, lambda=8)

if (x >= 10) {
  print("x é maior ou igual a 10")
}

x
~~~
{: .r}



~~~
[1] 8
~~~
{: .output}

Note que você pode não está obtendo a mesma saída que o seu colega, isto porque mesmo sendo números da mesma distribuição, estes são aleatórios.

Vamos definir um *seed*, semente, para que todos nós possamos gerar números "pseudo-aleatórios", e, em seguida, mostrar mais informações:


~~~
set.seed(10)
x <- rpois(1, lambda=8)

if (x >= 10) {
  print("x é maior ou igual a 10")
} else if (x > 5) {
  print("x é maior que 5")
} else {
  print("x é menor que 5")
}
~~~
{: .r}



~~~
[1] "x é maior que 5"
~~~
{: .output}

> ## Dica: Números pseudo-aleatórios
>
> No caso acima, a função `rpois()` gera um número aleatório a partir
> de uma distribuição de Poisson com uma média (ou seja, lambda) 8. A função
> `set.seed()` garante que todas as máquinas irão gerar o mesmo número
> pseudo-aleatórios [(mais sobre números  pseudo-aleatórios)](https://en.wikibooks.org/wiki/R_Programming/Random_Number_Generation).
> Então se definirmos `set.seed(10)`, vemos que x toma o valor 8.
> Você deve obter o mesmo número.
{: .callout}

     
**Importante:** quando R avalia a condição dentro do `if()`, ele está procurando um elemento lógico, isto é, `TRUE` ou `FALSE`. Isso pode causar algumas dores de cabeça para iniciantes. Por exemplo:


~~~
x  <-  4 == 3
if (x) {
  "4 igual a 3"
}
~~~
{: .r}

Como podemos ver, a mensagem não foi mostrada porque o vetor x é `FALSO`


~~~
x <- 4 == 3
x
~~~
{: .r}



~~~
[1] FALSE
~~~
{: .output}

> ## Desafio 1
>
> Use o comando `if()` para mostrar uma mensagem
> reportando se há algum registro de 2002 do
> conjunto de dados `gapminder`. 
> Faça o mesmo para 2012.
>
> > ## Solução do desafio 1
> > Veremos uma solução para o Desafio 1 que não inclue a função `any()`.
> > Primeiro obtemos um vetor lógico que descreve qual elemento do `gapminder$year` é igual a 2002:
> > 
> > ~~~
> > gapminder[(gapminder$year == 2002),]
> > ~~~
> > {: .r}
> > Em seguida, contaremos o número de linhas do data.frame `gapminder`que corresponde a 2002:
> > 
> > ~~~
> > rows2002_number <- nrow(gapminder[(gapminder$year == 2002),])
> > ~~~
> > {: .r}
> > A presença de algum registro de 2002 é equivalente a `rows2002_number` ser um ou mais:
> > 
> > ~~~
> > rows2002_number >= 1
> > ~~~
> > {: .r}
> > Colocando tudo junto, obtemos:
> > 
> > ~~~
> > if(nrow(gapminder[(gapminder$year == 2002),]) >= 1){
> >    print("Registro(s) do ano 2002 encontrado(s).")
> > }
> > ~~~
> > {: .r}
> >
> > Tudo isto pode se feito rapidamento utilizando a função `any()`. A condição logica para isto pode ser expressa por:
> > 
> > ~~~
> > if(any(gapminder$year == 2002)){
> >    print("Registro(s) do ano 2002 encontrado(s).")
> > }
> > ~~~
> > {: .r}
> >
> {: .solution}
{: .challenge}


Alguém obteve uma mensagem de aviso como esta?


~~~
Warning in if (gapminder$year == 2012) {: the condition has length > 1 and
only the first element will be used
~~~
{: .error}

Se a sua condição avalia um vetor com mais de um elemento lógico, a função `if()` ainda será executada, mas irá avaliar apenas  a condição no primeiro elemento. Você precisa ter certeza que sua condição é de comprimento 1.

> ## Dica: `any()` e `all()`
>
> A função `any()` irá retornar `TRUE` se pelo menos
> um valor `TRUE` for encontrado dentro do vetor, caso contrário a função irá retornar `FALSE`.
> Isto pode ser utilizado de uma maneira semelhante ao operador `%in%`.
> A função `all()`, como o nome sugere, irá retornar apenas `TRUE` se todos os valores
> do vetor são verdadeiros.
{: .callout}

## Operações repetidas

Se você quiser interagir sobre um conjunto de valores, quando a ordem da iteração é importante, e realizar a mesma operação em cada um deles, o laço `for()` irá fazer este trabalho. Vimos laços do `for()` nas lições anteriores do *Shell*. Dentro os laços de operações, este é o mais flexível, mas também é o mais difícil de usar corretamente. Evite o uso de laços `for()` a menos que a ordem de iteração seja importante: isto é, o cálculo em cada iteração depende dos resultados das iterações anteriores.

A estrutura básica de um laço `for()` é:


~~~
for(iterador no conjunto de valores){
  faça algo
}
~~~
{: .r}

Por exemplo:


~~~
for(i in 1:10){
  print(i)
}
~~~
{: .r}



~~~
[1] 1
[1] 2
[1] 3
[1] 4
[1] 5
[1] 6
[1] 7
[1] 8
[1] 9
[1] 10
~~~
{: .output}

A sequência `1:10` cria um vetor; você pode interagir sobre qualquer outro vetor também.

Podemos usar o laço `for()` aninhado em outro laço `for()` para iterar sobre duas coisas ao mesmo tempo.


~~~
for(i in 1:5){
  for(j in c('a', 'b', 'c', 'd', 'e')){
    print(paste(i,j))
  }
}
~~~
{: .r}



~~~
[1] "1 a"
[1] "1 b"
[1] "1 c"
[1] "1 d"
[1] "1 e"
[1] "2 a"
[1] "2 b"
[1] "2 c"
[1] "2 d"
[1] "2 e"
[1] "3 a"
[1] "3 b"
[1] "3 c"
[1] "3 d"
[1] "3 e"
[1] "4 a"
[1] "4 b"
[1] "4 c"
[1] "4 d"
[1] "4 e"
[1] "5 a"
[1] "5 b"
[1] "5 c"
[1] "5 d"
[1] "5 e"
~~~
{: .output}

Em vez de imprimir os resultados, podemos escrever a saída do **laço* em um novo objeto.


~~~
output_vector <- c()
for(i in 1:5){
  for(j in c('a', 'b', 'c', 'd', 'e')){
    temp_output <- paste(i, j)
    output_vector <- c(output_vector, temp_output)
  }
}
output_vector
~~~
{: .r}



~~~
 [1] "1 a" "1 b" "1 c" "1 d" "1 e" "2 a" "2 b" "2 c" "2 d" "2 e" "3 a"
[12] "3 b" "3 c" "3 d" "3 e" "4 a" "4 b" "4 c" "4 d" "4 e" "5 a" "5 b"
[23] "5 c" "5 d" "5 e"
~~~
{: .output}

Esta abordagem pode ser útil, mas "aumentar seus resultados" (criando incrementalmente o objeto do resultado) é computacionalmente ineficiente, então o evite quando você estiver interagindo através de uma série de valores.


> ## Dica: Não "aumente seus resultados"
>
> Uma das maiores coisas que atrapalha os novatos em R
> e até mesmo usuários mais experientes, é construir um objeto
> de resultados (vetor, lista, matriz, conjunto de dados) enquanto o seu laço *for* progride.
> Computadores são muito ruins em lidar com isso, então seus cálculos podem ser muito lerdos.
> É muito melhor definir um objeto de resultados vazio antes com as dimensões apropriadas.
> Sendo assim, o resultado final será guardado em uma matriz 
> como mostrado abaixo, crie uma matriz vazia com 5 linhas e
> 5 colunas, em seguida, em cada iteração armazene os resultados no local apropriado.
{: .callout}

Uma melhor maneira é definir o seu objeto (Vazio) de saída antes de preencher os valores. Este exemplo parece ser mais complexo, mas ainda é mais eficiente.


~~~
output_matrix <- matrix(nrow=5, ncol=5)
j_vector <- c('a', 'b', 'c', 'd', 'e')
for(i in 1:5){
  for(j in 1:5){
    temp_j_value <- j_vector[j]
    temp_output <- paste(i, temp_j_value)
    output_matrix[i, j] <- temp_output
  }
}
output_vector2 <- as.vector(output_matrix)
output_vector2
~~~
{: .r}



~~~
 [1] "1 a" "2 a" "3 a" "4 a" "5 a" "1 b" "2 b" "3 b" "4 b" "5 b" "1 c"
[12] "2 c" "3 c" "4 c" "5 c" "1 d" "2 d" "3 d" "4 d" "5 d" "1 e" "2 e"
[23] "3 e" "4 e" "5 e"
~~~
{: .output}

> ## Dica: Laço ``while``
> 
> 
> As vezes você precisará repetir uma operação até uma certa condição ocorrer.
> Isto pode ser feito através do laço `while()`, do português *enquanto*.
> 
> 
> ~~~
> while(essa condção é verdadeira){
>  faça algo
> }
> ~~~
> {: .r}
>
> Como por exemplo, aqui está um laço `while()` 
> que gerar valores da distribuição uniforme (a função `runif()`)
>  entre 0 e 1 até conseguir um valor que seja menor que 0.1.
>
> ~~~
> z <- 1
> while(z > 0.1){
>   z <- runif(1)
>   print(z)
> }
> ~~~
> {: .r}
>
> O laço `while()` nem sempre será apropriada. Você deve ser bastante cauteloso 
> para não acabar em um laço infinito devido a sua condição não ser alcançada.
{: .callout}



> ## Desafio 2
>
> Compare os objetos `output_vector` e `output_vector2`.
> Eles são iguais? Se não, por que não?
> Como você poderia mudar o último bloco de
> códigos para fazer `output_vector2` ser igual a `output_vector`?
>
> > ## Solução do desafio 2
> > Podemos checar se os dois vetores são idênticos usando a função `all()`:
> > 
> > ~~~
> > all(output_vector == output_vector2)
> > ~~~
> > {: .r}
> > No entanto, todos os elementos de `output_vector` podem ser encontrados no `output_vector2`:
> > 
> > ~~~
> > all(output_vector %in% output_vector2)
> > ~~~
> > {: .r}
> > e vice versa:
> > 
> > ~~~
> > all(output_vector2 %in% output_vector)
> > ~~~
> > {: .r}
> > Portanto, os elementos em `output_vector` e `output_vector2` estão ordenados de uma maneira diferente.
> > Isso porque a saída de `as.vector()` são os elementos de uma matriz de entrada pela sua coluna.
> > Olhando `output_matrix`, podemos notar que queremos seus elementos por linha.
> > A solução é transpor a `output_matrix`. Podemos fazer isto usando a função
> > transposta `t()` ou colocando os elementos na ordem certa.
> > A primeira solução requer mudar a original.
> > 
> > ~~~
> > output_vector2 <- as.vector(output_matrix)
> > ~~~
> > {: .r}
> > em
> > 
> > ~~~
> > output_vector2 <- as.vector(t(output_matrix))
> > ~~~
> > {: .r}
> > A segunda solução requer mudar
> > 
> > ~~~
> > output_matrix[i, j] <- temp_output
> > ~~~
> > {: .r}
> > em
> > 
> > ~~~
> > output_matrix[j, i] <- temp_output
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

> ## Desafio 3
>
> Escreva um script que que faça um laço nos dados `gapminder` por continente e mostre se 
> a média da expectativa de vida é menor ou maior do que 50 anos.
>
> > ## Solução do desafio 3
> >
> > **Passo 1**:  Queremos ter certeza que conseguimos extrair todos os valores únicos do vetor continente.
> > 
> > ~~~
> > gapminder <- read.csv("data/gapminder-FiveYearData.csv")
> > unique(gapminder$continent)
> > ~~~
> > {: .r}
> >
> > **Passo 2**: Devemos também fazer um laço em cada um dos continentes e calcular a média da expectativa de vida para cada `subconjunto` dos dados.
> > Podemos fazer isso da seguinte maneira:
> >
> > 1. Faça um laço em cada um dos valores únicos de `continent`
> > 2. Para cada valor de `continent`, crie uma variável temporária que armazene a expectativa de vida para aquele subconjunto,
> > 3. Retorne a expectativa de vida calculada mostrando o resultado:
> >
> > 
> > ~~~
> > for( iContinent in unique(gapminder$continent) ){
> >    tmp <- mean(subset(gapminder, continent==iContinent)$lifeExp)
> >    cat("A média da expectativa de vida em", iContinent, "é", tmp, "\n")
> >    rm(tmp)
> > }
> > ~~~
> > {: .r}
> >
> > **Passo 3**: O Exercício apenas quer que mostre se a média da expectativa de vida é maior ou menor do que 50.
> > Então precisamos adicionar uma condição `if` antes de mostrar o resultado.A função avalia se a média da expectativa de vida calculada é menor ou maior do que um limiar, e mostre uma saída condicionada ao resultado.
> > Precisamos corrigir (3) de cima:
> >
> > Se a expectativa de vida calculada for menor que um valor limiar (50 anos), retorne o continente e a afirmação que a expectativa de vida é menor que o valor limiar, caso contrário retorne o continente e uma afirmação que a expectativa de vida é maior que o valor limiar:
> >
> > 
> > ~~~
> > valorlimiar <- 50
> > > >
> > for( iContinent in unique(gapminder$continent) ){
> >    tmp <- mean(subset(gapminder, continent==iContinent)$lifeExp)
> >    
> >    if(tmp < thresholdValue){
> >        cat("A média da expectativa de vida em"", iContinent, "é menor que", valorlimiar, "\n")
> >    }
> >    else{
> >        cat("A média da expectativa de vida em"", iContinent, "é maior que", valorlimiar, "\n")
> >         } # end if else condition
> >    rm(tmp)
> >    } # Fim do laço
> > > >
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

> ## Desafio 4
>
> Modifique o script do Desafio 3 para fazer um laço em cada país.
> Dessa vez deverá mostrar se a expectativa de vida é menor
> que 50, entre 50 e 70 ou maior que 70.
>
> > ## Solução do desafio 4
> >  Nós modificamos nossa solução do Desafio 3 adicionando 2 valores limiares (limiar inferior e limiar superior) e estendendo as instruções `if-else`:
> >
> > 
> > ~~~
> >  limiarinferior <- 50
> >  limiarsuperior <- 70
> >  
> > for( iCountry in unique(gapminder$country) ){
> >     tmp <- mean(subset(gapminder, country==iCountry)$lifeExp)
> >     
> >     if(tmp < limiarinferior){
> >         cat("A média da expectativa de vida em", iCountry, "é menor que", limiarinferior, "\n")
> >     }
> >     else if(tmp > limiarinferior && tmp < limiarsuperior){
> >         at("A média da expectativa de vida em", iCountry, "está entre", limiarinferior, "e", limiarsuperior, "\n")
> >     }
> >     else{
> >         cat("A média da expectativa de vida em", iCountry, "é maior que", limiarsuperior, "\n")
> >     }
> >     rm(tmp)
> > }
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

> ## Desafio 5 - Avançado
>
> Escreva um script que faça um laço em cada país da base de dados `gapminder`,
> teste se o país começa com "B", e faça um gráfico de linha de Expectativa de vida X Tempo
> se a média da expectativa de vida é menor que 50 anos.
>
> > Solução do desafio 5
> >
> > Vamos usar o comando `grep`, que foi introduzido na lição *Unix Shell* para encontrar quais países começam com "B".
> > Vamos entender como fazer isto primeiro.
> >Seguindo a seção da lição *Unix Shell* somos tentados a tentar o seguinte:
> > 
> > ~~~
> > grep("^B", unique(gapminder$country))
> > ~~~
> > {: .r}
> >
> > Mas quando avaliamos este comando ele retorna os indices da variável fator `país` que começa com "B".
> > Para conseguir os valores, devemos adicionar a opção `value=TRUE` no comando `grep`:
> >
> > 
> > ~~~
> > grep("^B", unique(gapminder$country), value=TRUE)
> > ~~~
> > {: .r}
> >
> > Vamos agora armazenar esses países em uma variável `paisesCandidatos`, e então fazer um laço em cada entrada da variável.
> > Dentro do laço, avaliamos a média da expectativa de vida para cada país, e se a média é menor do que 50 anos. Usamos *base-plot* para plotar a evolução da média da expectativa de vida:
> >
> > 
> > ~~~
> > paisescondidatos <- grep("^B", unique(gapminder$country), value=TRUE)
> > > >
> > for( iCountry in paisescondidatos){
> >     tmp <- mean(subset(gapminder, country==iCountry)$lifeExp)
> >     
> >     if(tmp < valorlimiar){
> >         cat("A média da expectativa de vida em", iCountry, "é menor que", valorlimiar, "plotando o gráfico da expectativa de vida... \n")
> >         
> >         with(subset(gapminder, country==iCountry),
> >                 plot(year,lifeExp,
> >                      type="o",
> >                     main = paste("Expectativa de vida em", iCountry, "ao longo do tempo"),
> >                      ylab = "Expectativa de vida",
> >                      xlab = "Ano"
> >                    ) # Final do gráfico
> >               ) # Final do With
> >     } # Final do laço
> >     rm(tmp)
> >  }```
> > > {: .solution}
> > {: .challenge}
> > ~~~
> > {: .r}
