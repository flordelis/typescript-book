# @types

[Definitivamente Typed](https://github.com/DefinitelyTyped/DefinitelyTyped) é um dos maiores pontos fortes do TypeScript. A comunidade foi adiante e **documentou** a natureza de quase 90% dos principais projetos de JavaScript existentes.

Isso significa que você pode usar esses projetos de uma maneira muito interativa e exploratória, não é necessário ter os documentos abertos em uma janela separada e garantir que você não cometa erros de digitação.

## Usando `@types`

A instalação é bastante simples, porque funciona apenas no topo do `npm`. Então, como um exemplo, você pode instalar definições de tipo para `jquery` simplesmente como:

```text
npm install @types/jquery --save-dev
```

`@types` suporta as definições de tipo _global_ tanto como _module_.

### Global `@types`

Por padrão, quaisquer definições que suportam o consumo global são incluídas automaticamente. Por exemplo. Para o jquery, você deve começar a usar `$` _globalmente_ em seu projeto.

No entanto, para _bibliotecas_ \(como `jquery`\), geralmente recomendo usar _módulos_:

### Module `@types`

Após a instalação, nenhuma configuração especial é realmente necessária. Você apenas importa-o como um módulo, ex.:

```typescript
import * as $ from "jquery";

// Use $ à vontade neste módulo 😁
```

## Controlando as variáveis globais

Como pode ser visto, ter uma definição que permita o vazamento global automaticamente pode ser um problema para algumas equipes. Assim, você pode optar por trazer _explicitamente_ apenas os tipos que fazem sentido usando o `compilerOptions.types` `tsconfig.json`, por exemplo:

```javascript
{
    "compilerOptions": {
        "types" : [
            "jquery"
        ]
    }
}
```

O exemplo acima mostra um exemplo onde somente o `jquery` poderá ser usado. Mesmo que a pessoa instale outra definição como o `npm install @types/node` seus globals \(por exemplo, [`process`](https://nodejs.org/api/process.html)\) não irão vazar para o seu código até que você os inclua na opção **types** no `tsconfig.json`.

