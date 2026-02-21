# Exemplos de uso do `dialeto`

Este documento fornece exemplos práticos de como usar a biblioteca `dialeto` para analisar e gerar textos usando diferentes tipos de gramáticas.

## Símbolo

O tipo `símbolo` corresponde a um texto exato.

### Analisar
```
resultado = dialeto.analisar({
  entrada: "olá"
  gramática: {
    tipo: "símbolo"
    texto: "olá"
  }
})
# resultado.sucesso == 1
# resultado.valor == "olá"
```

### Gerar
```
resultado = dialeto.gerar({
  valor: "olá"
  gramática: {
    tipo: "símbolo"
    texto: "olá"
  }
})
# resultado.sucesso == 1
# resultado.saída == "olá"
```

---

## Faixa

O tipo `faixa` corresponde a qualquer caractere dentro de um intervalo especificado.

### Analisar
```
resultado = dialeto.analisar({
  entrada: "b"
  gramática: {
    tipo: "faixa"
    de: "a"
    até: "z"
  }
})
# resultado.sucesso == 1
# resultado.valor == "b"
```

### Gerar
```
resultado = dialeto.gerar({
  valor: "b"
  gramática: {
    tipo: "faixa"
    de: "a"
    até: "z"
  }
})
# resultado.sucesso == 1
# resultado.saída == "b"
```

---

## Sequência

O tipo `sequência` combina várias gramáticas em uma ordem específica. Pode retornar o resultado como texto, lista ou objeto.

### Formato Texto
```
resultado = dialeto.analisar({
  entrada: "ab"
  gramática: {
    tipo: "sequência"
    partes: [
      { tipo: "símbolo" texto: "a" }
      { tipo: "símbolo" texto: "b" }
    ]
    formato: "texto"
  }
})
# resultado.valor == "ab"
```

### Formato Lista
```
resultado = dialeto.analisar({
  entrada: "ab"
  gramática: {
    tipo: "sequência"
    partes: [
      { tipo: "símbolo" texto: "a" }
      { tipo: "símbolo" texto: "b" }
    ]
    formato: "lista"
  }
})
# resultado.valor == ["a" "b"]
```

### Formato Objeto
```
resultado = dialeto.analisar({
  entrada: "ab"
  gramática: {
    tipo: "sequência"
    partes: [
      { nome: "primeiro" gramatica: { tipo: "símbolo" texto: "a" } }
      { nome: "segundo" gramatica: { tipo: "símbolo" texto: "b" } }
    ]
    formato: "objeto"
  }
})
# resultado.valor == { primeiro: "a" segundo: "b" }
```

---

## Alternativa

O tipo `alternativa` tenta corresponder a qualquer uma das opções fornecidas.

### Analisar
```
resultado = dialeto.analisar({
  entrada: "carro"
  gramática: {
    tipo: "alternativa"
    opções: [
      { tipo: "símbolo" texto: "carro" }
      { tipo: "símbolo" texto: "moto" }
    ]
  }
})
# resultado.sucesso == 1
# resultado.valor == "carro"
```

---

## Opcional

O tipo `opcional` permite que uma gramática esteja presente ou ausente.

### Analisar
```
gramática_opcional = {
  tipo: "opcional"
  gramática: { tipo: "símbolo" texto: "talvez" }
}

# Com a entrada presente:
dialeto.analisar({ entrada: "talvez" gramática: gramática_opcional }).valor == "talvez"

# Com a entrada ausente:
dialeto.analisar({ entrada: "" gramática: gramática_opcional }).valor == ""
```

---

## Repetição

O tipo `repetição` permite que uma gramática ocorra múltiplas vezes.

### Analisar (1 ou mais)
```
resultado = dialeto.analisar({
  entrada: "aaa"
  gramática: {
    tipo: "repetição"
    gramática: { tipo: "símbolo" texto: "a" }
    formato: "texto"
    minimo: 1
  }
})
# resultado.valor == "aaa"
```

### Analisar (com limites)
```
resultado = dialeto.analisar({
  entrada: "aa"
  gramática: {
    tipo: "repetição"
    gramática: { tipo: "símbolo" texto: "a" }
    formato: "lista"
    minimo: 2
    maximo: 2
  }
})
# resultado.valor == ["a" "a"]
```

---

## Negação

O tipo `negação` tem sucesso se a sub-gramática falhar, consumindo um caractere.

### Analisar
```
resultado = dialeto.analisar({
  entrada: "b"
  gramática: {
    tipo: "negação"
    gramática: { tipo: "símbolo" texto: "a" }
  }
})
# resultado.sucesso == 1
# resultado.valor == "b" (sucesso porque "b" não é "a")
```
