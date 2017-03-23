---
title: "Explorando Data Frames"
teaching: 20
exercises: 10
questions:
- "Como eu posso manipular um data frame?"
objectives:
- "Ser capaz de adicionar e remover linhas e colunas."
- "Ser capaz de remover linhas com valores `NA`."
- "Ser capaz de juntar dois data frames."
- "Ser capaz de articular o que um `factor`  e como converter entre `factor` e `character`."
- "Estar apto a descobrir propriedades básicas de data frames, incluindo tamanho, classe, tipo das colunas, nomes, e as primeiras linhas."
keypoints:
- "Usar `cbind()` para adicionar uma nova coluna ao data frame."
- "Usar `rbind()` para adicionar uma nova linha ao data frame."
- "Remover linhas de um data frame."
- "Usar `na.omit()` para remover linhas com valor `NA` do data frame."
- "Usar `levels()` e `as.character()` para explorar e manipular fatores"
- "Usae `str()`, `nrow()`, `ncol()`, `dim()`, `colnames()`, `rownames()`, `head()` e `typeof()` para entender a estrutura de um data frame."
- "Ler um arquivo csv com `read.csv()`"
- "Entender o tamanho de um data frame com  `length()`"
---
  


Neste ponto, você viu isso tudo - na última lição, nós visitamos todos os tipos básicos
de dados e estruturas de dados no R. Tudo o que você fará será uma manipulação destas
ferramentas. Mas na maior parte do tempo, a estrela do show será o
data frame - a tabela que nós criamos carregando informação de um arquivo csv. Nesta lição, 
nós iremos aprender algumas coisas a mais sobre trabalhar com data frames.

## Adicionando colunas e linhas a um data frame

Aprendemos anteriormente que colunas em um data frame eram vetores, tal que nossos
dados eram consistentes em tipo por coluna. Tal que, se nós quiséssemos adicionar uma
nova coluna nós precisaríamos começar fazendo um novo vetor:
  
  



~~~
age <- c(2,3,5,12)
cats
~~~
{: .r}



~~~
    coat weight likes_string
1 calico    2.1            1
2  black    5.0            0
3  tabby    3.2            1
~~~
{: .output}

Nós podemos então adicionar como uma nova coluna via:
  

~~~
cats <- cbind(cats, age)
~~~
{: .r}



~~~
Error in data.frame(..., check.names = FALSE): arguments imply differing number of rows: 3, 4
~~~
{: .error}

Por que isso não funcionou? Com certeza, o R quer ver um elemento em nossa nova coluna
para cada linha da tabela:
  

~~~
cats
~~~
{: .r}



~~~
    coat weight likes_string
1 calico    2.1            1
2  black    5.0            0
3  tabby    3.2            1
~~~
{: .output}



~~~
age <- c(4,5,8)
cats <- cbind(cats, age)
cats
~~~
{: .r}



~~~
    coat weight likes_string age
1 calico    2.1            1   4
2  black    5.0            0   5
3  tabby    3.2            1   8
~~~
{: .output}

Agora como adicionar linhas - neste caso, nós vimos da última vez que a linhas
de um data frame são feitas de listas:
  

~~~
newRow <- list("tortoiseshell", 3.3, TRUE, 9)
cats <- rbind(cats, newRow)
~~~
{: .r}



~~~
Warning in `[<-.factor`(`*tmp*`, ri, value = "tortoiseshell"): invalid
factor level, NA generated
~~~
{: .error}

## Fatores

Outra coisa para se prestar atenção surgiu - quando o R cria um fator, ele apenas
permite os que estavam originalmente na tabela quando os dados foram carregados pela
primeira vez, os quais eram 'black', 'calico' e 'tabby' em nosso caso. Qualquer coisa
nova que não se ajustar em uma das categorias é rejeitada como sem sentido (transforma-se NA).

