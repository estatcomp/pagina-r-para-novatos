---
title: Subsetting Data
teaching: 35
exercises: 15
questions:
- "How can I work with subsets of data in R?"
objectives:
- "To be able to subset vectors, factors, matrices, lists, and data frames"
- "To be able to extract individual and multiple elements: by index, by name, using comparison operations"
- "To be able to skip and remove elements from various data structures."
keypoints:
- "Indexing in R starts at 1, not 0."
- "Access individual values by location using `[]`."
- "Access slices of data using `[low:high]`."
- "Access arbitrary sets of data using `[c(...)]`."
- "Use `which` to select subsets of data based on value."
source: Rmd
---




O R tem v�rios operadores poderosos para subconjuntos e o dom�nio deles ir�
permitir que voc� facilmente utilize opera��es complexas em qualquer tipo de
conjunto de dados.

Existem seis diferentes maneiras de n�s criarmos subconjuntos de qualquer tipo de
objeto, e tr�s diferentes operadores de subconjuntos para as diferentes
estruturas de dados.

Vamos come�ar com o carro chefe do R: vetores at�micos.


~~~
x <- c(5.4, 6.2, 7.1, 4.8, 7.5)
names(x) <- c('a', 'b', 'c', 'd', 'e')
x
~~~
{: .r}



~~~
  a   b   c   d   e 
5.4 6.2 7.1 4.8 7.5 
~~~
{: .output}

Ent�o, agora que n�s criamos um vetor *dummy* para brincar, como n�s temos acesso
ao seu conte�do?

## Acessando elementos usando seus �ndices

Para extrair elementos de um vetor n�s podemos dar seus correspondentes �ndices,
come�ando por um:


~~~
x[1]
~~~
{: .r}



~~~
  a 
5.4 
~~~
{: .output}


~~~
x[4]
~~~
{: .r}



~~~
  d 
4.8 
~~~
{: .output}

Isso pode parecer diferente, mas o operador par de colchetes � uma fun��o. Para
vetores at�micos (e matrizes), isso significa "me passe o *n*-�simo elemento".

N�s podemos pedir por m�ltiplos elementos de uma �nica vez:


~~~
x[c(1, 3)]
~~~
{: .r}



~~~
  a   c 
5.4 7.1 
~~~
{: .output}

Ou fatias do vetor:


~~~
x[1:4]
~~~
{: .r}



~~~
  a   b   c   d 
5.4 6.2 7.1 4.8 
~~~
{: .output}

O operador : cria uma sequ�ncia de n�meros do elemento da esquerda at� o da
direita.


~~~
1:4
~~~
{: .r}



~~~
[1] 1 2 3 4
~~~
{: .output}



~~~
c(1, 2, 3, 4)
~~~
{: .r}



~~~
[1] 1 2 3 4
~~~
{: .output}


N�s podemos pedir pelo mesmo elemento m�ltiplas vezes:


~~~
x[c(1,1,3)]
~~~
{: .r}



~~~
  a   a   c 
5.4 5.4 7.1 
~~~
{: .output}

Se n�s pedirmos por um n�mero fora do vetor, o R retornar� valores faltantes:


~~~
x[6]
~~~
{: .r}



~~~
<NA> 
  NA 
~~~
{: .output}

Este � um vetor de comprimento um contendo um `NA`, cujo nome � tamb�m `NA`.

Se n�s pedirmos pelo elemento de �ndice 0, n�s temos um vetor vazio:


~~~
x[0]
~~~
{: .r}



~~~
named numeric(0)
~~~
{: .output}

> ## Numera��o de vetores no R come�a em 1
>
> Em v�rias linguagens de programa��o (C e python, por exemplo), o primeiro
> elemento de um vetor possu� um indexador igual a 0. Em R, o primeiro elemento
> � 1.
{: .callout}

## Pulando e removendo elementos

