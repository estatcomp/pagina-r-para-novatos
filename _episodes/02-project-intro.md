---
t�tulo: " Gerenciamento de projetos com RStudio"
ensino: 20
exerc�cios: 10
quest�es:
- "Como eu posso gerenciar meus projetos no R ?"
objetivos:
- Ser capaz de criar projetos independentes com RStudio
- TSer capaz de usar o git com o RStudio
pontos-chave:
- "Utilizar o RStudio para criar e gerenciar projetos com bom layout."
- "Tratar os dados apenas como arquivos de leitura."
- "Tratas as sa�das como dispens�veis."
- "Separar as fun��es das aplica��es."
- "Usar a vers�o de controle"
source: Rmd
---



## Introdu��o

O processo cient�fico � de natureza incremental. Muitos projetos come�am com notas ou c�digos aleat�rios e a partir disso surgem manuscritos. Eventualmente essas escritas e c�digos se misturam.
<blockquote class="twitter-tweet"><p>Managing your projects in a reproducible fashion doesn't just make your science reproducible, it makes your life easier.</p>— Vince Buffalo (@vsbuffalo) <a href="https://twitter.com/vsbuffalo/status/323638476153167872">April 15, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

A maioria das pessas organizam seus projetos da seguinte maneira

![](../fig/bad_layout.png)

Por diversas raz�es SEMPRE devemos evitar esse tipo de armazenamento de projetos:

1. � dif�cil ver qual vers�o � a original e quais s�o as modificadas.
2. Deste modo obtemos diversas extens�es de arquivos na mesma pasta.
3. Provavelmente iremos demorar bastante para para encontrar alguma coisa. Relacionar uma figura com o c�digo que a gera, por exemplo.

Um bom *layout* pode facilitar bastante nossa vida. Algumas vantagens s�o:

* Nos ajuda a assegurar a integridade dos dados;
* Facilita o compartilhamento dos c�digos com outras pessoas (colegas de laborat�rio, colaboradores ou supervisores);
* Facilita o processo de atualiza��o dos c�digos;
* � mais f�cil encontrar um projeto ap�s algum tempo.

## Uma poss�vel solu��o

Existem ferramentas e pacotes que nos ajudam a gerenciar nosso trabalho de forma mais efetiva.

Uma das melhores caracter�sticas do RStudio, s�o as funcionalidades oferecidas em termos de gerenciamento de projetos. Usaremos tais ferramentas para uma criar um projeto independente e pass�vel de ser reproduzido.



> ## Desafio: Criando um projeto independente
>
> Vamos criar um novo projeto no RStudio
>
> 1. Clique no bot�o File e ent�o em  New Progect.
> 2. Clique em New Directory.
> 3. Clique em Empty Project.
> 4. Digite o nome do diret�rio que em que seu projeto ser� gravado.
> 5. Clique em Create a git repository.
> 6. Clique em Create Projeto.
{: .challenge}

Agora, toda vez que iniciarmos uma sess�o desse projeto no RStudio todo o trabalho estar� inteiramente contido neste diret�rio.

## Melhores pr�ticas aplicadas a organiza��o de projetos

Embora n�o exista a `MELHOR` forma de organizar um projeto, existem alguns princ�pios gerais que s�o consistentes com o objetico de deixar o gerenciamento de projetos mais simples.

### Trate os dados apenas como leitura

Este � provavelmente o principal objetivo ao organizar um projeto. Dados geralmente s�o dif�ceis de se coletar. Trabalhar com dados em programas interativos (Excel) onde eles podem ser modificados atrapalha. Isso porque n�o temos certeza de onde os dados vieram ou como foram modificados desde a coleta. Para evitar este tipo de problema � recomend�vel trabalhar os dados como arquivos apenas para leitura.

### Limpeza dos dados

Em muitos casos os dados s�o "sujos". Nestes casos � extremamente dif�cil transformar os dados at� que eles sejam pass�veis de serem lidos pelo R (ou qualquer outro programa). Esta tarefa � geralmente chamada de "data munging". Quando altera��es devem ser feitas no conjunto de dados original, � aconselh�vel criar um segundo arquivo de leitura em uma pasta separada.

