---
title: "Introduction to R and RStudio"
teaching: 45
exercises: 10
questions:
- "Como encontrar o seu camihno ao redor de RStudio?"
- "Como interagir com R?"
- "Como gerenciar seu ambiente?"
- "Como instalar pacotes?"
objectives:
- "Obter familiaridade com os vários panéis no IDE do RStudio"
- "Obter familiaridade com os botões, atalhos e opções no IDE do RStudio"
- "Entender variáveis e como atribuir a ela"
- "Ser capaz de gerenciar seu espaço de trabalho em uma sessaão interativa de R"
- "Ser capaz de usar operaçoões matemáticas e de comparação"
- "Ser capaz de chamar funções"
- "Introduzir o gerenciamento de pacotes"  
keypoints:
- "Usar RStudio para escrever e rodar programas de R."
- "R tem os operadores aritmeticos usuais e funções matemáticas."
- "Usar `<-` para atribuir valores a uma variável."
- "Usar `ls()` para listar as variáveis num programa."
- "Usar `rm()` para deletar objetos num programa."
- "Usar `install.packages()` para instalar pacotes (librerias)."
---




## Motivação

A ciência é um processo de várias etapas: uma vez que você criou uma experiência e coletou dados, a verdadeira diversão começa! Esta lição ensinará como iniciar este processo usando R e RStudio. Começaremos com dados brutos, realizaremos análises exploratórias e aprenderemos a traçar resultados graficamente. Este exemplo começa com um conjunto de dados de [gapminder.org](https://www.gapminder.org) que contém informações de população para muitos países ao longo do tempo. Você pode ler os dados em R? Pode traçar a população para o Senegal? Você pode calcular a renda média dos países do continente asiático? No final dessas lições você será capaz de fazer coisas como tramar as populações de todos esses países em menos de um minuto!

## Antes de iniciar o Workshop

Certifique-se de que tem a versão mais recente do R e do RStudio instalados na sua máquina. Isso é importante, pois alguns pacotes usados no workshop podem não ser instalados corretamente (ou em todos) se R não estiver atualizado.

[Download and install the latest version of R here](https://www.r-project.org/)
[Download and install RStudio here](https://www.rstudio.com/)

## Introduçaõ ao RStudio 


Bem-vindo à parte do R do Software Carpentry..

Ao longo desta lição, vamos ensinar-lhe alguns dos fundamentos da linguagem R, bem como algumas práticas recomendadas para organizar o código para projetos científicos que facilitarão a sua vida.

Estaremos usando o RStudio: um ambiente de desenvolvimento integrado livre e de código aberto. Ele fornece um editor embutido, funciona em todas as plataformas (incluindo servidores) e oferece muitas vantagens, como integração com controle de versão e gerenciamento de projetos.



**Layout básico**

Quando você abrir RStudio pela primeira vez, você será recebido por três painéis: 

  * O console R interativo (todo à esquerda)
  * Ambiente/História (tabulada no canto direito)
  * Archivos/Gráficos/Pacotes/Ajuda/Visualizador (com abas na parte inferior direita)

![](http://swcarpentry.github.io/r-novice-gapminder/fig/01-rstudio.png)

Depois de abrir arquivos, como R scripts, um painel de editor também será aberto no canto superior esquerdo.


![](http://swcarpentry.github.io/r-novice-gapminder/fig/01-rstudio-script.png) 


## Fluxo de trabalho no RStudio
Existem duas maneiras principais de se trabalhar dentro do RStudio.

1. Teste e jogue dentro do console R interativo, em seguida, copie o código para um arquivo .R para ser executado posteriormente.
   *  Isso funciona bem ao fazer pequenos testes e inicialmente começar.
   *  Torna-se rapidamente trabalhoso.
2. Comece a escrever em um arquivo .R e use o comando / atalho RStudio para pressionar a linha atual, as linhas selecionadas ou as linhas modificadas para o console R interativo. .
   * Esta é uma ótima maneira de começar; Todo o seu código é salvo para mais tarde.
   * Você poderá executar o arquivo criado a partir de RStudio ou usando a função **source ()** de R.

> ## Dica: Executando segmentos do seu código
>
> O RStudio oferece-lhe uma grande flexibilidade na execução de código 
>a partir da janela do editor. Existem botões, opções de menu e atalhos 
>de teclado. Para executar a linha atual, você pode: 1. pressionar no botão 
>Executar acima do painel do editor ou 2. selecionar "Run lines" no menu "Code",
>ou 3. pressionar Ctrl-Enter no Windows ou Linux ou Command-Enter no OS X.
>(Este atalho também pode ser visto ao passar o mouse sobre o botão).
>Para executar um bloco de código, selecione-o e, em seguida, Executar. 
>Se você modificou uma linha de código dentro de um bloco de código que 
>você acabou de executar, não há necessidade de reajustar a seção e Run, 
>você pode usar o próximo botão, Re-Run the previous code region. Isso 
>executará o bloco de código anterior incluindo as modificações feitas.
>
{: .callout}

## Introdução a R

A maior parte do seu tempo em R será gasto no console interativo R. Isto é onde você irá executar todo o seu código, e pode ser um ambiente útil para experimentar idéias antes de adicioná-los a um arquivo de script R. Este console no RStudio é o mesmo que você obteria se você digitou R em seu ambiente de linha de comando.

A primeira coisa que você vai ver na sessão interativa R é um monte de informações, seguido por um ">" e um cursor piscando. Em muitos aspectos isso é semelhante ao ambiente de shell que você aprendeu durante as lições do shell: ele opera na mesma idéia de um "Read, evaluate, print loop": você digita comandos, R tenta executá-los e, em seguida, retorna um resultado.

## Usando R como uma calculadora 

A coisa mais simples que você pode fazer com R é aritmética: 


~~~
1 + 100
~~~
{: .r}



~~~
[1] 101
~~~
{: .output}

E R vai imprimir a resposta, com um precedente "[1]". Não se preocupe com isso por agora, vamos explicar isso mais tarde. Por agora, pense nisso como uma saída indicadora. 

Como bash, se você digitar um comando incompleto, R esperará que você o complete:
~~~
> 1 +
~~~
{: .r}

~~~
+
~~~
{: .output}

Cada vez que você pressionar a tecla Enter e a sessão R mostre um "+" em vez de um ">", isso significa que está esperando que você complete o comando. Se você deseja cancelar um comando, você pode simplesmente presionar em "Esc" e rstudio vai lhe dar de volta o ">" alerta.

> ## Dica: Cancelamento de comandos
>
> Se você estiver usando R a partir da linha de comando em vez de  
>dentro RStudio, você precisará usar `Ctrl+C` em vez de `Esc` 
> para cancelar o comando. Isso também se aplica aos usuários de Mac!
>
> Cancelar um comando não é útil somente para matar comandos incompletos: 
> você também pode usá-lo para dizer a R para parar o código em execução
> (por exemplo, se estiver demorando muito mais do que você espera) 
>ou para se livrar do código que você está escrevendo. 
>
{: .callout}

Ao usar R como uma calculadora, a ordem das operações é a mesma que você teria aprendido na escola.   

Da precedência mais alta à mais baixa:

 * Parênteses: `(`, `)`
 * Exponentes: `^` or `**`
 * Dividir: `/`
 * Multiplicar: `*`
 * Adicionar: `+`
 * Subtrair: `-`


~~~
3 + 5 * 2
~~~
{: .r}



~~~
[1] 13
~~~
{: .output}

Use parênteses para agrupar operações, a fim de forçar a ordem de avaliação se difere do padrão, ou para tornar claro o que você pretende.


~~~
(3 + 5) * 2
~~~
{: .r}



~~~
[1] 16
~~~
{: .output}

Isso pode ficar complicado quando não é necessário, mas esclarece suas intenções. Lembre-se de que os outros podem ler o seu código mais tarde. 


~~~
(3 + (5 * (2 ^ 2))) # difícil de ler
3 + 5 * 2 ^ 2       # claro, se você se lembrar das regras
3 + 5 * (2 ^ 2)     # se você esquecer algumas regras, isso pode ajudar
~~~
{: .r}


O texto após cada linha de código é chamado de "comentário". Qualquer coisa que se segue após o hash (ou octothorpe) símbolo `#` é ignorado por R quando ele executa código.

Números realmente pequenos ou grandes obtêm uma notação científica:


~~~
2/10000
~~~
{: .r}



~~~
[1] 2e-04
~~~
{: .output}

Qual é taquigrafia para "multiplicado por `10^XX`". Então `2e-4` é abreviação para `2 * 10^(-4)`.


Você também pode escrever números em notação científica: 


~~~
5e3  # Note a falta de menos aqui
~~~
{: .r}



~~~
[1] 5000
~~~
{: .output}

## Funções matemáticas

R tem muitas funções matemáticas construídas. Para chamar uma função, simplesmente digite seu nome, seguido por parênteses abertos e fechados. Qualquer coisa que digitemos dentro dos parênteses é chamada de argumentos da função:


~~~
sin(1)  # funções trigonométricas
~~~
{: .r}



~~~
[1] 0.841471
~~~
{: .output}


~~~
log(1)  # logaritmo natural
~~~
{: .r}



~~~
[1] 0
~~~
{: .output}


~~~
log10(10) # logaritmo base-10
~~~
{: .r}



~~~
[1] 1
~~~
{: .output}


~~~
exp(0.5) # e^(1/2)
~~~
{: .r}



~~~
[1] 1.648721
~~~
{: .output}

Não se preocupe em tentar lembrar cada função em R. Você pode simplesmente procurá-los no Google, ou se lembrar do início do nome da função, use a conclusão da guia no RStudio.

Esta é uma vantagem que RStudio tem sobre R por conta própria, tem auto-conclusão habilidades que lhe permitem procurar mais facilmente as funções, os seus argumentos e os valores que eles tomam.

Digite um "?" antes do nome dum comando e abrirá uma página de ajuda para esse comando. Assim como fornecerá uma descrição detalhada do comando e como ele funciona, baixando na a detailed description of the command and how it works, a rolagem para a parte inferior da página de ajuda normalmente mostrará uma coleção de exemplos de código que ilustram o uso do comando. Passaremos por um exemplo mais adiante.

## Comparando coisas

Podemos também fazer comparação em R:


~~~
1 == 1  # igualdade (nota dois sinais iguais, leai-se como "é igual a")
~~~
{: .r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 != 2  # desigualdade (leai-se como "não é igual a")
~~~
{: .r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 <  2  # menor que
~~~
{: .r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 <= 1  # Menor ou igual que
~~~
{: .r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 > 0  # maior que
~~~
{: .r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 >= -9 #Maior ou igual que
~~~
{: .r}



~~~
[1] TRUE
~~~
{: .output}

> ## Dica: Comparando Números
>
>Uma palavra de advertência sobre a comparação de números: 
>você nunca deve usar `==` para comparar dois números a
> menos que sejam inteiros (um tipo de dados que pode representar
> especificamente apenas números inteiros).
>
> Os computadores só podem representar números decimais com 
>um certo grau de precisão, então dois números que parecem os mesmos
>quando impressos por R, podem realmente ter diferentes representações 
>subjacentes e, portanto, ser diferentes por uma pequena margem de erro 
>(chamada tolerância numérica da máquina).
>
> Em vez disso, você deve usar a função `all.equal`.
> Leitura adicional:     [http://floating-point-gui.de/](http://floating-point-gui.de/)
> 
{: .callout}

## Variáveis e atribuição  

Podemos armazenar valores em variáveis usando o operador de atribuição `<-`, assim: 


~~~
x <- 1/40
~~~
{: .r}

Observe que a atribuição não imprime um valor. Em vez disso, nós armazenamos isso para mais tarde em algo chamado de **variável**, `x` agora contém o **valor** `0.025`:


~~~
x
~~~
{: .r}



~~~
[1] 0.025
~~~
{: .output}

Mais precisamente, o valor armazenado ? uma *aproximação decimal* dessa fração chamada uma [Número de ponto flutuante](http://en.wikipedia.org/wiki/Floating_point).

Procure a guia `Ambiente` em um dos painéis do RStudio, e você verá que `x` e seu valor apareceram. Nossa variável `x` pode ser usada no lugar de um número em qualquer cálculo que espera um número: 


~~~
log(x)
~~~
{: .r}



~~~
[1] -3.688879
~~~
{: .output}

Observe também que as variáveis podem ser reatribuídas:


~~~
x <- 100
~~~
{: .r}

`x` usado para conter o valor 0.025 e agora ele tem o valor 100.  

valores asignados podem conter a variável sendo assignidada:


~~~
x <- x + 1 #observe como o RStudio atualiza sua descrição de x na guia superior direita
~~~
{: .r}

O lado direito da atribuição pode ser qualquer expressão R válida. 
O lado direito é *totalmente avaliado* antes da atribuição ocorrer.

Nomes de variáveis podem conter letras, números, sublinhados e pontos. Eles não podem começar com um número nem conter espaços em tudo. Diferentes pessoas usam convenções diferentes para nomes de variáveis longas,

  * pontos.entre.palavras
  * sublinha\_entre_palavras
  * cameloCasoParaSeparadoPalavras

O que você usa depende de você, mas seja **consistente**.

Também é possível usar o operador = para atribuição: 


~~~
x = 1/40
~~~
{: .r}

Mas isso é muito menos comum entre os usuários de R. O mais importante é ser **consistente** com o operador que você usa. Há ocasionalmente lugares onde é menos confuso usar `<-` than `=`, e é o símbolo mais comum usado na comunidade. Portanto, a recomendação é usar `<-`.  

## Vetoriza??o

? de extrema relev?ncia compreender que o R ? um software vetorizado. Isso simplesmnte quer dizer que vari?veis e fun??es podem receber vetores. 
Veja os exemplos abaixo:


~~~
1:5
~~~
{: .r}



~~~
[1] 1 2 3 4 5
~~~
{: .output}



~~~
2^(1:5)
~~~
{: .r}



~~~
[1]  2  4  8 16 32
~~~
{: .output}



~~~
x <- 1:5
2^x
~~~
{: .r}



~~~
[1]  2  4  8 16 32
~~~
{: .output}

A possibilidade de vari?veis e fun??es receber valores faz do R um software extremamente poderoso. Este t?pico ser? abordado em detalhes adiante.


## Controlando o ambiente de trabalho

Existem alguns comandos que o usu?rio pode utilizar para interagir com o ambiente de trabalho do R.

A fun??o `ls`, por exemplo, lista todas as vari?veis e fun??es gravadas no ambiente de trabalho.



~~~
ls()
~~~
{: .r}



~~~
[1] "x" "y"
~~~
{: .output}

> ## Dica: Objetos escondidos
>
> A fun??o `ls()`n?o mostra vari?veis e fun??es que come??o com `.`.
> A fun??o  Para listar todos os objetos, inclusive os que   iniciam com `.`, digite `ls(all.names=TRUE)` e n?o `ls()`.
> 
{: .callout}

Note que na fun??o `ls` n?o ? necess?rio fornecer argumentos, mas ? necess?rio colocar par?ntesis para que o R entenda que se trata de uma fun??o.

Se digitarmos apenas `ls` o R nos fornecer? o c?digo fonte da fun??o!


~~~
ls
~~~
{: .r}



~~~
function (name, pos = -1L, envir = as.environment(pos), all.names = FALSE, 
    pattern, sorted = TRUE) 
{
    if (!missing(name)) {
        pos <- tryCatch(name, error = function(e) e)
        if (inherits(pos, "error")) {
            name <- substitute(name)
            if (!is.character(name)) 
                name <- deparse(name)
            warning(gettextf("%s converted to character string", 
                sQuote(name)), domain = NA)
            pos <- name
        }
    }
    all.names <- .Internal(ls(envir, all.names, sorted))
    if (!missing(pattern)) {
        if ((ll <- length(grep("[", pattern, fixed = TRUE))) && 
            ll != length(grep("]", pattern, fixed = TRUE))) {
            if (pattern == "[") {
                pattern <- "\\["
                warning("replaced regular expression pattern '[' by  '\\\\['")
            }
            else if (length(grep("[^\\\\]\\[<-", pattern))) {
                pattern <- sub("\\[<-", "\\\\\\[<-", pattern)
                warning("replaced '[<-' by '\\\\[<-' in regular expression pattern")
            }
        }
        grep(pattern, all.names, value = TRUE)
    }
    else all.names
}
<bytecode: 0x7fd12938a0b0>
<environment: namespace:base>
~~~
{: .output}

Pode ser interessante deletar objetos que n?o ser?o utilizados adiante. Para isso utilizamos a fun??o `rm`.


~~~
rm(x)
~~~
{: .r}

Se muitos objetos devem ser exclu?dos de uma s? vez n?o h? necessidade de excluir um por um. Basta utilizar a fun??o `ls` conjugada com a `rm` da seguinte forma:


~~~
rm(list = ls())
~~~
{: .r}

Neste caso duas fun??es foram utilizadas em conjunto. Sempre que este for o caso o que est? localizado dentro do par?ntesis mais interno ser? avaliado primeiro e assim em diante.

No caso acima foi especificado que o resultado da fun??o `ls` deveria ser usado na forma de lista `list` como argumento da fun??o `rm`. Quando destinados valores de argumentos a fun??es por nome, o operador a ser utilizado dever? ser o s?mbolo `=`.

Se utilizarmos `<-` teremos efeitos indesejados ou  mensagens de erro.

~~~
rm(list <- ls())
~~~
{: .r}



~~~
Error in rm(list <- ls()): ... must contain names or character strings
~~~
{: .error}

> ## Dica: Avisos vs Erros
>
> Fique atento pois o R poder? fazer algo inesperado.
> Erros, como no caso acima, ocorrem quando o R n?o consegue efetuar as opera??es.
> Avisos, por outro lado, indicam que o R conseguiu efetuar as opera??es, mas algo  provavelmente n?o ocorreu como esperado.
>
> Em ambos os casos, as mensagens que o R fornece ajudam a consertar o problema.
>
{: .callout}

## Pacotes do R

? poss?vel adicionar fun??es ao R atrav?s da escrita de pacote escritos por voc? mesmo, ou por pacotes escritos por outras pessoas. Hoje existem mais de 7000 pacotes dispon?veis no CRAN (*the comprehensive R archive network*). O R e o Rstudio possuem elevada funcionalidade no quesito de gerenciamento de pacotes:

* ? poss?vel ver quais pacotes est?o instalados. Para isso devemos digitar `installed.packages()`.
* ? poss?vel instalar novos pacotes ao digitar `install.packages("packagename")`, onde `packagename` ? o nome do pacote a ser instalado. 
* ? poss?vel atualizar pacotes j? instalados. A fun??o utilizada ? `update.packages()`.
* ? poss?vel remover pacotes com a fun??o `remove.packages("packagename")`. 
* ? poss?vel tornar um pacote habilitado ao uso. A fun??o utilizada neste caso ? `library(packagename)`.

> ## Desafio 1
>
> Quais nomes a seguir s?o v?lidos para vari?veis no R ?
> 
> ~~~
> min_height
> max.height
> _age
> .mass
> MaxLength
> min-length
> 2widths
> celsius2kelvin
> ~~~
> {: .r}
>
> > ## Solu??o do desafio 1
> >
> > Os nomes a seguir s?o v?lidos:
> > 
> > ~~~
> > min_height
> > max.height
> > MaxLength
> > celsius2kelvin
> > ~~~
> > {: .r}
> >
> > O nome a seguir cria uma vari?vel escondida
> > 
> > ~~~
> > .mass
> > ~~~
> > {: .r}
> >
> > Os nomes a seguir n?o podem ser usados para nomear objetos
> > 
> > ~~~
> > _age
> > min-length
> > 2widths
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

> ## Desafio 2
>
> Quais ser?o os valores das vari?veis definidas abaixo ?
>
> 
> ~~~
> mass <- 47.5
> age <- 122
> mass <- mass * 2.3
> age <- age - 20
> ~~~
> {: .r}
>
> > ## Solu??o do desafio 2
> >
> > 
> > ~~~
> > mass <- 47.5
> > ~~~
> > {: .r}
> > Este comando atribui o valor 47.5 para a vari?vel ` mass` for the variable mass
> >
> > 
> > ~~~
> > age <- 122
> > ~~~
> > {: .r}
> > Este comando atribiu o valor 122 para a vari?vel ` age` 
> >
> > 
> > ~~~
> > mass <- mass * 2.3
> > ~~~
> > {: .r}
> > O valor da vari?vel ` mass`ser? dividido por 2.3 e a vari?vel ` mass` passar? a ter um novo valor.
> > 
> >
> > 
> > ~~~
> > age <- age - 20
> > ~~~
> > {: .r}
> > Ser? realizada uma subtra??o de 20 unidades na vari?vel ` age`.
> > 
> {: .solution}
{: .challenge}


> ## Desafio 3
>
> Rode os c?digos do desafio anterior, escreva um comando e compare massa com idade. 
> A massa ? maior que a idade ?
>
> > ## Solu??o do desafio 3
> >
> > Uma maneira de realizar esta tarefa ? utilizar `>`:
> > 
> > ~~~
> > mass > age
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > [1] TRUE
> > ~~~
> > {: .output}
> > O resultado a ser retornado deve ser `TRUE` porque a vari?vel ` mass` ? maior que ` age`.
> {: .solution}
{: .challenge}


> ## Desafio 4
>
> Limpe o seu ambiente de trabalho. Delete as vari?veis massa e idade.
>
>
> > ## Solu??o do desafio 4
> >
> > O comando `rm` pode ser utilizado para realizar essa tarefa
> > 
> > ~~~
> > rm(age, mass)
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

> ## Desafio 5
>
> Instale os pacotes `ggplot2`, `plyr` e `gapminder`.
>
> > ## Solu??o do desafio 5
> >
> > Podemos utilizar o comando `install.packages()` para instalar os referidos pacotes.
> > 
> > ~~~
> > install.packages("ggplot2")
> > install.packages("plyr")
> > install.packages("gapminder")
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}