O aviso está dizendo que não conseguimos adicionar 'tortoiseshell' ao nosso
fator *coat*, mas 3.3 (um número), TRUE (um lógico) e 9 (um número) foram 
adicionados com sucesso a *weight*, *likes_string*, e *age*, respectivamente, desde
que esses valores não são fatores e um gato com um 
*coat* 'tortoiseshell', explicitamente adicionar 'tortoiseshell' como um *nível* no fator:
  

~~~
levels(cats$coat)
~~~
{: .r}



~~~
[1] "black"  "calico" "tabby" 
~~~
{: .output}



~~~
levels(cats$coat) <- c(levels(cats$coat), 'tortoiseshell')
cats <- rbind(cats, list("tortoiseshell", 3.3, TRUE, 9))
~~~
{: .r}
Alternativamente, nós podemos modificar uma coluna de fatores para um vetor de caracteres; nós perdemos
o acesso a categorias do fator, mas podemos subsequentemente adicionar qualquer palavra à 
coluna sem necessidade de vigiar os níveis do fator:
  

~~~
str(cats)
~~~
{: .r}



~~~
'data.frame':	5 obs. of  4 variables:
 $ coat        : Factor w/ 4 levels "black","calico",..: 2 1 3 NA 4
 $ weight      : num  2.1 5 3.2 3.3 3.3
 $ likes_string: int  1 0 1 1 1
 $ age         : num  4 5 8 9 9
~~~
{: .output}



~~~
cats$coat <- as.character(cats$coat)
str(cats)
~~~
{: .r}



~~~
'data.frame':	5 obs. of  4 variables:
 $ coat        : chr  "calico" "black" "tabby" NA ...
 $ weight      : num  2.1 5 3.2 3.3 3.3
 $ likes_string: int  1 0 1 1 1
 $ age         : num  4 5 8 9 9
~~~
{: .output}
## Removendo Linhas

Nós sabemos como adicionar linhas e colunas ao nosso data frame no R - mas em nossa
primeira tentativa de adicionar um gato 'casco de tartaruga' ao data frame, nós acidentalmente
adicionamos uma linha errada:
  

~~~
cats
~~~
{: .r}



~~~
           coat weight likes_string age
1        calico    2.1            1   4
2         black    5.0            0   5
3         tabby    3.2            1   8
4          <NA>    3.3            1   9
5 tortoiseshell    3.3            1   9
~~~
{: .output}

Nós podemos pedir um data frame menos a esta linha ofensiva:
  

~~~
cats[-4,]
~~~
{: .r}



~~~
           coat weight likes_string age
1        calico    2.1            1   4
2         black    5.0            0   5
3         tabby    3.2            1   8
5 tortoiseshell    3.3            1   9
~~~
{: .output}
Note que a vírgula com nada após indica que queremos remover a quarta linha inteiramente.

Nota: Nós podemos também remover várias linhas de uma só vez colocando as linhas
em um vetor: `cats[c(-4,-5),]`

Alternativaente, nós podemos tirar todas as linhas com valores `NA`:
  

~~~
na.omit(cats)
~~~
{: .r}



~~~
           coat weight likes_string age
1        calico    2.1            1   4
2         black    5.0            0   5
3         tabby    3.2            1   8
5 tortoiseshell    3.3            1   9
~~~
{: .output}

Vamos reatribuir a saída de `cats`, tal que nossas mudanças sejam permanentes:
  

~~~
cats <- na.omit(cats)
~~~
{: .r}

## Anexando a um data frame

A chave para lembrar quando adicionar dados a um data frame é *colunas são
vetores ou fatores, e linhas são listas.* Podemos também juntar dois data frames
com `rbind`:
  

~~~
cats <- rbind(cats, cats)
cats
~~~
{: .r}



~~~
            coat weight likes_string age
1         calico    2.1            1   4
2          black    5.0            0   5
3          tabby    3.2            1   8
5  tortoiseshell    3.3            1   9
11        calico    2.1            1   4
21         black    5.0            0   5
31         tabby    3.2            1   8
51 tortoiseshell    3.3            1   9
~~~
{: .output}

