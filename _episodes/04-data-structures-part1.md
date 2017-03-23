---
title: "Estruturas de dados"
teaching: 40
exercises: 15
questions:
- "Como eu posso ler dados no R?"
- "Quais sÃ£o os tipos bÃ¡sicos de dados no R?"
- "Como eu represento informaÃ§Ãµes categÃ³ricas em R?"
objectives:
- "Conhecer os diferentes tipos de dados."
- "ComeÃ§ar a explorar data frames, e entender como eles estÃ£o relacionados a vetores, fatores e listas."
- "Ser capaz de perguntar ao R questÃµes sobre o tipo, classe e estrutura de um objeto."
keypoints:
- "Usar `read.csv` para ler dados tabulares em R."
- "Os tipos bÃ¡sicos de dados em R sÃ£o double, inteiro, complexo, lÃ³gico e caractere."
- "Usar fatores para representar categorias em R."
---



Uma das caracterÃ?sticas mais poderosas do R Ã© sua capacidade de lidar com dados em tabelas - como vocÃª jÃ¡ deve ter visto em uma planilha em CSV. Vamos comeÃ§ar fazendo um banco de dados para testes na sua pasta `data/`, chamado _ directory, called `feline-data.csv`:


~~~
coat,weight,likes_string
calico,2.1,1
black,5.0,0
tabby,3.2,1
~~~
{: .r}

> ## Dica: Editando arquivos de texto em R
>
> Alternativamente, vocÃª pode criar `data/feline-data.csv` usando um editor de texto
> (Nano), ou dentro do RStudio com o item do menu **Arquivo -> Novo Arquivo -> Arquivo de texto**.
{: .callout}



VocÃª pode carregar isso no R com o seguinte comando:


~~~
cats <- read.csv(file = "data/feline-data.csv")
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

A funÃ§Ã£o `read.csv` Ã© utilizada para ler dados de tabelas armazenados em um arquivo de texto onde as colunas sÃ£o delimitadas por vÃ?rgulas (csv = comma separated values, i.e., valores separados por vÃ?rgulas). Tabs tambÃ©m sÃ£o comumente usados para separar colunas - se os seus dados estÃ£o neste formato vocÃª pode usar a funÃ§Ã£o `read.delim`. Se as colunas nos seus dados sÃ£o delimitadas por um outro caractere alÃ©m de vÃ?rgulas ou tabs, vocÃª pode usar a funÃ§Ã£o `read.table`, que Ã© mais geral e flexÃ?vel.


JÃ¡ podemos comeÃ§ar a explorar o nosso banco de dados, imprimindo colunas especificando elas com o operador `$`:


~~~
cats$weight
~~~
{: .r}



~~~
[1] 2.1 5.0 3.2
~~~
{: .output}



~~~
cats$coat
~~~
{: .r}



~~~
[1] calico black  tabby 
Levels: black calico tabby
~~~
{: .output}

NÃ³s podemos fazer outras operaÃ§Ãµes nas colunas:


~~~
## Digamos que nÃ³s descobrimos que a escala de quilos tem dois Kg a menos:
cats$weight + 2
~~~
{: .r}



~~~
[1] 4.1 7.0 5.2
~~~
{: .output}



~~~
paste("My cat is", cats$coat)
~~~
{: .r}



~~~
[1] "My cat is calico" "My cat is black"  "My cat is tabby" 
~~~
{: .output}

Mas e se fizermos


~~~
cats$weight + cats$coat
~~~
{: .r}



~~~
Warning in Ops.factor(cats$weight, cats$coat): '+' not meaningful for
factors
~~~
{: .error}



~~~
[1] NA NA NA
~~~
{: .output}

Entendendo o que aconteceu aqui Ã© a chave para analisar dados em R de maneira satisfatÃ³ria.

## Tipos de Dados

Se vocÃª imaginasse que o Ãºltimo comando fosse retornar um erro porque `2.1` mais `"black"` nÃ£o faz sentido, vocÃª estava certo - e vocÃª jÃ¡ tem alguma intuiÃ§Ã£o para um importante conceito em programaÃ§Ã£o chamado *tipos de dados*. Podemos perguntar que tipo de dado algo Ã©:


~~~
typeof(cats$weight)
~~~
{: .r}



~~~
[1] "double"
~~~
{: .output}

Existem 5 tipos principais de dados:`duplo`, `inteiro`, `complexo`, `lÃ³gico` e `caracter`.


~~~
typeof(3.14)
~~~
{: .r}



~~~
[1] "double"
~~~
{: .output}



~~~
typeof(1L) # O sufixo L forÃ§a o nÃºmero a ser um inteiro, uma vez que o padrÃ£o do R usa nÃºmeros fltuantes
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
typeof(1+1i)
~~~
{: .r}



~~~
[1] "complex"
~~~
{: .output}



~~~
typeof(TRUE)
~~~
{: .r}



~~~
[1] "logical"
~~~
{: .output}



~~~
typeof('banana')
~~~
{: .r}



~~~
[1] "character"
~~~
{: .output}

NÃ£o importa quÃ£o complicada sua analize se torne, todos os dados em R sÃ£o interpretados como um desses tipos bÃ¡sicos de dados.Esse rigor tem algumas consequÃªncias importantes. 
Um usuÃ¡rio adicionou detalhes sobre outro gato. Essas informaÃ§Ãµes estÃ£o no aquivo
`data/feline-data_v2.csv`.



~~~
file.show("data/feline-data_v2.csv")
~~~
{: .r}


~~~
coat,weight,likes_string
calico,2.1,1
black,5.0,0
tabby,3.2,1
tabby,2.3 or 2.4,1
~~~
{: .r}

Carregue os novos dados sobre os gatos como anteriormente, e cheque que tipos de dados acharemos na
coluna`weight`: 


~~~
cats <- read.csv(file="data/feline-data_v2.csv")
typeof(cats$weight)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}


Ah nÃ£o, nossos pesos nÃ£o estÃ£o mais no tipo double! Se tentarmos usar a mesma lÃ³gica que usamos antes, teremos problemas: 


~~~
cats$weight + 2
~~~
{: .r}



~~~
Warning in Ops.factor(cats$weight, 2): '+' not meaningful for factors
~~~
{: .error}



~~~
[1] NA NA NA NA
~~~
{: .output}

O que aconteceu? Quando o R lÃª um csv nessas tabelas, ele insiste que tudo na coluna seja do mesmo tipo bÃ¡sico; se ele nÃ£o pode entender *tudo* na coluna como double, entÃ£o *ninguÃ©m* na coluna serÃ¡ double. A tabela em que o R carregou os dados dos gatos Ã© algo chamado *data.frame*, e esse Ã© o nosso primeiro exemplo de algo chamado *estrutura de dados* - que Ã©, a estrutura em que o R sabe construir os tipos de dados bÃ¡sicos. 

Conseguimos ver que isso Ã© um *data.frame* adicionando a funÃ§Ã£o `class` nele:


~~~
class(cats)
~~~
{: .r}



~~~
[1] "data.frame"
~~~
{: .output}

Para utlizarmos com sucesso nossos dados no R, precisamos entender o que as estrutaras bÃ¡sicas de dados sÃ£o, e como elas se comportam.Por hora, vamos remover aquela linha extra dos nossos dados e recarregÃ¡-lo, enquanto aprofundamos a investigaÃ§Ã£o desse comportamento:

feline-data.csv:

```
coat,weight,likes_string
calico,2.1,1
black,5.0,0
tabby,3.2,1
```

E de volta ao RStudio:


~~~
cats <- read.csv(file="data/feline-data.csv")
~~~
{: .r}




## Vetores e CoerÃ§Ã£o de Tipo

Para melhor entender esse comportamento, vamos conhecer mais outra estrutura de dados:
O *vetor*.


~~~
my_vector <- vector(length = 3)
my_vector
~~~
{: .r}



~~~
[1] FALSE FALSE FALSE
~~~
{: .output}

Um vetor em R Ã© essencialmente uma lista de coisas, com a condiÃ§Ã£o especial que *tudo  no vetor precisa ser do mesmo tipo bÃ¡sico de dados*. Se vocÃª nÃ£o escolher o tipo de dados, ele serÃ¡ padronizado como `logico`; ou, vocÃª pode declarar um vetor vazio do tipo que vocÃª quiser.



