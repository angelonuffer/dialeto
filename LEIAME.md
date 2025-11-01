# dialeto

Este projeto implementa um avaliador de gramática simples para textos, com suporte a faixas de caracteres e símbolos exatos. Ele permite verificar se uma entrada está dentro de uma faixa definida ou se corresponde exatamente a um símbolo especificado.

## Como executar os testes

Os testes são executados automaticamente via GitHub Actions (workflow em `.github/workflows/IC.yml`). Para rodar localmente:

1. Instale Node.js 22.
2. Execute:
   ```sh
   node 0/código/0_node.js testes/0 node | node
   ```

## Exemplos de uso

### Gramática de Faixa

Verifica se a entrada está dentro de um intervalo definido:

```
dialeto.analisar({
  entrada: "b"
  gramática: {
    tipo: "faixa"
    de: "a"
    até: "c"
  }
})
// Retorna: { sucesso: 1 valor: "b" }
```

### Gramática de Símbolo

Verifica se a entrada é exatamente igual ao texto especificado:

```
dialeto.analisar({
  entrada: "hello"
  gramática: {
    tipo: "símbolo"
    texto: "hello"
  }
})
// Retorna: { sucesso: 1 valor: "hello" }
```