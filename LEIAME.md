# dialeto

Esta biblioteca implementa um analisador que valida a entrada de acordo com a gramática definida e retorna o valor correspondente. Também fornece uma função geradora que faz o inverso, validando um valor e gerando a saída correspondente.

## analisar : função

`{ entrada : texto gramática : objeto }` => `análise : objeto`

Analisa a entrada fornecida de acordo com a gramática especificada.

## gerar : função

`{ valor : qualquer gramática : objeto }` => `geração : objeto`

Faz o inverso de `analisar`. Recebe um valor e uma gramática, valida se o valor pode ser gerado pela gramática e retorna a saída correspondente.

## gramática : objeto

O objeto de gramática que define as regras de análise.

- `tipo : texto` - O tipo de gramática a ser utilizada.

- Se `tipo` == "símbolo":
  - `texto : texto` - O texto a ser comparado.

- Se `tipo` == "faixa":
  - `de : texto` - O limite inferior da faixa.
  - `até : texto` - O limite superior da faixa.

- Se `tipo` == "sequência":
  - `partes : lista` - Lista de objetos de gramática. Cada item é outra gramática válida. Se `formato` == "objeto", cada item deve ter os campos `nome : texto` (chave de saída/entrada) e `gramatica : objeto` (sub-gramática).
  - `formato : texto` - Formato de retorno, pode ser "texto", "lista" ou "objeto".

- Se `tipo` == "alternativa":
  - `opções : lista` - Lista de objetos de gramática. Cada item é outra gramática válida. A análise terá sucesso se qualquer uma das opções corresponder à entrada.

- Se `tipo` == "opcional":
  - `gramática : objeto` - Objeto de gramática. A análise terá sucesso se a gramática corresponder à entrada ou se a entrada for vazia, retornando uma string vazia neste caso.

- Se `tipo` == "repetição":
  - `gramática : objeto` - A sub-gramática que será repetida.
  - `formato : texto` - Formato de retorno, pode ser "texto" ou "lista".
  - `minimo : número` (opcional) - Mínimo de ocorrências exigidas. Padrão: 1.
  - `maximo : número` (opcional) - Máximo de ocorrências permitidas. Omitir para ilimitado.

- Se `tipo` == "negação":
  - `gramática : objeto` - A sub-gramática que será negada. A análise falha se a sub-gramática tiver sucesso e tem sucesso consumindo um caractere se a sub-gramática falhar.

## análise : objeto

Um objeto contendo o resultado da análise.

- `sucesso : número` - Indica se a análise foi bem-sucedida (1) ou não (0).
- `valor : texto | lista | objeto` - O valor correspondente à entrada analisada, se a análise for bem-sucedida. Se `formato` == "objeto", retorna um objeto mapeando nomes de partes para valores analisados.
- `pos : número` - A posição na entrada onde a análise falhou.
- `esperado : texto` - A descrição do que era esperado pela gramática.
- `encontrado : texto` - O que foi realmente encontrado na entrada.

## geração : objeto

Um objeto contendo o resultado da geração.

- `sucesso : número` - Indica se a geração foi bem-sucedida (1) ou não (0).
- `saída : texto` - A saída gerada, se a geração for bem-sucedida.