~~~
another_vector <- vector(mode='character', length=3)
another_vector
~~~
{: .r}



~~~
[1] "" "" ""
~~~
{: .output}

VocÃª pode checar se algo Ã© um vetor:


~~~
str(another_vector)
~~~
{: .r}



~~~
 chr [1:3] "" "" ""
~~~
{: .output}

Essa saÃ?da um tanto enigmÃ¡tica para esse comando indica o tipo bÃ¡sico de dados encontrados no vetor - nesse caso `chr`, caracter; uma indicaÃ§Ã£o do nÃºmero de coisas no vetor - na realidade, os Ã?ndices do vetor, nesse caso `[1:3]`; e alguns exemplos do que estÃ¡ no vetor - nesse caso uma sÃ©rie vazia de caracteres. Se similarmente fizermos


~~~
str(cats$weight)
~~~
{: .r}



~~~
 num [1:3] 2.1 5 3.2
~~~
{: .output}

Veremos que isto Ã© um vetor, tambÃ©m - *as colunas de dados que carregamos nos data.frames do R sÃ£o todos vetores*, e essa Ã© a raiz do porque que o R forÃ§a tudo em uma coluna a ser do mesmo tipo bÃ¡sico de dados. 

> ## DiscussÃ£o 1
>
> Porque o R Ã© tÃ£o rigoroso sobre o que colocamos em nossas colunas de dados?
> Como isso nos ajuda?
>
> > ## DiscussÃ£o 1
> >
> > Mantendo tudo na culuna o mesmo, nos possibilitamos fazer simples suposiÃ§Ãµes > >a respeito de nossos dados; se vocÃª pode interpretar uma entrada na coluna 
> >como um nÃºmero, entÃ£o pode interpretar *todos* eles como nÃºmeros, e entÃ£o nÃ£o
> >precisaremos checar toda vez. Essa consistÃªncia, como usar consistentemente o > >mesmo separador nos nossos aquivos de dados, Ã© o que as pessoas querem dizer 
> >quando falam em *dados limpos*; no longo prazo essa consistencia contribui 
> >para tornar nossa vida mais fÃ¡cil no R. 
> {: .solution}
{: .discussion}

VocÃª tambÃ©m pode criar vetores com conteudos explÃ?citos com a funÃ§Ã£o combine:


~~~
combine_vector <- c(2,6,3)
combine_vector
~~~
{: .r}



~~~
[1] 2 6 3
~~~
{: .output}

Dado o que aprendemos atÃ© agora, o que vocÃª acha que irÃ¡ produzir o seguinte?


~~~
quiz_vector <- c(2,6,'3')
~~~
{: .r}

Isso Ã© algo chamado *coerÃ§Ã£o de tipo*, e Ã© a fonte de muitas surpesas e a razÃ£o de precisarmos estar alertas ao tipo bÃ¡sico de dados e como o R irÃ¡ interpretÃ¡-los.Quando o R encontra uma mistura de tipos (aqui, numÃ©rico e caracter) para combinar em um Ãºnico vetor, ele irÃ¡ forÃ§Ã¡-los todos para serem do mesmo tipo. Considere:


~~~
coercion_vector <- c('a', TRUE)
coercion_vector
~~~
{: .r}



~~~
[1] "a"    "TRUE"
~~~
{: .output}



~~~
another_coercion_vector <- c(0, TRUE)
another_coercion_vector
~~~
{: .r}



~~~
[1] 0 1
~~~
{: .output}

A regra de coerÃ§Ã£o segue: `logico` -> `inteiro` -> `numerico` -> `complexo` ->
`caracter`, onde -> pode ser lido como *foram transformados em*. VocÃª pode forÃ§ar a coerÃ§Ã£o contra essa ordem usando funÃ§Ãµes `as.`:


~~~
character_vector_example <- c('0','2','4')
character_vector_example
~~~
{: .r}



~~~
[1] "0" "2" "4"
~~~
{: .output}



~~~
character_coerced_to_numeric <- as.numeric(character_vector_example)
character_coerced_to_numeric
~~~
{: .r}



~~~
[1] 0 2 4
~~~
{: .output}