Se n�s usarmos como indexador de um vetor um n�mero negativo, o R ir� retornar
todo elemento *exceto* o elemento espec�ficado:


~~~
x[-2]
~~~
{: .r}



~~~
  a   c   d   e 
5.4 7.1 4.8 7.5 
~~~
{: .output}


N�s podemos pular m�ltiplos elementos:


~~~
x[c(-1, -5)]  # ou x[-c(1,5)]
~~~
{: .r}



~~~
  b   c   d 
6.2 7.1 4.8 
~~~
{: .output}

> ## Dica: Ordem de opera��es
>
> Uma experi�ncia em comum para os novatos ocorre quando se tenta pular
> peda�os de um vetor. A maioria das pessoas primeiro tenta negar uma
> sequ�ncia, como por exemplo:
>
> 
> ~~~
> x[-1:3]
> ~~~
> {: .r}
>
> Isto retorna uma esp�cie de erro cr�tico:
>
> 
> ~~~
> Error in x[-1:3]: only 0's may be mixed with negative subscripts
> ~~~
> {: .error}
>
> Mas lembre da ordem das opera��es. : � realmente uma fun��o, ent�o o que
> acontece � que ele pega seu primento argumento como -1, o segundo como 3,
> e ent�o gera a sequ�ncia de n�meros: `c(-1, 0, 1, 2, 3)`.
>
> A solu��o correta � colocar o que a fun��o chama em par�nteses, assim o
> operador `-` � aplicado ao resultado:
>
> 
> ~~~
> x[-(1:3)]
> ~~~
> {: .r}
> 
> 
> 
> ~~~
>   d   e 
> 4.8 7.5 
> ~~~
> {: .output}
{: .callout}


Para remover elementos de um vetor, n�s precisamos atribuir o resultado
novamente na vari�vel:


~~~
x <- x[-4]
x
~~~
{: .r}



~~~
  a   b   c   e 
5.4 6.2 7.1 7.5 
~~~
{: .output}

> ## Desafio 1
>
> Dado o c�digo a seguir:
>
> 
> ~~~
> x <- c(5.4, 6.2, 7.1, 4.8, 7.5)
> names(x) <- c('a', 'b', 'c', 'd', 'e')
> print(x)
> ~~~
> {: .r}
> 
> 
> 
> ~~~
>   a   b   c   d   e 
> 5.4 6.2 7.1 4.8 7.5 
> ~~~
> {: .output}
>
> Forne�a ao menos 3 diferentes comandos que produzem o seguinte resultado:
>
> 
> ~~~
>   b   c   d 
> 6.2 7.1 4.8 
> ~~~
> {: .output}
>
> Depois de voc� encontrar 3 diferentes comandos, compare anota��es com seu colega. Voc�s tiveram diferentes estrat�gias?
>
> > ## Resposta do desafio 1
> >
> > 
> > ~~~
> > x[2:4]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> > 
> > ~~~
> > x[-c(1,5)]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> > 
> > ~~~
> > x[c("b", "c", "d")]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> > 
> > ~~~
> > x[c(2,3,4)]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> >
> {: .solution}
{: .challenge}

## Subconjuntos por nome

N�s podemos extrair elementos atrav�s de seu nome, inv�s do indexador:


~~~
x[c("a", "c")]
~~~
{: .r}



~~~
  a   c 
5.4 7.1 
~~~
{: .output}

Esta � uma maneira muito mais confi�vel de dividir objetos: a posi��o de v�rios
elementos pode frequentemente mudar quando encadeamos opera��es de subconjuntos,
mas os nomes sempre permanecer�o os mesmos!

Infelizmente n�o podemos pular ou remover elementos t�o facilmente.

Para pular (ou remover) um �nico elemento nomeado:


~~~
x[-which(names(x) == "a")]
~~~
{: .r}



~~~
  b   c   d   e 
6.2 7.1 4.8 7.5 
~~~
{: .output}

