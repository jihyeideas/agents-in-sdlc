---
title: "Lição 8: Crie e faça merge do PR do recurso"
description: "Revise em conjunto a filtragem, as instruções, o skill, o perfil de QA e os testes; depois crie um PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação da filtragem, as instruções atualizadas, o skill personalizado, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma branch. Agora, você vai revisar tudo junto e abrir um pull request. Você fez o merge manualmente do PR de avaliação por estrelas; desta vez, vai deixar o **Agent Merge** gerenciar o processo.

> [!NOTE]
> Normalmente, dividiríamos o recurso, as instruções, o skill e o agente de QA em alguns PRs. Para simplificar o workshop, todo o trabalho de filtragem e qualidade ficou em uma conversa e branch, e será incluído em um único PR.

Nesta lição, você vai:

- entender o que é o Agent Merge e como ele automatiza o ciclo de vida de um PR;
- inspecionar as alterações completas do recurso e as evidências de verificação;
- criar o PR de filtragem;
- habilitar o Agent Merge somente após a revisão e confirmar que o PR foi mesclado.

## Cenário

Durante o fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. Agora, o Tailspin Toys quer automatizar o restante do trabalho do PR, mantendo o desenvolvedor responsável pela autorização do merge.

## Conheça o Agent Merge

O **Agent Merge** automatiza o trabalho restante para concluir um pull request. Quando habilitado, o Copilot resolve o que estiver bloqueando o PR — corrige verificações de integração contínua (CI) que falharam, responde a comentários da revisão e faz rebase quando necessário — e então habilita o merge automático do GitHub se o repositório permitir.

Até aqui, você mesmo selecionou **Merge pull request**. O Agent Merge pode assumir essa responsabilidade. Antes de habilitá-lo, revise o trabalho e decida se está pronto.

## Use o Agent Merge para gerenciar o PR

Com o código pronto, revise as alterações, crie o PR e deixe que o Agent Merge cuide do restante.

1. Volte ao Codespace.
2. Digite `/agent` para abrir o diálogo do agente.
3. Selecione **Default** e pressione <kbd>Enter</kbd>.
4. Crie um novo PR com o comando `/pr create`.
5. Ative o Agent Merge com `/pr agentmerge`.
6. O Copilot vai acompanhar a integração contínua do PR. Quando tudo passar, ele fará o merge.
7. Confirme que o Copilot exibiu uma mensagem semelhante a “PR #14 was squash-merged successfully”.

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de merge, configurações do repositório ou permissões ausentes. Se o processo for bloqueado, leia o motivo e conclua manualmente o merge revisado quando o repositório permitir.

## Resumo e próximos passos

Você automatizou várias partes do desenvolvimento: geração de código, testes e validação e, agora, o processo do pull request. Nesta lição, você:

- aprendeu o que é o Agent Merge e como ele automatiza o ciclo de vida de um PR;
- inspecionou as alterações completas do recurso e as evidências de verificação;
- criou o PR de filtragem;
- habilitou o Agent Merge após a revisão e confirmou que o PR foi mesclado.

Em seguida, você vai [explorar comandos de barra do Copilot CLI][next-lesson] para gerenciar contexto, modelos, sessões compartilhadas e delegação opcional ao agente na nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
