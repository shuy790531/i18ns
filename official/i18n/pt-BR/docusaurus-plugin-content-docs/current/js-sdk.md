---
sidebar_position: 5
---

# JS SDK

O Immersive Translate JS SDK ajuda você a implementar tradução bilíngue em seu site.

## Como Usar

1. Inicialize o Immersive Translate:

```js
<script>
  window.immersiveTranslateConfig = {
    pageRule: {}
  }
</script>
```

2. Adicione o seguinte código `script` à sua página web

```html
<script src="https://download.immersivetranslate.com/immersive-translate-sdk-latest.js"></script>
```

Exemplo

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Immersive Translate JS SDK</title>
    <script>
      window.immersiveTranslateConfig = {
        pageRule: {},
      };
    </script>
    <script
      async
      src="https://download.immersivetranslate.com/immersive-translate-sdk-latest.js"
    ></script>
  </head>

  <body>
    <div>
      <p>
        Night gathers, and now my watch begins. It shall not end until my death.
        I shall take no wife, hold no lands, father no children. I shall wear no
        crowns and win no glory. I shall live and die at my post.
      </p>
    </div>
  </body>
</html>
```

## Parâmetros

Com `pageRule`, você pode personalizar a configuração do site, decidindo qual conteúdo precisa ser traduzido ou ajustando os estilos da página.

```js
initImmersiveTranslate({
  pageRule: {
    selectors: [".text"],
    excludeSelectors: ["nav", "footer"],
  },
});
```

Usar `selectors` substituirá o intervalo de tradução inteligente, traduzindo apenas elementos correspondentes ao seletor.

Usar `excludeSelectors` pode excluir elementos da tradução.

Usar `selectors.add` adicionará alguns seletores além dos padrões.

Usar `selectors.remove` removerá alguns seletores dos padrões.

Se você quiser traduzir uma área específica e considerar um elemento como um todo sem dividi-lo em linhas, você pode usar o seletor `atomicBlockSelectors`. Note que você precisa selecionar elementos usando `selectors` antes de usar `atomicBlockSelectors`.

```json
{
  "selectors": ["div._aa_c h1", "li._acaz div[role=\"menuitem\"]"],
  "atomicBlockSelectors": ["div._aa_c h1", "li._acaz div[role=\"menuitem\"]"]
}
```

Mais explicações sobre parâmetros de `pageRule`:

```typescript
export interface PageRule {
  excludeMatches?: string | string[]; // Excluir sites específicos.
  selectorMatches?: string | string[]; // Correspondência usando seletores sem especificar todos os URLs
  excludeSelectorMatches?: string | string[]; // Regras de exclusão, igual ao acima.

  // Especificar intervalo de tradução
  selectors?: string | string[]; // Traduzir apenas elementos correspondentes
  excludeSelectors?: string | string[]; // Excluir elementos, não traduzir elementos correspondentes
  excludeTags?: string | string[]; // Excluir tags, não traduzir tags correspondentes

  // Adicionar intervalo de tradução, não substituir
  additionalSelectors?: string | string[]; // Adicionar intervalo de tradução. Adicionar posições de tradução em áreas de tradução inteligente.
  additionalExcludeSelectors?: string | string[]; // Adicionar elementos excluídos para evitar tradução inteligente em posições específicas.
  additionalExcludeTags?: string | string[]; // Adicionar tags excluídas

  // Manter original
  stayOriginalSelectors?: string | string[]; // Elementos correspondentes permanecerão originais. Comumente usado para tags em sites de fóruns.
  stayOriginalTags?: string | string[]; // Tags correspondentes permanecerão originais, como `code`

  // Tradução de região
  atomicBlockSelectors?: string | string[]; // Seletor de região, elementos correspondentes serão considerados como um todo, não traduzidos em segmentos
  atomicBlockTags?: string | string[]; // Seletor de tag de região, igual ao acima

  // Bloco ou Inline
  extraBlockSelectors?: string | string[]; // Seletores extras, elementos correspondentes serão tratados como elementos de bloco, ocupando uma linha.
  extraInlineSelectors?: string | string[]; // Seletores extras, elementos correspondentes serão tratados como elementos inline.

  inlineTags?: string | string[]; // Tags correspondentes serão tratadas como elementos inline
  preWhitespaceDetectedTags?: string | string[]; // Tags correspondentes automaticamente quebrarão linhas

  // Estilos de tradução
  translationClasses?: string | string | string[]; // Adicionar classes extras à tradução

  // Estilos globais
  globalStyles?: Record<string, string>; // Modificar estilos de página, útil quando traduções causam desordem na página.
  globalAttributes?: Record<string, Record<string, string>>; // Modificar atributos de elementos da página

  // Estilos embutidos
  injectedCss?: string | string[]; // Incorporar estilos CSS
  additionalInjectedCss?: string | string[]; // Adicionar estilos CSS em vez de substituir diretamente.

  // Contexto
  wrapperPrefix?: string; // Prefixo da área de tradução, padrão é inteligente, decide se deve quebrar linhas com base no número de caracteres.
  wrapperSuffix?: string; // Sufixo da área de tradução

  // Contagem de caracteres para quebra de tradução
  blockMinTextCount?: number; // Contagem mínima de caracteres para tradução como bloco, caso contrário, a tradução será um elemento inline.
  blockMinWordCount?: number; // Igual ao acima. Para sempre quebrar linhas, defina ambos como 0.

  // Contagem mínima de caracteres para conteúdo traduzível
  containerMinTextCount?: number; // Contagem mínima de caracteres para elementos serem traduzidos durante reconhecimento inteligente, padrão é 18
  paragraphMinTextCount?: number; // Contagem mínima de caracteres para parágrafo original, conteúdo maior que o número será traduzido
  paragraphMinWordCount?: number; // Contagem mínima de palavras para parágrafo original

  // Contagem de caracteres para quebra de linha forçada em parágrafos longos
  lineBreakMaxTextCount?: number; // Contagem máxima de caracteres para quebra de linha forçada ao traduzir parágrafos longos.

  // Momento para iniciar tradução
  urlChangeDelay?: number; // Atraso em milissegundos antes de iniciar tradução após entrar na página. Padrão é 250ms para aguardar inicialização da página.

  // Tradução de streaming AI
  aiRule: {
    streamingSelector: string; // Seletor de página GPT marcando o elemento em tradução
    messageWrapperSelector: string; // Seletor do corpo da mensagem
    streamingChange: boolean; // Atualização incremental ou completa para mensagens repetidas em páginas tipo GPT. GPT é incremental
  };
}
```
