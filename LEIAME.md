# Dialeto

Esta biblioteca implementa um analisador que valida a entrada de acordo com a gramática definida e retorna o valor correspondente. Também fornece uma função geradora que faz o inverso, validando um valor e gerando a saída correspondente.

## dialeto.analisar

Esta função analisa a entrada fornecida de acordo com a gramática especificada.

### Parâmetros

- **entrada** (texto) - A entrada a ser analisada.
- **gramática** (objeto) - O objeto de gramática que define as regras de análise.
  - **gramática.tipo** (texto) - O tipo de gramática a ser utilizada.

  - Se **gramática.tipo** == "símbolo":
    - **gramática.texto** (texto) - O texto a ser comparado.

  - Se **gramática.tipo** == "faixa":
    - **gramática.de** (texto) - O limite inferior da faixa.
    - **gramática.até** (texto) - O limite superior da faixa.

  - Se **gramática.tipo** == "sequência":
    - **gramática.partes** (lista) - Lista de objetos de gramática. Cada item é outra gramática válida. Se **gramática.formato** == "objeto", cada item deve ter os campos **nome** (texto - chave de saída/entrada) e **gramatica** (objeto - sub-gramática).
    - **gramática.formato** (texto) - Formato de retorno, pode ser "texto", "lista" ou "objeto".

  - Se **gramática.tipo** == "alternativa":
    - **gramática.opções** (lista) - Lista de objetos de gramática. Cada item é outra gramática válida. A análise terá sucesso se qualquer uma das opções corresponder à entrada.

  - Se **gramática.tipo** == "opcional":
    - **gramática.gramática** (objeto) - Objeto de gramática. A análise terá sucesso se a gramática corresponder à entrada ou se a entrada for vazia, retornando uma string vazia neste caso.

  - Se **gramática.tipo** == "repetição":
    - **gramática.gramática** (objeto) - A sub-gramática que será repetida (obrigatório).
    - **gramática.formato** (texto) - Formato de retorno, pode ser "texto" ou "lista".
    - **gramática.minimo** (número, opcional) - Mínimo de ocorrências exigidas. Padrão: 1.
    - **gramática.maximo** (número, opcional) - Máximo de ocorrências permitidas. Omitir para ilimitado.

### Retorno

- **retorno** (objeto) - Um objeto contendo o resultado da análise.
  - **retorno.sucesso** (número) - Indica se a análise foi bem-sucedida (1) ou não (0).
  - **retorno.valor** (texto | lista | objeto) - O valor correspondente à entrada analisada, se a análise for bem-sucedida. Se **gramática.formato** == "objeto", retorna um objeto mapeando nomes de partes para valores analisados.

  - **retorno.pos** (número) - A posição na entrada onde a análise falhou.
  - **retorno.esperado** (texto) - A descrição do que era esperado pela gramática.
  - **retorno.encontrado** (texto) - O que foi realmente encontrado na entrada.

## dialeto.gerar

Esta função faz o inverso de `dialeto.analisar`. Ela recebe um valor e uma gramática, valida se o valor pode ser gerado pela gramática e retorna a saída correspondente.

### Parâmetros

- **valor** (texto | lista | objeto) - O valor a ser validado e convertido em saída. Se a gramática usa formato "objeto", deve ser um objeto mapeando nomes de partes para valores.
- **gramática** (objeto) - O objeto de gramática que define as regras de geração. Mesma estrutura da função `dialeto.analisar`.
  - **gramática.tipo** (texto) - O tipo de gramática a ser utilizada.

  - Se **gramática.tipo** == "símbolo":
    - **gramática.texto** (texto) - O texto esperado. O valor deve ser igual a este texto.

  - Se **gramática.tipo** == "faixa":
    - **gramática.de** (texto) - O limite inferior da faixa.
    - **gramática.até** (texto) - O limite superior da faixa. O valor deve ser um caractere único dentro desta faixa.

  - Se **gramática.tipo** == "sequência":
    - **gramática.partes** (lista) - Lista de objetos de gramática. Cada item é outra gramática válida. Se **gramática.formato** == "objeto", cada item deve ter os campos **nome** (texto - chave de entrada) e **gramatica** (objeto - sub-gramática).
    - **gramática.formato** (texto) - Formato esperado do valor:
      - Se "texto": o valor deve ser um texto que pode ser analisado sequencialmente pelas partes.
      - Se "lista": o valor deve ser uma lista onde cada elemento corresponde a uma parte.
      - Se "objeto": o valor deve ser um objeto onde cada chave corresponde ao **nome** de uma parte e o valor correspondente é gerado pela sub-gramática.

  - Se **gramática.tipo** == "alternativa":
    - **gramática.opções** (lista) - Lista de objetos de gramática. O valor deve corresponder a pelo menos uma das opções.

  - Se **gramática.tipo** == "opcional":
    - **gramática.gramática** (objeto) - Objeto de gramática. O valor pode ser uma string vazia ou corresponder à gramática.

  - Se **gramática.tipo** == "repetição":
    - **gramática.gramática** (objeto) - A sub-gramática que será repetida (obrigatório).
    - **gramática.formato** (texto) - Formato esperado do valor:
      - Se "texto": o valor deve ser um texto que pode ser analisado como repetições da sub-gramática.
      - Se "lista": o valor deve ser uma lista onde cada elemento corresponde a uma repetição.
    - **gramática.minimo** (número, opcional) - Mínimo de ocorrências exigidas. Padrão: 1.
    - **gramática.maximo** (número, opcional) - Máximo de ocorrências permitidas. Omitir para ilimitado.

### Retorno

- **retorno** (objeto) - Um objeto contendo o resultado da geração.
  - **retorno.sucesso** (número) - Indica se a geração foi bem-sucedida (1) ou não (0).
  - **retorno.saída** (texto) - A saída gerada, se a geração for bem-sucedida.