~~~
numeric_coerced_to_logical <- as.logical(character_coerced_to_numeric)
numeric_coerced_to_logical
~~~
{: .r}



~~~
[1] FALSE  TRUE  TRUE
~~~
{: .output}

Como vocÃª pode ver, algumas coisas surpreendentes podem acontecer quando o R forÃ§a algum tipo bÃ¡sico de dados em outro! Pormenores da coerÃ§Ã£o de tipo a parte:  se seus dados nÃ£o se parecem com o que vocÃª pensava que eles deveria se parecer, a coerÃ§Ã£o de tipo pode ser a culpada; tenha certeza qe tudo no seus vetores Ã© do mesmo tipo e nas suas colunas de data.frames, ou vocÃª terÃ¡ supresas desagradÃ¡veis!

Mas a coerÃ§Ã£o tambÃ©m pode ser bastante Ãºtil! Por exemplo, nos nossos dados `cats`
`likes_string` Ã© numÃ©rico, mas nÃ³s sabemos que os 1s and 0s representam na realidade `VERDADEIRO` e `FALSO` (uma maneira comum de representÃ¡-los). NÃ³s devemos usar o tipo de dados `lÃ³gico` aqui, que tem dois estados: `VERDADEIRO` ou `FALSO`, que Ã© exatamente o que nossos dados representam. NÃ³s podemos 'coagir' esssa coluna para que seja`lÃ³gica` ussando a funÃ§Ã£o `as.logical`:


~~~
cats$likes_string
~~~
{: .r}



~~~
[1] 1 0 1
~~~
{: .output}



~~~
cats$likes_string <- as.logical(cats$likes_string)
cats$likes_string
~~~
{: .r}



~~~
[1]  TRUE FALSE  TRUE
~~~
{: .output}

A funÃ§Ã£o `c()` tambÃ©m irÃ¡ anexar coisas a um vetor existente:


~~~
ab_vector <- c('a', 'b')
ab_vector
~~~
{: .r}



~~~
[1] "a" "b"
~~~
{: .output}



~~~
combine_example <- c(ab_vector, 'SWC')
combine_example
~~~
{: .r}



~~~
[1] "a"   "b"   "SWC"
~~~
{: .output}

VocÃª tambÃ©m pode fazer sÃ©ries de nÃºmeros:


~~~
mySeries <- 1:10
mySeries
~~~
{: .r}



~~~
 [1]  1  2  3  4  5  6  7  8  9 10
~~~
{: .output}



~~~
seq(10)
~~~
{: .r}



~~~
 [1]  1  2  3  4  5  6  7  8  9 10
~~~
{: .output}



~~~
seq(1,10, by=0.1)
~~~
{: .r}



~~~
 [1]  1.0  1.1  1.2  1.3  1.4  1.5  1.6  1.7  1.8  1.9  2.0  2.1  2.2  2.3
[15]  2.4  2.5  2.6  2.7  2.8  2.9  3.0  3.1  3.2  3.3  3.4  3.5  3.6  3.7
[29]  3.8  3.9  4.0  4.1  4.2  4.3  4.4  4.5  4.6  4.7  4.8  4.9  5.0  5.1
[43]  5.2  5.3  5.4  5.5  5.6  5.7  5.8  5.9  6.0  6.1  6.2  6.3  6.4  6.5
[57]  6.6  6.7  6.8  6.9  7.0  7.1  7.2  7.3  7.4  7.5  7.6  7.7  7.8  7.9
[71]  8.0  8.1  8.2  8.3  8.4  8.5  8.6  8.7  8.8  8.9  9.0  9.1  9.2  9.3
[85]  9.4  9.5  9.6  9.7  9.8  9.9 10.0
~~~
{: .output}

Podemos fazer algumas perguntas a respeito de vetores:


~~~
sequence_example <- seq(10)
head(sequence_example, n=2)
~~~
{: .r}



~~~
[1] 1 2
~~~
{: .output}



~~~
tail(sequence_example, n=4)
~~~
{: .r}



~~~
[1]  7  8  9 10
~~~
{: .output}



~~~
length(sequence_example)
~~~
{: .r}



~~~
[1] 10
~~~
{: .output}



~~~
class(sequence_example)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
typeof(sequence_example)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}

Por fim, vocÃª pode nomear os elementos em seu vetor:


