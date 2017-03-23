---
title: Writing Data
teaching: 10
exercises: 10
questions:
- "Como salvar gráficos e dados criados em R?"
objectives:
- "Ser capaz de redigir gráficos e dados de R."
keypoints:
- "Salvar gráficos do RStudio usando o botão 'Export'."
- "Usar `write.table` para salvar dados tabulares."
source: Rmd
---




## Como salvar gráficos

Você já viu como salvar o plot mais recente que você criou no `ggplot2`,
usando o comando `ggsave`. Como utiliza-lo:


~~~
ggsave("My_most_recent_plot.pdf")
~~~
{: .r}

Você pode salvar um plot de dentro do RStudio usando o botão 'Export'
na janela 'Plot'. Isto dará a você a opção de salvar como um
.pdf ou como .png, .jpg ou outro formato de imagem.

Às vezes você irá querer salvar plots sem criar-los na janela do
'Plot' primeiro. Talvez você queira fazer um documento pdf com
várias páginas: cada um com um plot diferente, por exemplo. Ou talvez
você poder fazendo loop através de vários subconjuntos de um arquivo, plotando dados
de cada subconjunto e queira salvar cada plot, mas obviamente não pode parar
o loop terá que clicar em 'Export' para cada um.

Neste caso, você pode usar uma abordagem mais flexível. A função
`pdf` cria um novo dispositivo pdf. Você pode controlar o tamanho e a
resolução usando os argumentos desta função.


~~~
pdf("Life_Exp_vs_time.pdf", width=12, height=4)
ggplot(data=gapminder, aes(x=year, y=lifeExp, colour=country)) +
  geom_line()

# You then have to make sure to turn off the pdf device!

dev.off()
~~~
{: .r}

Abra este documento e dê uma olhada.

> ## Desafio 1
>
> Reescreva seu comando 'pdf' para imprimir uma segunda
> página no pdf, mostrando um enredo de faceta (dica: use `facet_grid`)
> dos mesmos dados com um painel por continente.
{: .challenge}


Os comandos `jpeg`, `png` etc. São utilizados de forma semelhante para produzir
documentos em formatos distintos.

## Escrevendo dados

Em algum momento, você também vai querer digitar os dados de R.

Podemos usar a função `write.table` para isso, que é
muito semelhante a `read.table` de antes.

Vamos criar um script de dados em branco, para esta análise,
só queremos focar os dados do gapminder para a Austrália:


~~~
aust_subset <- gapminder[gapminder$country == "Australia",]

write.table(aust_subset,
  file="cleaned-data/gapminder-aus.csv",
  sep=","
)
~~~
{: .r}

Vamos voltar ao shell para dar uma olhada nos dados para ter certeza de que ele está
OK:


~~~
head cleaned-data/gapminder-aus.csv
~~~
{: .r}




~~~
"country","year","pop","continent","lifeExp","gdpPercap"
"61","Australia",1952,8691212,"Oceania",69.12,10039.59564
"62","Australia",1957,9712569,"Oceania",70.33,10949.64959
"63","Australia",1962,10794968,"Oceania",70.93,12217.22686
"64","Australia",1967,11872264,"Oceania",71.1,14526.12465
"65","Australia",1972,13177000,"Oceania",71.93,16788.62948
"66","Australia",1977,14074100,"Oceania",73.49,18334.19751
"67","Australia",1982,15184200,"Oceania",74.74,19477.00928
"68","Australia",1987,16257249,"Oceania",76.32,21888.88903
"69","Australia",1992,17481977,"Oceania",77.56,23424.76683
~~~
{: .output}

Hmm, isso não é exatamente o que queríamos. De onde vieram todas
essas aspas? Também os números de linha são
sem sentido.

Vejamos o arquivo de ajuda para descobrir como alterar esse
comportamento.


~~~
?write.table
~~~
{: .r}

Por padrão, R envolverá vetores de caracteres com aspas ao
escrever para o arquivo. Ele também irá escrever os nomes das
linhas e colunas.

Vamos corrigir isso:


~~~
write.table(
  gapminder[gapminder$country == "Australia",],
  file="cleaned-data/gapminder-aus.csv",
  sep=",", quote=FALSE, row.names=FALSE
)
~~~
{: .r}

Agora vamos olhar para os dados novamente usando nossas habilidades shell:


~~~
head cleaned-data/gapminder-aus.csv
~~~
{: .r}




~~~
country,year,pop,continent,lifeExp,gdpPercap
Australia,1952,8691212,Oceania,69.12,10039.59564
Australia,1957,9712569,Oceania,70.33,10949.64959
Australia,1962,10794968,Oceania,70.93,12217.22686
Australia,1967,11872264,Oceania,71.1,14526.12465
Australia,1972,13177000,Oceania,71.93,16788.62948
Australia,1977,14074100,Oceania,73.49,18334.19751
Australia,1982,15184200,Oceania,74.74,19477.00928
Australia,1987,16257249,Oceania,76.32,21888.88903
Australia,1992,17481977,Oceania,77.56,23424.76683
~~~
{: .output}

Isso parece melhor!

> ## Desafio 2
>
> Faça um novo arquivo de dados com os subconjuntos dos dados gapminder
> incluindo apenas os dados coletados desde 1990.
>
> Use este script para escrever um novo subconjunto para um arquivo
> no diretório `cleaned-data/`.
{: .challenge}