### Trate as sa�das como dispens�veis

Quaisquer coisas geradas pelos scripts devem ser tratadas como dispens�veis. Devemos ser capazes de recriar as altera��es ou an�lises feitas a partir do script.

Existem diversas maneiras de gerenciar os outputs. � interessante termos uma pasta com subdiret�rios para cada an�lise que formos fazer. Desta maneira � mais f�cil encontrar as an�lises de interesse, pois ao mesmo tempo que nem todas as an�lises feitas s�o utilizadas no trabalho final, outras poder�o ser aplicadas em outros projetos.


> ## Dica: Praticas interessantes em computa��o cient�fica
>
> [Boas pr�ticas em computa��o cient�fica](https://github.com/swcarpentry/good-enough-practices-in-scientific-computing/blob/gh-pages/good-enough-practices-for-scientific-computing.pdf) sugerem as recomenda��es para uma boa organiza��o de projetos:
>
> 1. Coloque cada projeto em seu pr�prio diret�rio. O diret�rio deve ser nomeado ap�s o projeto.
> 2. Coloque documentos de textos associados a um diret�rio `doc`.
> 3. Coloque os dados puros no diret�rio `data`, os dados alterados e os dados limpos devem ser colocados em uma pasta `results`.
> 4. Coloque os scripts e os programas em um diret�rio `src`. Os programas importados de outros locais devem ser alocados no diret�rio `bin`.
> 5. Escolha nomes que indiquem a fun��o de cada arquivo.
>
{: .callout}

> ## Dica: Modelo de projeto - uma poss�vel solu��o
>
> Uma maneira de automatizar o gerenciamento de projetos se d� com a instala��o do pacote `ProjectTemplate`. Esse  > pacote oferece uma estrutura que � considerada ideal para o bom gerenciamento do projeto. O pacote � �til porque > mostra o fluxo de trabalho de forma organizada e estruturada. Com o RStudio e com o Git � poss�vel ter controle  > total dos trabalhos, al�m de facilitar o compartilhamento dos arquivos com colaboradores.
>
> 1. Instale o pacote ProjectTemplate
> 2. Carregue o pacote
> 3. Inicie o projeto:
>
> 
> ~~~
> install.packages("ProjectTemplate")
> library("ProjectTemplate")
> create.project("../my_project", merge.strategy = "allow.non.conflict")
> ~~~
> {: .r}
>
> Para mais informa��es sobre o pacote `ProjectTemplate` e suas funcionalidades acesse   
> [ProjectTemplate](http://projecttemplate.net/index.html)
{: .callout}

### Separe as fun��es das aplica��es

O modo mais efetivo de trabalhar no R � brincando com os c�digos na sess�o interativa. Quando temos certeza de que os c�digos funcionam e fazem o que queremos, copiamos para um arquivo de script. Tamb�m � poss�vel salvar todos os comandos utilizados, para isso utilizamos a fun��o *history()*. Utilizar essa fun��o nem sempre � �til pois quando estamos desenvolvendo algum programa novo surgem muitos erros.

Quando o prejeto � novo, geralmente o arquivo de script cont�m muitas linhas. Quando o projeto est� em um est�gio mais avan�ado peda�os de c�digos podem ser re-utilizados. � uma boa ideia separar os c�digos em diferrentes pastas; Uma para salvar os c�digos que ser�o utilizados com frequ�ncia e outra para salvar os scripts das an�lises feitas.

> ##  Dica: evite duplica��o
>
> � poss�vel que o mesmo conjunto de dados e o mesmo script sejam usados em projetos distintos. De modo geral 
> queremos evitar a duplica��o de arquivos de modo a salvar espa�o e n�o termos que atualizar o mesmo c�digo em 
> diferentes lugares.

> Quando este for o caso � interessante usar *symbolic links*, que s�o atalhos para arquivos que se encontram em 
> outro lugares. No Linux e no OS X podemos usar o comando `ln -s`, no Windows podemos criar um atalho ou usar o
> comando `mklink` no terminal de comandos.
{: .callout}

### Save the data in the data directory

Now we have a good directory structure we will now place/save the data file in the `data/` directory.

> ## Challenge 1
> Download the gapminder data from [here](https://raw.githubusercontent.com/resbaz/r-novice-gapminder-files/master/data/gapminder-FiveYearData.csv).
>
> 1. Download the file (CTRL + S, right mouse click -> "Save as", or File -> "Save page as")
> 2. Make sure it's saved under the name `gapminder-FiveYearData.csv`
> 3. Save the file in the `data/` folder within your project.
>
> We will load and inspect these data later.
{: .challenge}

> ## Challenge 2
> It is useful to get some general idea about the dataset, directly from the
> command line, before loading it into R. Understanding the dataset better
> will come in handy when making decisions on how to load it in R. Use the command-line
> shell to answer the following questions:
> 1. What is the size of the file?
> 2. How many rows of data does it contain?
> 3. What kinds of values are stored in this file?
>
> > ## Solution to Challenge 2
> >
> > By running these commands in the shell:
> > 
> > ~~~
> > ls -lh data/gapminder-FiveYearData.csv
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > 
> > ~~~
> > -rw-r--r--  1 gabrielfranco89  staff    80K Mar 20 20:50 data/gapminder-FiveYearData.csv
> > ~~~
> > {: .output}
> > The file size is 80K.
> > 
> > ~~~
> > wc -l data/gapminder-FiveYearData.csv
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > 
> > ~~~
> >     1705 data/gapminder-FiveYearData.csv
> > ~~~
> > {: .output}
> > There are 1705 lines. The data looks like:
> > 
> > ~~~
> > head data/gapminder-FiveYearData.csv
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > 
> > ~~~
> > country,year,pop,continent,lifeExp,gdpPercap
> > Afghanistan,1952,8425333,Asia,28.801,779.4453145
> > Afghanistan,1957,9240934,Asia,30.332,820.8530296
> > Afghanistan,1962,10267083,Asia,31.997,853.10071
> > Afghanistan,1967,11537966,Asia,34.02,836.1971382
> > Afghanistan,1972,13079460,Asia,36.088,739.9811058
> > Afghanistan,1977,14880372,Asia,38.438,786.11336
> > Afghanistan,1982,12881816,Asia,39.854,978.0114388
> > Afghanistan,1987,13867957,Asia,40.822,852.3959448
> > Afghanistan,1992,16317921,Asia,41.674,649.3413952
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Tip: command line in R Studio
>
> You can quickly open up a shell in RStudio using the **Tools -> Shell...** menu item.
{: .callout}

### Version Control

We also set up our project to integrate with git, putting it under version control.
RStudio has a nicer interface to git than shell, but is very limited in what it can
do, so you will find yourself occasionally needing to use the shell. Let's go
through and make an initial commit of our template files.

The workspace/history pane has a tab for "Git". We can stage each file by checking the box:
you will see a green "A" next to stage files and folders, and yellow question marks next to
files or folders git doesn't know about yet. RStudio also nicely shows you the difference
between files from different commits.

> ## Tip: versioning disposable output
>
> Generally you do not want to version disposable output (or read-only data).
> You should modify the `.gitignore` file to tell git to ignore these files
> and directories.
{: .callout}

> ## Challenge 3
>
> 1. Create a directory within your project called `graphs`.
> 2. Modify the `.gitignore` file to contain `graphs/`
> so that this disposable output isn't versioned.
>
> Add the newly created folders to version control using
> the git interface.
>
> > ## Solution to Challenge 3
> >
> > This can be done with the command line:
> > ```
> > $ mkdir graphs
> > $ echo "graphs/" >> .gitignore
> > ```
> > {: . shell}
> {: .solution}
{: .challenge}