A fun��o `which` retorna os �ndices de todos os elementos `TRUE` de seu
argumento. Lembre que express�es s�o avaliadas antes de serem passadas para
fun��es. Vamos mostrar passo � passo para ficar claro o que est� acontecendo.

Primeiro isso acontece:


~~~
names(x) == "a"
~~~
{: .r}



~~~
[1]  TRUE FALSE FALSE FALSE FALSE
~~~
{: .output}

O operador condicional � aplicado a todo nome do vetor `x`. Apenas o primeiro
nome � `a` e por isso seu elemento � `TRUE`.

`which` ent�o converte isto para um indexador:


~~~
which(names(x) == "a")
~~~
{: .r}



~~~
[1] 1
~~~
{: .output}



Apenas o primeiro elemento � `TRUE`, ent�o `which` retorna 1. Agora que temos
�ndices podemos pular um elemento, pois temos um index negativo!

Pular m�ltiplos �ndices nomeados � similar, mas usa um operador de compara��o
diferente:


~~~
x[-which(names(x) %in% c("a", "c"))]
~~~
{: .r}



~~~
  b   d   e 
6.2 4.8 7.5 
~~~
{: .output}

O `%in%` vai em cada elemento de seu argumento � esquerda, nesse caso os nomes
de `x`, e pergunta, "Esse elemento ocorre no segundo argumento?"

> ## Desafio 2
>
> Rode o c�digo a seguir para definir o vetor `x` como acima:
>
> 
> ~~~
> x <- c(5.4, 6.2, 7.1, 4.8, 7.5)
> names(x) <- c('a', 'b', 'c', 'd', 'e')
> print(x)
> ~~~
> {: .r}
> 
> 
> 
> ~~~
>   a   b   c   d   e 
> 5.4 6.2 7.1 4.8 7.5 
> ~~~
> {: .output}
>
> Dado este vetor `X`, o que voc� espera que o c�digo a seguir fa�a?
>
>~~~
> x[-which(names(x) == "g")]
>~~~
>{: .r}
>
> Teste este comando e veja o que voc� recebe. � o que voc� esperava?
> Por que n�s recebemos este resultado? (Dica: teste cada parte do comando - esta � uma ferramenta �til de depura��o, *debugging*)
>
> Quais das afirma��es a seguir s�o verdadeiras:
>
> * A) se n�o existem valores `TRUE` passados ao `witch`, um vetor vazio � retornado
> * B) se n�o existem valores `TRUE` passados ao `witch`, uma mensagem de erro � retornada
> * C) `integer` � um vetor vazio
> * D) fazendo um vetor vazio negativo � retornado um vetor "com todo mundo"
> * E) `x[]` d� o mesmo resultado que `x[integer()]`
>
> > ## Resposta do desafio 2
> >
> > A e C est�o corretas.
> >
> > O comando `which` retorna o indexador de todo valor `TRUE` em sua entrada,
> > *input*. O comando `names(x) == "g"` n�o retorna cada valor `TRUE`. Se n�o 
> > existem valores `TRUE` passados ao comando `which`, � retornado um vetor vazio.
> > Transformado este vetor em negativo com um sinal de menos n�o altera seu
> > significado. Pois n�s usamos este vetor vazio para recuperar valores de `x`, o
> > que produz um vetor num�rico vazio. Ele � um vetor `num�rico nomeado` vazio
> > porque o tipo do vetor `x` � "num�rico nomeado" desde que n�s atribu�mos nomes
> > aos valores (tente `str(x)`).
> {: .solution}
{: .challenge}

> ## Dica: Nomes n�o-�nicos
>
> Voc� deve estar consciente de que � poss�vel que m�ltiplos elementos de um vetor
> tenham o mesmo nome. (Para um *data frame*, colunas podem ter o mesmo nome -
> embora o R tente evitar isso - mas o nome das linhas deve ser �nico). Considere
> estes exemplos:
>



































































