~~~
my_example <- 5:8
names(my_example) <- c("a", "b", "c", "d")
my_example
~~~
{: .r}



~~~
a b c d 
5 6 7 8 
~~~
{: .output}



~~~
names(my_example)
~~~
{: .r}



~~~
[1] "a" "b" "c" "d"
~~~
{: .output}

> ## Desafio 1
>
> Comece criando um vetor com os nÃºmeros 1 a 26.
> Multiplique o vetor por 2, e dÃª ao vetor resultante nomes de A a Z (dica: 
> existe um atributo em vetores chamado `LETTERS`)

> > ## SoluÃ§Ã£o do Desafio 1
> >
> > 
> > ~~~
> > x <- 1:26
> > x <- x * 2
> > names(x) <- LETTERS
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}


## Data Frames

Dizems que colunas nos data.frames sÃ£o vetores:


~~~
str(cats$weight)
~~~
{: .r}



~~~
 num [1:3] 2.1 5 3.2
~~~
{: .output}



~~~
str(cats$likes_string)
~~~
{: .r}



~~~
 logi [1:3] TRUE FALSE TRUE
~~~
{: .output}

Isso faz sentido. Mas e quanto a


~~~
str(cats$coat)
~~~
{: .r}



~~~
 Factor w/ 3 levels "black","calico",..: 2 1 3
~~~
{: .output}

## Factors

Outro tipo importante de estrutura de dados Ã© chamado de *factor*. Fatores usualmente se parecem com dados de caracter, mas sÃ£o tipicamente utilizados para representar informaÃ§Ã£o categÃ³rica. Por exemplo, vamos criar um vetor rotulando coloraÃ§Ãµes de gato para todos os gatos em nosso estudo:



~~~
coats <- c('tabby', 'tortoiseshell', 'tortoiseshell', 'black', 'tabby')
coats
~~~
{: .r}



~~~
[1] "tabby"         "tortoiseshell" "tortoiseshell" "black"        
[5] "tabby"        
~~~
{: .output}



~~~
str(coats)
~~~
{: .r}



~~~
 chr [1:5] "tabby" "tortoiseshell" "tortoiseshell" "black" ...
~~~
{: .output}


Podemos transformar um vetor em um fator assim:


~~~
CATegories <- factor(coats)
class(CATegories)
~~~
{: .r}



~~~
[1] "factor"
~~~
{: .output}



~~~
str(CATegories)
~~~
{: .r}



~~~
 Factor w/ 3 levels "black","tabby",..: 2 3 3 1 2
~~~
{: .output}


Agora o R notou que existem trÃªs categorias possÃ?veis em nossos dados - mas isso
tambÃ©m fez algo surpreendente; Em vez de imprimir as sequÃªncias que nÃ³s demos,
temos um monte de nÃºmeros.O R substituiu nossas categorias por Ã?ndices numerdos:


~~~
typeof(coats)
~~~
{: .r}



~~~
[1] "character"
~~~
{: .output}



~~~
typeof(CATegories)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}

> ## Desafio 2
>

> Existe um fator no nosso data.frame`cats`? Qual o nome dele?
> Tente usar `? Read.csv` para descobrir como manter as colunas de texto como
> vetores  de caracteres em vez de fatores; EntÃ£o escreva um comando ou dois para
> mostrar que o fator em `cats` Ã© realmente um vetor de caracteres quando
> carregado dessa maneira.

> > ## SoluÃ§Ã£o do Desafio 2
> >
> > Uma soluÃ§Ã£o Ã© usar o argumento `stringAsFactors`:
> >
> > 
> > ~~~
> > cats <- read.csv(file="data/feline-data.csv", stringsAsFactors=FALSE)
> > str(cats$coat)
> > ~~~
> > {: .r}
> >
> > Outra soluÃ§Ã£o Ã© usar o argumento `colClasses`
> > que permite um controle mais fino.
> >
> > 
> > ~~~
> > cats <- read.csv(file="data/feline-data.csv", colClasses=c(NA, NA, "character"))
> > str(cats$coat)
> > ~~~
> > {: .r}
> >
> > Nota: os alunos menos experientes acham os arquivos de ajuda difÃ?ceis de entender; Certifique-se de deixÃ¡-los saber que isso Ã© comum, e incentivÃ¡-los a darem seu melhor palpite com base no significado semÃ¢ntico, mesmo que eles nÃ£o tenham certeza..
> {: .solution}
{: .challenge}


