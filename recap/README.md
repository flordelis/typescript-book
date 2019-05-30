# JavaScript

Havia \(e continuará a ter\) muitos competidores em _alguns compiladores de sintaxe_ para o _JavaScript_. TypeScript é diferente deles isso por que o _Seu JavaScript é o TypeScript_. Aqui está um diagrama:

![Seu JavaScript &#xE9; o TypeScript](https://raw.githubusercontent.com/overlineink/typescript-book/master/images/venn_pt.png)

No entanto, isso significa que _você só precisa conhecer JavaScript_ \(a boa notícia é _você **apenas** precisa aprender JavaScript_\). O TypeScript está apenas padronizando todas as maneiras que você fornece _uma boa documentação_ em JavaScript.

* Apenas dando-lhe uma nova sintaxe não ajuda a corrigir bugs \(olhando para você CoffeeScript\).
* Criando uma nova linguagem abstrai você muito longe de seus tempos de execução, comunidades \(olhando para você Dart\).

O TypeScript é apenas um JavaScript documentado.

## Tornando o JavaScript melhor

O TypeScript tentará protegê-lo de partes do JavaScript que nunca funcionaram \(então você não precisa se lembrar disso\):

```typescript
[] + []; // JavaScript vai te dar "" (o que faz pouco sentido), TypeScript vai reportar um erro

//
// outras coisas que são sem sentido no JavaScript
// - não lhe dão um erro de execução (dificultando a depuração)
// - mas o TypeScript lhe dará um erro em tempo de compilação (tornando a depuração desnecessária)
//
{} + []; // JS : 0, TS Erro
[] + {}; // JS : "[object Object]", TS Erro
{} + {}; // JS : NaN ou [object Object][object Object] dependendo do navegador, TS Erro
"hello" - 1; // JS : NaN, TS Erro

function add(a,b) {
  return
    a + b; // JS : undefined, TS Erro 'código inacessível detectado'
}
```

Essencialmente TypeScript faz lint dos erros do JavaScript. Apenas fazendo um trabalho melhor do que outros linters que não possuem _tipo de informações_.

## Você ainda precisa aprender JavaScript

Dito isso, o TypeScript é muito pragmático sobre o fato de que _você escreve JavaScript_, portanto, há algumas coisas sobre JavaScript que você ainda precisa saber para não ser pego de surpresa. Vamos discuti-los em seguida.

> Nota: O TypeScript é um superconjunto do JavaScript. Apenas com documentação que pode realmente ser usada por compiladores / IDEs ;\)

