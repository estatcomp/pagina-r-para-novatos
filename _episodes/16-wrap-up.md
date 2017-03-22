---
title: Escrevendo bons softwares
teaching: 15
exercises: 0
questions:
- "Como posso escrever softwares que outras pessoas possam utilizar?"
objectives:
- "Describe best practices for writing R and explain the justification for each."
keypoints:
- "Document what and why, not how."
- "Break programs into short single-purpose functions."
- "Write re-runnable tests."
- "Don't repeat yourself."
- "Don't repeat yourself."
- "Be consistent in naming, indentation, and other aspects of style."
source: Rmd
---
  
## Tornar o código legível
  
A parte mais importante de escrever código é torná-lo legível e compreensível.
O ideal é que outra pessoa seja capaz de pegar seu código e ser capaz de entender
o que ele faz.

## Documentação: diga-nos qual e por quê, não como

Quando você começa pela primeira vez, seus comentários muitas vezes descrevem o que um comando faz, dado que você ainda está aprendendo por si mesmo e isso pode lhe ajudar a esclarecer conceitos e lembrá-lo(a) mais tarde. No entanto, estes comentários não são particularmente úteis futuramente quando você não se lembra que problema seu código estava tentando resolver. Tente também incluir comentários que lhe digam * por que * você está resolvendo um problema, e * qual * problema
isso é. O * como * pode vir depois disso: é um detalhe de implementação que você a princípio não deve ter que se preocupar.

## Mantenha seu código modular

Nossa recomendação é que você separe sua suas funções de seus scripts de análise, armazenando-as em um arquivo separado que você possa linkar (`source`) ao abrir sua sessão do R em determinado projeto. Esta abordagem é bacana porque lhe permite ter um script de análise organizado e um repositório de funções úteis que podem ser carregadas em qualquer script de análise em seu projeto. Isso também permite agrupar funções em conjunto facilmente.

## Dividir o problema em pequenos pedaços

Quando você começa pela primeira vez, resolver problemas e escrever funções podem ser tarefas assustadores e difíceis de separar devido sua inexperiência com o código. Tente quebrar o seu problema em pequenos pedaços e se preocupar com os detalhes de implementação mais tarde: continue dividindo o problema em funções cada vez menores até que você chegar a um ponto onde você pode codificar uma solução e construir o problema de volta a partir daí.

## Saiba que seu código está fazendo a coisa certa

Certifique-se de testar suas funções!
  
## Não se ~~reprima~~ repita

As funções possibilitam sua reutilização fácil dentro de um projeto. Se você vir blocos semelhantes de linhas de código ao longo do seu projeto, esses são candidatos para se tornarem funções.

Se os cálculos forem executados através de uma série de funções, então o projeto torna-se mais modular e mais fácil de manusear. Este é especialmente o caso para o qual uma determinada entrada resulta sempre uma saída particular.

## Lembre-se de ser elegante
Use um estilo consistente ao longo de código.