Nas funÃ§Ãµes de modelagem, Ã© importante saber quais sÃ£o os nÃ?veis de linha de
base. Este Ã© considerado o primeiro fator, mas por padrÃ£o os fatores sÃ£o
rotulados em ordem alfabÃ©tica. VocÃª pode alterar isso especificando os nÃ?veis:



~~~
mydata <- c("case", "control", "control", "case")
factor_ordering_example <- factor(mydata, levels = c("control", "case"))
str(factor_ordering_example)
~~~
{: .r}



~~~
 Factor w/ 2 levels "control","case": 2 1 1 2
~~~
{: .output}


Neste caso, explicitamente dissemos ao R que "controle" deve ser representado por
1, e "Case" por 2. Esta designaÃ§Ã£o pode ser muito importante para a interpretaÃ§Ã£o
dos resultados de modelos estatÃ?sticos!

## Listas


Outra estrutura de dados que vocÃª vai querer em seu saco de truques Ã© a `lista`.
Uma lista Ã© mais simples em alguns aspectos do que os outros tipos, porque vocÃª
pode colocar qualquer coisa que vocÃª quiser nele:


~~~
list_example <- list(1, "a", TRUE, 1+4i)
list_example
~~~
{: .r}



~~~
[[1]]
[1] 1

[[2]]
[1] "a"

[[3]]
[1] TRUE

[[4]]
[1] 1+4i
~~~
{: .output}



~~~
another_list <- list(title = "Research Bazaar", numbers = 1:10, data = TRUE )
another_list
~~~
{: .r}



~~~
$title
[1] "Research Bazaar"

$numbers
 [1]  1  2  3  4  5  6  7  8  9 10

$data
[1] TRUE
~~~
{: .output}


Agora podemos entender algo um pouco surpreendente em nosso data.frame; O que
acontece se rodarmos:


~~~
typeof(cats)
~~~
{: .r}



~~~
[1] "list"
~~~
{: .output}

Vemos que os data.frames parecem listas - isto Ã© porque um data.frame Ã© realmente
uma lista de vetores e fatores, como eles tÃªm que ser - para manter essas colunas
que sÃ£o uma mistura de vetores e fatores, o data.frame precisa de algo um pouco
mais flexÃ?vel do que um vetor para colocar todas as colunas em uma tabela
familiar. Em outras palavras, um `data.frame` Ã© uma lista especial em que todos
os vetores devem ter o mesmo comprimento.

Em nosso exemplo de `gatos`, temos um nÃºmero inteiro, um duplo e uma variÃ¡vel
lÃ³gica. Como jÃ¡ vimos, cada coluna do data.frame Ã© um vetor.


~~~
cats$coat
~~~
{: .r}



~~~
[1] calico black  tabby 
Levels: black calico tabby
~~~
{: .output}



~~~
cats[,1]
~~~
{: .r}



~~~
[1] calico black  tabby 
Levels: black calico tabby
~~~
{: .output}



~~~
typeof(cats[,1])
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
str(cats[,1])
~~~
{: .r}



~~~
 Factor w/ 3 levels "black","calico",..: 2 1 3
~~~
{: .output}


Cada linha Ã© uma * observaÃ§Ã£o * de diferentes variÃ¡veis, ela prÃ³pria Ã© um
data.frame, e assim, pode ser composto de elementos de diferentes tipos


~~~
cats[1,]
~~~
{: .r}



~~~
    coat weight likes_string
1 calico    2.1         TRUE
~~~
{: .output}



~~~
typeof(cats[1,])
~~~
{: .r}



~~~
[1] "list"
~~~
{: .output}



~~~
str(cats[1,])
~~~
{: .r}



~~~
'data.frame':	1 obs. of  3 variables:
 $ coat        : Factor w/ 3 levels "black","calico",..: 2
 $ weight      : num 2.1
 $ likes_string: logi TRUE
~~~
{: .output}