Mas agora o nome das linhas estão desnecessariamente complicados. Nós podemos
remover o nome das linhas, e R irá renomeá-las sequencialmente:
  

~~~
rownames(cats) <- NULL
cats
~~~
{: .r}



~~~
           coat weight likes_string age
1        calico    2.1            1   4
2         black    5.0            0   5
3         tabby    3.2            1   8
4 tortoiseshell    3.3            1   9
5        calico    2.1            1   4
6         black    5.0            0   5
7         tabby    3.2            1   8
8 tortoiseshell    3.3            1   9
~~~
{: .output}

> ## Desafio 1
>
> Você pode criar um novo data frame direto de dentro do R com a seguinte sintáxe:
> 
> ~~~
> df <- data.frame(id = c('a', 'b', 'c'),
>                  x = 1:3,
>                  y = c(TRUE, TRUE, FALSE),
>                  stringsAsFactors = FALSE)
> ~~~
> {: .r}
> Fazer um data frame que contém as seguintes informação sobre você mesmo:
>
> - Nome (name)
> - Sobrenome (last name)
> - Número da sorte (lucky number)
>
> Então use `rbind` para adicionar um novo registro da pessoa sentada ao teu lado.
> Finalmente, utilize `cbind` para adicionar uma coluna para cada pessoa a responder a questão, "É hora do coffee break?"
>
> > ## Solution to Challenge 1
> > 
> > ~~~
> > df <- data.frame(first = c('Grace'),
> >                  last = c('Hopper'),
> >                  lucky_number = c(0),
> >                  stringsAsFactors = FALSE)
> > df <- rbind(df, list('Marie', 'Curie', 238) )
> > df <- cbind(df, coffeetime = c(TRUE,TRUE))
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

## Exemplo realista
Até agora, você viu o básico de manipulação de data frames com nossos dados sobre gatos;
agora vamos utilizar essas habilidades para resumir um conjunto de dados mais realista.
Vamos ler os dados do conjunto gapminder que baixamos previamente:
  

~~~
gapminder <- read.csv("data/gapminder-FiveYearData.csv")
~~~
{: .r}

