# Null vs. Undefined

JavaScript \(e, por extensão, TypeScript \) tem dois tipos inferiores: `null` e `undefined`. Eles têm a intenção de significar coisas diferentes:

* Algo não foi inicializado: `undefined`.
* Algo está indisponível no momento: `null`.

## Verificando para qualquer

Fato é que você precisará lidar com ambos. Para esse caso usamos simplesmente o `==` para checar.

```typescript
/// Imagine que você está fazendo `foo.bar == undefined` onde bar pode ser uma das seguintes:
console.log(undefined == undefined); // true
console.log(null == undefined); // true

// Você não precisa se preocupar com valores falsos efetuados por meio dessa verificação
console.log(0 == undefined); // false
console.log('' == undefined); // false
console.log(false == undefined); // false
```

Recomendo `== null` para verificar ambos `undefined` ou `null`. Você geralmente não quer fazer uma distinção entre os dois.

```typescript
function foo(arg: string | null | undefined) {
  if (arg != null) {
    // arg deve ser uma string tal como a`!=` condição exclui os dois, null e undefined. 
  }
}
```

Uma exceção, os valores indefinidos no nível raiz que discutiremos a seguir.

## Verificando nível de raiz undefined

Lembre-se de como eu disse que você deveria usar `== null`. Claro que sim \(porque acabei de dizer ^ \). Não o use para coisas no nível da raiz. No modo **strict**, se você usa `foo` e `foo` como undefined, você obtém uma **exceção** `ReferenceError` e toda a pilha de chamadas é desativada.

> Você deve usar o modo strict ... e, de fato, o compilador TS o inserirá para você se você usar os módulos ... mais sobre isso mais tarde no livro, assim você não tem que ser explícito sobre isso :\)

Então, para verificar se uma variável é definida ou não em um nível _global_ você normalmente usa `typeof`:

```typescript
if (typeof someglobal !== 'undefined') {
  // someglobal agora é seguro de usar
  console.log(someglobal);
}
```

## Limite o uso explícito de `undefined`

Como o TypeScript oferece a oportunidade de _documentar_ suas estruturas separadamente dos valores, em vez de coisas como:

```typescript
function foo(){
  // Se for alguma coisa
  return {a:1,b:2};
  // outro caso
  return {a:1,b:undefined};
}
```

você deve usar uma anotação de tipo:

```typescript
function foo():{a:number,b?:number}{
  // Se for alguma coisa
  return {a:1,b:2};
  // outro caso
  return {a:1};
}
```

## Estilos de callbacks no Node

As funções de retorno de chamada ou callbacks no node\(por exemplo, `(err, somethingElse) => {/* something */}` \) são geralmente chamadas com `err` definido como `null` se não houver um erro. Você geralmente usa uma verificação de verdade para isso de qualquer maneira:

```typescript
fs.readFile('someFile', 'utf8', (err,data) => {
  if (err) {
    // faça alguma coisa
  } else {
    // sem erro
  }
});
```

Ao criar suas próprias APIs, é _normal_ usar `null` nesse caso para obter consistência. Com toda a sinceridade para suas próprias APIs, você deve considerar suas _promises_; nesse caso, você realmente não precisa se preocupar com valores de erro ausentes \(você os trata com `.then` vs.` .catch` \).

## Não use `undefined` como meio de denotar _validade_

Por exemplo, uma função horrível como esta:

```typescript
function toInt(str:string) {
  return str ? parseInt(str) : undefined;
}
```

pode ser muito melhor desse jeito:

```typescript
function toInt(str: string): { valid: boolean, int?: number } {
  const int = parseInt(str);
  if (isNaN(int)) {
    return { valid: false };
  }
  else {
    return { valid: true, int };
  }
}
```

## Considerações finais

A equipe do TypeScript não usa `null`: [Diretrizes de codificação do TypeScript](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines#null-and-undefined) e não causa nenhum problema. Douglas Crockford acha que [`null` é uma péssima idéia](https://www.youtube.com/watch?v=PSGEjv3Tqo0&feature=youtu.be&t=9m21s) e todos nós devemos apenas usar `undefined`.

No entanto, as bases de código no estilo NodeJS usam `null` para argumentos de erro como padrão, pois denota `algo está indisponível no momento`. Pessoalmente, não me importo em distinguir entre os dois, pois a maioria dos projetos usa bibliotecas com opiniões diferentes e apenas descarta os dois com `== null`.