> ## Desafio 3
>
> HÃ¡ vÃ¡rias maneiras sutilmente diferentes de chamar variÃ¡veis, observaÃ§Ãµes e
> elementos dos data.frames:
>
> - `cats[1]`
> - `cats[[1]]`
> - `cats$coat`
> - `cats["coat"]`
> - `cats[1, 1]`
> - `cats[, 1]`
> - `cats[1, ]`
>

> Experimente estes exemplos e explique o que Ã© devolvido por cada um.
>
> * Dica: * Use a funÃ§Ã£o `typeof ()` para examinar o que Ã© retornado em cada
> caso.
>
> > ## SoluÃ§Ã£o do Desafio 3
> > 
> > ~~~
> > cats[1]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >     coat
> > 1 calico
> > 2  black
> > 3  tabby
> > ~~~
> > {: .output}

> > Podemos pensar em um data frame como uma lista de vetores. O colchetes `[1]`
> > retorna a primeira fatia da lista, como outra lista. Neste caso, Ã© a primeira
> > coluna do data frame.
> > 
> > ~~~
> > cats[[1]]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] calico black  tabby 
> > Levels: black calico tabby
> > ~~~
> > {: .output}
> > O colchete duplo `[[1]]` retorna o conteÃºdo do item da lista. Nesse caso
> > Ã© o conteÃºdo da primeira coluna, um _vetor_ do tipo _fator_.
> > 
> > ~~~
> > cats$coat
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] calico black  tabby 
> > Levels: black calico tabby
> > ~~~
> > {: .output}
> > Este exemplo usa o caractere `$` para endereÃ§ar itens por nome. _coat_ Ã© a
> > primeira coluna do data frame, novamente um _vetor_ do tipo _fator_.
> > 
> > ~~~
> > cats["coat"]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >     coat
> > 1 calico
> > 2  black
> > 3  tabby
> > ~~~
> > {: .output}
> > Aqui estamos usando o colchete simples `["coat"]` substituindo o Ã?ndice
> > numÃ©rico pelo nome da coluna. Como no exemplo 1, o objeto de retorno Ã© uma
> > _lista_.
> > 
> > ~~~
> > cats[1, 1]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] calico
> > Levels: black calico tabby
> > ~~~
> > {: .output}
> > Este exemplo usa um colchete Ãºnico, mas desta vez nÃ³s fornecemos as
> > coordenadas de linha e coluna. O objeto retornado Ã© o valor na linha 1,
> > coluna 1. O objeto Ã© um _inteiro_ mas porque Ã© parte de um _vetor_ do tipo
> > _fator_, o R exibe o rÃ³tulo "calico" associado com o valor inteiro
> > 
> > ~~~
> > cats[, 1]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] calico black  tabby 
> > Levels: black calico tabby
> > ~~~
> > {: .output}
> > Como no exemplo anterior, usamos colchetes simples e fornecemos coordenadas
> > de  linhas e colunas. A coordenada da linha nÃ£o Ã© especificada, o R
> > interpreta o valor faltante como todos os elementos deste _vetor_ _coluna_.
> > 
> > ~~~
> > cats[1, ]
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> >     coat weight likes_string
> > 1 calico    2.1         TRUE
> > ~~~
> > {: .output}
> > Novamente, usamos o colchete Ãºnico com coordenadas de linha e coluna. A
> > coordenada da coluna nÃ£o Ã© especificada. O valor de retorno Ã© uma _lista_
> > contendo todos os valores na primeira linha.
> {: .solution}
{: .challenge}

## Matrizes

Por Ãºltimo mas nÃ£o menos importante Ã© a matriz. Podemos declarar uma matriz cheia
de zeros:


~~~
matrix_example <- matrix(0, ncol=6, nrow=3)
matrix_example
~~~
{: .r}



~~~
     [,1] [,2] [,3] [,4] [,5] [,6]
[1,]    0    0    0    0    0    0
[2,]    0    0    0    0    0    0
[3,]    0    0    0    0    0    0
~~~
{: .output}

E semelhante a outras estruturas de dados, podemos perguntar coisas sobre a nossa
matriz:


~~~
class(matrix_example)
~~~
{: .r}



~~~
[1] "matrix"
~~~
{: .output}



~~~
typeof(matrix_example)
~~~
{: .r}



