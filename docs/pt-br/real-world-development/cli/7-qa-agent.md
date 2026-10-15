---
title: "Lição 7: Crie e use um agente de QA"
description: "Crie um agente personalizado de QA que combina os requisitos da issue, o skill quality-checks e o Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você usou o skill `quality-checks` para executar verificações automatizadas e o Playwright MCP para observar a experiência de filtragem em um navegador. Agora, vai reunir esses recursos em um agente personalizado com um processo de QA bem definido.

Nesta lição, você vai:

- explorar como um agente personalizado trabalha com instruções, skills e ferramentas MCP;
- criar e inspecionar um perfil reutilizável de garantia de qualidade;
- selecionar o agente de QA e revisar as descobertas com base na issue de filtragem.

## Cenário

Antes de abrir um pull request (PR), o Tailspin Toys quer revisar de forma consistente os requisitos, a qualidade do código, as verificações automatizadas, a cobertura de testes e o comportamento no navegador. Um agente personalizado pode coordenar esse processo de QA e gerar um relatório reutilizável.

## O que é um agente personalizado?

Um agente personalizado é uma versão especializada do Copilot definida em um perfil Markdown. O perfil descreve a finalidade, as instruções e as ferramentas disponíveis para o agente. Neste workshop, você vai definir uma função de QA em `.github/agents/qa.agent.md` e selecioná-la no Copilot CLI.

As personalizações usadas até agora têm funções diferentes. As instruções do repositório descrevem os padrões da equipe; o skill `quality-checks` reúne verificações repetíveis; o Playwright MCP fornece ferramentas de navegador; e o perfil de QA orienta o Copilot a combinar esses recursos para avaliar requisitos e relatar descobertas. Ele não substitui as outras personalizações nem exige outra conversa.

## Crie o perfil de QA

Antes de abrir o PR do recurso, peça ao Copilot que crie um perfil reutilizável de QA. O perfil vai definir as verificações e os limites que o QA deve respeitar.

1. Volte ao Codespace e confirme que a conversa de filtragem está no modo Interactive.
2. Peça ao agente padrão que crie o agente personalizado:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Inspecione o perfil

Antes de usar o agente, revise o perfil para confirmar que ele inclui o fluxo e os limites de QA desejados.

1. Digite `/diff` e abra `.github/agents/qa.agent.md`.
2. Leia o frontmatter. `description` é obrigatório; `name` é opcional, mas fornece um nome de exibição.
3. Confirme que as instruções fazem o QA começar pelos requisitos, seguir as instruções do repositório, executar o skill `quality-checks` e usar o Playwright MCP.
4. Confirme que o QA informa evidências, pede autorização antes de alterar o código de implementação e não faz commits nem abre pull requests.
5. Se faltar alguma responsabilidade ou limite, peça ao agente padrão que revise o perfil antes de continuar.

## Execute o QA com base na issue

O Copilot CLI carrega os agentes do projeto quando uma conversa começa. Depois de criar o perfil, retome a mesma conversa de filtragem e selecione QA para usar a issue e as decisões do planejamento.

1. Ative o agente usando este prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como o agente acabou de ser criado, talvez ele ainda não apareça na lista. O comando acima vai ativá-lo mesmo assim.

2. Peça ao agente de QA que revise o recurso:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. O agente de QA vai começar a trabalhar.
4. Leia o relatório quando ele terminar.

## Resumo e próximos passos

Você adicionou uma função especializada reutilizável e revisou o trabalho dela. Nesta lição, você:

- explorou como um agente personalizado trabalha com instruções, skills e ferramentas MCP;
- criou e inspecionou um perfil reutilizável de garantia de qualidade;
- selecionou o agente de QA e revisou suas descobertas com base na issue.

A implementação, a atualização do skill, o perfil de QA, os testes e o relatório de verificação estão prontos para revisão. Em seguida, você vai [reuni-los em um PR de recurso e usar o Agent Merge][next-lesson].

## Recursos

- [Criar agentes personalizados para o Copilot CLI][create-agents]
- [Configuração de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