> ## Dicas Variadas
>
> * Outro tipo de arquivo que você deve encontrar são os dados separados por tabulação, do inglês tab-separetad value files (.tsv). Para especificar tabulação como um separador, utilize `"\\t"` ou `read.delim()`.
>
> * Arquivo também podem ser baixados diretamente da internet para uma pasta local
> de seu escolha dentro de seu computador utilizando a função `dowbload.file`.
> A função `read.csv` pode ser executada para ler o arquivo baixado, por exemplo:
> 
> ~~~
> download.file("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv", destfile = "data/gapminder-FiveYearData.csv")
> gapminder <- read.csv("data/gapminder-FiveYearData.csv")
> ~~~
> {: .r}
>
> * Alternativamente, você pode também ler arquivos da internet diretamente no R trocando o endereço da pasta por um endereço da web em `read.csv`. Deve-se notar que ao fazer isso nenhuma cópia do arquivo será salva no computador. Por exemplo,
> 
> ~~~
> gapminder <- read.csv("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv")
> ~~~
> {: .r}
>
> * Podemos ler diretamente uma tabela excel sem
> converter em texto usando o pacote [readxl](https://cran.r-project.org/web/packages/readxl/index.html)
{: .callout}

Vamos investigar um pouco o gapminder; a primeira coisa que sempre devemos
fazer é checar como os dados estão organizados com `str`:
  

~~~
str(gapminder)
~~~
{: .r}



~~~
'data.frame':	1704 obs. of  6 variables:
 $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop      : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
 $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap: num  779 821 853 836 740 ...
~~~
{: .output}

Podemos também examinar individualmente as colunas de um data frame com a função `typeof`:


~~~
typeof(gapminder$year)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
typeof(gapminder$country)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
str(gapminder$country)
~~~
{: .r}



~~~
 Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
~~~
{: .output}

Podemos interrogar um data frame por informação sobre suas dimensões;
lembrando que `str(gapminder)` disse que há 1704 observações de 6
variáveis em gapminder, o que você acha que o código a seguir produzirá, e por quê?


~~~
length(gapminder)
~~~
{: .r}



~~~
[1] 6
~~~
{: .output}

Uma aposta justa seria dizer que o tamanho do data frame seria o
número de linhas que ele tem (1704), mas não é o caso; lembre-se, um data frame
é uma *lista de vetores e fatores*:


~~~
typeof(gapminder)
~~~
{: .r}



~~~
[1] "list"
~~~
{: .output}

Quando `length` nos deu 6, é porque gapminder é construído fora por uma lista de 6
colunas. Para obter o número de linhas e colunas do data frame, tente:


~~~
nrow(gapminder)
~~~
{: .r}



~~~
[1] 1704
~~~
{: .output}



~~~
ncol(gapminder)
~~~
{: .r}



~~~
[1] 6
~~~
{: .output}

Ou, ambos de uma só vez:


~~~
dim(gapminder)
~~~
{: .r}



~~~
[1] 1704    6
~~~
{: .output}

Nós vamos possivelmente saber quais os nomes de todas as colunas, então nós
podemos pedir por elas:
  

~~~
colnames(gapminder)
~~~
{: .r}



~~~
[1] "country"   "year"      "pop"       "continent" "lifeExp"   "gdpPercap"
~~~
{: .output}

Neste ponto, é importante perguntar a nós mesmos se a estrutura que o R está reportando
bate com nossas intuições e expectativas; os tipos básicos de dados reportados para cada
coluna fazem sentido? Se não, nós precisamos separar quaisquer problemas agora antes que eles
se tornem más surpresas pelo caminho, usando o que já aprendemos sobre como o R
interpreta dados, e a importância da *consciência estrita* em como armazenar nossos dados

Uma vez que estamos satisfeitos que os tipos de dados e as estruturas parecem 
razoáveis, é hora de começar a explorar os dados propriamente. Confira as primeiras
linhas:


~~~
head(gapminder)
~~~
{: .r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
4 Afghanistan 1967 11537966      Asia  34.020  836.1971
5 Afghanistan 1972 13079460      Asia  36.088  739.9811
6 Afghanistan 1977 14880372      Asia  38.438  786.1134
~~~
{: .output}

Para ter certeza que nossa análise é reproduzível, devemos colocas
o código em um script para poder voltar a ele depois.

> ## Desafio 2
>
> Vá a arquivo -> novo arquivo -> script do R, e escreva o script do R
> para carregar o conjunto gapminder. Coloque-o no diretório `scripts/`
> e adicione-o ao controle de versão.
>
> Rode o script usando a função `source`, usando o endereço do arquivo
> como argumento (ou apertando o botão "source" no RStudio)
>
> > ## Solução do Desafio 2
> > Os conteúdos de `script/load-gapminder.R`:
> >
> >~~~
> > download.file("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv", destfile = "data/gapminder-FiveYearData.csv")
> > gapminder <- read.csv(file = "data/gapminder-FiveYearData.csv")
> >~~~
> >{: .r}
> > Rode o script e carregue os dados de `gapminder` em uma variável:
> >
> >~~~
> > source(file = "scripts/load-gapminder.R")
> >~~~
> >{: .r}
> {: .solution}
{: .challenge}

> ## Desafio 3
>
> Leia a saída de `str(gapminder)` novamente;
> dessa vez, use o que você aprendeu sobre fatores, listas e vetores,
> bem como a saída de funções como `colnames` e `dim`
> para explicar tudo o que `str` imprimiu para gapminder significa.
> Se houver partes que você não consegue interpretar, discuta com seus amigos!
>
> > ## Solução do Desafio 3
> >
> > O objeto `gapminder` é um data frame com as colunas
> > - `country` e `continent` são fatores factors.
> > - `year` é um vetor inteiro.
> > - `pop`, `lifeExp`, e `gdpPercap` são vetores numéricos.
> >
> {: .solution}
{: .challenge}
