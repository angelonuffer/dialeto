**Objetivo**: Instruções breves para desenvolver este repositório usando a linguagem 0.

- **Contexto**: Este repositório usa arquivos escritos na sintaxe da linguagem 0. O código-fonte fica em `código/` e os testes em `testes/` (arquivos com extensão `.0`).

- **Interpretador**: Sempre execute os testes com a versão mais recente do interpretador da linguagem 0 usando:

  `npx angelonuffer/0 testes/0`

  Use esse comando para validar mudanças antes de abrir PRs; inclua a saída no PR quando relevante.

- **Fluxo de desenvolvimento**:
  - Editar ou adicionar arquivos em `código/` seguindo a sintaxe da linguagem 0.
  - Colocar casos de teste em `testes/` (siga o padrão dos arquivos existentes).
  - Rodar `npx angelonuffer/0 testes/0` e corrigir erros até que todos os testes passem.

- **Boas práticas para commits e PRs**:
  - Execute `npx angelonuffer/0 testes/0` localmente e anexe a saída ao PR.
  - Mantenha mudanças pequenas e focadas; se adicionar novas funcionalidades, inclua testes correspondentes em `testes/`.
  - Documente mudanças relevantes no `LEIAME.md` ou em arquivos de documentação apropriados.

- **Escrever em sintaxe 0**:
  - Use arquivos `.0` para expressar código e testes seguindo a sintaxe da linguagem 0.
  - Preserve a estrutura e nomes de arquivos quando estiver adaptando testes já existentes.

- **Verificação rápida**:
  - Para validar apenas um teste ou pasta: `npx angelonuffer/0 testes/0` pode receber caminhos relativos quando aplicável.

- **Ajuda e referência**:
  - Repositório do interpretador: https://github.com/angelonuffer/0
  - Use esse repositório como referência de implementação e para entender atualizações do interpretador.

Se precisar, o mantenedor pode incluir exemplos mínimos de sintaxe 0 neste arquivo para guiar contribuições futuras.
