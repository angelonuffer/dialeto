# dialeto

Este projeto implementa um avaliador de gramática simples para textos, com suporte a faixas de caracteres. Ele permite verificar se uma entrada está dentro de uma faixa definida.

## Como executar os testes

Os testes são executados automaticamente via GitHub Actions (workflow em `.github/workflows/IC.yml`). Para rodar localmente:

1. Instale Node.js 22.
2. Execute:
   ```sh
   node 0/código/0_node.js testes/0 node | node
   ```

## Exemplo de uso

```
dialeto.avaliar({
  entrada: "b"
  gramática: {
    tipo: "texto"
    faixa: {
      de: "a"
      até: "c"
    }
  }
})
// Retorna: { sucesso: 1 valor: "b" }
```