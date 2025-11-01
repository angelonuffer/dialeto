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
    - **gramática.separador** (texto, opcional) - String usada ao concatenar partes quando formato == "texto". Valor padrão: "" (string vazia).

### Retorno

- **retorno** (objeto) - Um objeto contendo o resultado da análise.
  - **retorno.sucesso** (número) - Indica se a análise foi bem-sucedida (1) ou não (0).
  - **retorno.valor** (texto ou lista) - O valor correspondente à entrada analisada, se a análise for bem-sucedida. Para gramáticas do tipo "sequência" com formato "lista", o valor é uma lista; caso contrário, é texto.

### Exemplos

#### Símbolo

```
dialeto.analisar({
  entrada: "hello"
  gramática: {
    tipo: "símbolo"
    texto: "hello"
  }
})
// Retorna: { sucesso: 1, valor: "hello" }
```

#### Faixa

```
dialeto.analisar({
  entrada: "5"
  gramática: {
    tipo: "faixa"
    de: "0"
    até: "9"
  }
})
// Retorna: { sucesso: 1, valor: "5" }
```

#### Sequência com formato "texto"

```
dialeto.analisar({
  entrada: "hi"
  gramática: {
    tipo: "sequência"
    formato: "texto"
    partes: [
      { tipo: "símbolo", texto: "h" }
      { tipo: "símbolo", texto: "i" }
    ]
  }
})
// Retorna: { sucesso: 1, valor: "hi" }
```

#### Sequência com formato "lista"

```
dialeto.analisar({
  entrada: "a7"
  gramática: {
    tipo: "sequência"
    formato: "lista"
    partes: [
      { tipo: "símbolo", texto: "a" }
      { tipo: "faixa", de: "0", até: "9" }
    ]
  }
})
// Retorna: { sucesso: 1, valor: ["a", "7"] }
```

#### Sequência com separador

```
dialeto.analisar({
  entrada: "abc"
  gramática: {
    tipo: "sequência"
    formato: "texto"
    separador: "-"
    partes: [
      { tipo: "símbolo", texto: "a" }
      { tipo: "símbolo", texto: "b" }
      { tipo: "símbolo", texto: "c" }
    ]
  }
})
// Retorna: { sucesso: 1, valor: "a-b-c" }
```