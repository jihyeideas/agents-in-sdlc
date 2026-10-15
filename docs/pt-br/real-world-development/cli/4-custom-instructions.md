---
title: "Lição 4: Oriente o Copilot com instruções personalizadas"
description: "Explore as instruções do repositório, adicione um padrão de documentação e aplique-o ao código de filtragem."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O contexto é fundamental ao trabalhar com IA generativa. Se uma tarefa precisa ser feita de uma maneira específica, forneça essa orientação ao Copilot. Os [arquivos de instruções][instruction-files] descrevem não apenas *qual* código você quer, mas também *como* ele deve ser estruturado. Agora que você criou a filtragem, vai explorar as instruções usadas pelo Copilot, adicionar um padrão de documentação e aplicá-lo ao código.

Nesta lição, você vai:

- explorar como as instruções do repositório e as instruções específicas de caminhos chegam ao agente;
- atualizar o arquivo de instruções para exigir o cumprimento dos padrões de código;
- observar o impacto dos arquivos de instruções no código.

## Cenário

O Tailspin Toys tem diretrizes para as práticas de desenvolvimento, incluindo:

- Comentários devem explicar a intenção e decisões que não são óbvias, em vez de repetir o código.
- Funções exportadas em `db/` e `src/lib/` devem documentar finalidade, parâmetros e valores de retorno com TSDoc/JSDoc, incluindo um argumento `db` injetável quando houver.
- Componentes Astro reutilizáveis devem documentar seus contratos `Props`, e os comentários precisam acompanhar as alterações no código relacionado.
- As orientações atuais de formatação e lint devem ser preservadas.

Com arquivos de instruções, você garante que o Copilot tenha as informações necessárias para seguir essas práticas.

## Arquivos de instruções

As instruções personalizadas fornecem contexto e preferências para ajudar o Copilot a entender seu estilo de desenvolvimento e seus requisitos. Você pode indicar convenções de código, bibliotecas e os comentários que devem ser incluídos. As instruções podem valer para todo o repositório ou para tipos específicos de arquivo.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`, um único arquivo enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter orientações gerais sobre o projeto.
- `.github/instructions/*.instructions.md`, arquivos com diretrizes para linguagens, tipos de arquivo ou tarefas específicas.

> [!NOTE]
> O suporte a outros formatos de instrução varia conforme o ambiente. Consulte a [referência de suporte a instruções personalizadas][custom-instructions-support] antes de depender de um formato específico.

## Explore os arquivos de instruções personalizadas do projeto

O projeto inicial já inclui arquivos de instruções. Explore-os antes de fazer alterações para entender seu efeito.

1. Volte ao Codespace.
2. No editor do Codespaces (não no terminal), abra `.github/copilot-instructions.md`.
3. Leia a breve descrição do projeto e as orientações de código. Essas instruções se aplicam a todas as interações com o Copilot neste repositório.
4. Explore os arquivos na pasta `.github/instructions`, incluindo os de Astro, Drizzle e testes.
5. Abra `.github/instructions/unit-tests.instructions.md` e observe o campo `applyTo`: o glob determina a quais arquivos as instruções se aplicam.
6. Abra `.github/instructions/drizzle.instructions.md` e examine os links para outros arquivos de instruções e arquivos existentes do projeto.

> [!NOTE]
> As instruções do projeto documentam os padrões de desenvolvimento, mas ainda não exigem comentários TSDoc em TypeScript. Você vai adicionar essa exigência nas próximas etapas.

## Explore os arquivos de instruções personalizadas do projeto

O projeto inicial inclui um arquivo `copilot-instructions.md` e vários arquivos `*.instructions.md` para tarefas diferentes. Explore-os antes de fazer alterações.

1. Volte ao Codespace.
2. No editor do Codespaces (não no terminal), abra `.github/copilot-instructions.md`.
3. Leia a breve descrição do projeto e as orientações. Elas se aplicam a todas as interações com o Copilot neste repositório.
4. Explore os arquivos da pasta `.github/instructions`, que incluem orientações para Astro, a camada de dados do Drizzle, testes e outros tópicos.
5. Abra `.github/instructions/unit-tests.instructions.md` e observe o campo `applyTo`: o glob determina a quais arquivos as instruções se aplicam. Neste caso, ele corresponde a arquivos de teste TypeScript, como `**/*.test.ts`.
6. Abra `.github/instructions/drizzle.instructions.md` e examine os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos do projeto. Assim, é possível dividir instruções extensas em arquivos menores e reutilizáveis e fornecer exemplos ao Copilot.

> [!NOTE]
> No IDE, os arquivos de instruções são usados para gerar código no Copilot Chat, não para conclusões de código ou sugestões da próxima edição. O Copilot Chat, o Copilot CLI e o Copilot cloud agent usam tanto as instruções do repositório quanto os arquivos `*.instructions.md` com frontmatter `applyTo`. O Copilot também oferece suporte a outros formatos, como AGENTS.md e CLAUDE.md.

## Atualize as instruções para refletir os padrões da equipe

O projeto inicial é um bom ponto de partida, mas falta uma regra. Atualize `.github/copilot-instructions.md` para exigir comentários TSDoc no novo TypeScript.

1. Abra `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting guidance**, que deve estar perto da linha 35.
3. Adicione este item ao final da seção:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

O arquivo será salvo automaticamente.

## Aplique as instruções atualizadas

O Copilot CLI carrega as instruções do repositório quando uma conversa começa. Saia e retome a conversa de filtragem para que o Copilot use as instruções novas sem perder o contexto do recurso.

1. Se a conversa de filtragem ainda estiver aberta, digite `/exit`. O Copilot CLI salva as conversas automaticamente.
2. Na raiz do repositório e na branch `game-filters-cli`, retome a conversa salva:

   ```bash
   copilot --resume
   ```

   Se solicitado, selecione a conversa de filtragem e confirme que a branch `game-filters-cli` está selecionada.
3. Peça ao Copilot que aplique as instruções atualizadas:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Digite `/diff` e revise os arquivos TypeScript alterados. Confirme que os novos comentários TSDoc descrevem o código corretamente.

## Resumo e próximos passos

Você explorou como o Copilot usa as instruções do repositório e aplicou um novo padrão. Nesta lição, você:

- explorou como as instruções do repositório e as específicas de caminhos chegam ao agente;
- atualizou as instruções para exigir os padrões de código;
- observou o impacto dos arquivos de instruções no código.

Em seguida, você vai personalizar e executar o skill reutilizável `quality-checks` para rodar lint e testes de forma consistente.

## Recursos

- [Adicionar instruções personalizadas ao Copilot CLI][instruction-files]
- [Suporte a instruções personalizadas][custom-instructions-support]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [Awesome Copilot: uma coleção de instruções e outros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
