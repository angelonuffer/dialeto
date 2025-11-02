# Dialeto

Esta biblioteca implementa um analisador que valida a entrada de acordo com a gramática definida e retorna o valor correspondente.

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
    - **gramática.partes** (lista) - Lista de objetos de gramática. Cada item é outra gramática válida.
    - **gramática.formato** (texto) - Formato de retorno, pode ser "texto" ou "lista".

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
  - **retorno.valor** (texto | lista) - O valor correspondente à entrada analisada, se a análise for bem-sucedida.

  - **retorno.pos** (número) - A posição na entrada onde a análise falhou.
  - **retorno.esperado** (texto) - A descrição do que era esperado pela gramática.
  - **retorno.encontrado** (texto) - O que foi realmente encontrado na entrada.