~~~
[1] "double"
~~~
{: .output}



~~~
str(matrix_example)
~~~
{: .r}



~~~
 num [1:3, 1:6] 0 0 0 0 0 0 0 0 0 0 ...
~~~
{: .output}



~~~
dim(matrix_example)
~~~
{: .r}



~~~
[1] 3 6
~~~
{: .output}



~~~
nrow(matrix_example)
~~~
{: .r}



~~~
[1] 3
~~~
{: .output}



~~~
ncol(matrix_example)
~~~
{: .r}



~~~
[1] 6
~~~
{: .output}

> ## Desafio 4
>
> Qual vocÃª acha que serÃ¡ o resultado de
> Tente.
> VocÃª acertou? Porque / Porque nÃ£o?
>
> > ## SoluÃ§Ã£o do Desafio 4
> >
> > Qual vocÃª acha que serÃ¡ o resultado de
> > `length(matrix_example)`?
> >
> > 
> > ~~~
> > matrix_example <- matrix(0, ncol=6, nrow=3)
> > length(matrix_example)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] 18
> > ~~~
> > {: .output}
> >
> > Porque uma matriz Ã© um vetor com atributos de dimensÃ£o adicionados, `length`
> > fornece o nÃºmero total de elementos na matriz.
> {: .solution}
{: .challenge}


> ## Desafio 5
>
> Crie outra matriz, dessa vez contendo os nÃºmeros de 1 a 50,
> com 5 colunas e 10 linhas.
> Sua funÃ§Ã£o`matrix` preencheu sua matriz por colunas ou por linhas, esse Ã© o
> comportamento padrÃ£o?
> Veja se vocÃª descobre como mudar isto.
> (Dica: leia a documentaÃ§Ã£o para `matrix`!)
>
> > ## SoluÃ§Ã£o para o Desafio 5

> > 
> > ~~~
> > x <- matrix(1:50, ncol=5, nrow=10)
> > x <- matrix(1:50, ncol=5, nrow=10, byrow = TRUE) # to fill by row
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}


> ## Desafio 6

> Crie uma lista de comprimento dois contendo um vetor de caracteres para cada
uma das seÃ§Ãµes nesta parte da oficina:
>
>  - Tipos de dados
>  - Estruturas de dados
>
> Preencha cada vetor de caracteres com os nomes dos tipos de dados e estruturas
> de dados que vimos atÃ© agora
>
> > ## SoluÃ§Ã£o do Desafio 6
> > 
> > ~~~
> > dataTypes <- c('double', 'complex', 'integer', 'character', 'logical')
> > dataStructures <- c('data.frame', 'vector', 'factor', 'list', 'matrix')
> > answer <- list(dataTypes, dataStructures)
> > ~~~
> > {: .r}
> > Nota: Ã© bom fazer uma lista em letras grandes numa placa ou gravado na parede
> > lista ndo todos esses tipos e estruturas - Deixe-o para o resto da oficina
> > para lembrar as pessoas da importÃ¢ncia dessas noÃ§Ãµes bÃ¡sicas.

> {: .solution}
{: .challenge}


> ## Desafio 7
>
> Considere a saÃ?da do R da matriz abaixo:
> 
> ~~~
>      [,1] [,2]
> [1,]    4    1
> [2,]    9    5
> [3,]   10    7
> ~~~
> {: .output}
> Qual foi o comando correto usado para escrever essa matriz? Examine cada
> comando e tente descobrir o correto antes de digitÃ¡-los. Pense em quais
> matrizes os outros comandos produzirÃ£o.
>
> 1. `matrix(c(4, 1, 9, 5, 10, 7), nrow = 3)`
> 2. `matrix(c(4, 9, 10, 1, 5, 7), ncol = 2, byrow = TRUE)`
> 3. `matrix(c(4, 9, 10, 1, 5, 7), nrow = 2)`
> 4. `matrix(c(4, 1, 9, 5, 10, 7), ncol = 2, byrow = TRUE)`
>
> > ## SoluÃ§Ã£o do Desafio 7
> >

> > 
> > ~~~
> > matrix(c(4, 1, 9, 5, 10, 7), ncol = 2, byrow = TRUE)
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}
