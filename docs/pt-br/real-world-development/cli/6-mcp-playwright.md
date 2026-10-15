---
title: "Lição 6: Valide a funcionalidade com o Playwright MCP"
description: "Inspecione ou configure o Playwright MCP no Copilot CLI e use-o para explorar o recurso de filtragem em um navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como já destacamos, desenvolver não é apenas escrever código. Também é preciso trabalhar com dados e serviços externos e permitir que o Copilot use automações adicionais. Os servidores MCP permitem ampliar as ferramentas e os serviços disponíveis no Copilot CLI.

Nesta lição, você vai:

- entender o que é o Model Context Protocol (MCP) e como o Copilot CLI o utiliza;
- adicionar o servidor Playwright MCP, caso ele ainda não esteja disponível;
- pedir ao agente que controle um navegador e explore o recurso de filtragem.

## Cenário

Testes de unidade e de ponta a ponta são importantes, mas validar alterações na interface exige interagir com ela. Você quer permitir que o Copilot use o site como uma pessoa usuária, automatizando melhor a validação das alterações.

## O que é o Model Context Protocol (MCP)?

O [Model Context Protocol (MCP)][mcp-blog-post] permite que agentes de IA se comuniquem com ferramentas e serviços externos em tempo real, acessem informações atualizadas e executem ações em seu nome.

Essas ferramentas e recursos são acessados por um servidor MCP, que atua como ponte entre o agente de IA e os serviços externos. Cada servidor MCP disponibiliza um conjunto diferente de ferramentas e recursos.

Alguns servidores MCP populares:

- **[GitHub MCP Server][github-mcp]**: fornece acesso às APIs para gerenciar repositórios, issues e pull requests do GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: oferece automação de navegador com o Playwright.

Há muitos outros servidores MCP disponíveis. O GitHub mantém um [registro de MCP][mcp-registry] para facilitar a descoberta e as contribuições ao ecossistema.

> [!CAUTION]
> Trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor, revise o código-fonte, verifique quem o publica e considere as implicações de segurança.

## Adicione o servidor Playwright MCP

Se o servidor Playwright MCP ainda não estiver disponível, adicione-o para que o Copilot possa interagir com o site.

> [!NOTE]
> Se o Playwright MCP já estiver configurado no Copilot CLI, pule estas etapas e continue na próxima seção.

1. Volte ao Codespace.
2. No Copilot CLI, digite o comando abaixo para abrir a caixa de diálogo de adição de servidor MCP:

   ```plaintext
   /mcp add
   ```

3. Digite `playwright` como nome e pressione <kbd>Tab</kbd>.
4. Pressione <kbd>Enter</kbd> para confirmar o tipo **STDIO** e depois pressione <kbd>Tab</kbd>.
5. Cole o texto abaixo na caixa de diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pressione <kbd>Control</kbd>+<kbd>S</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para salvar o servidor MCP.
7. Pressione <kbd>Esc</kbd> para sair da caixa de diálogo.

## Peça ao Copilot para explorar o recurso com o Playwright

Você confirmou manualmente que a funcionalidade funciona como esperado. Agora, use o Playwright MCP disponível no Copilot para fazer a mesma verificação.

1. Use este prompt para pedir que o Copilot valide a funcionalidade com o servidor Playwright MCP:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> Normalmente, não é necessário dizer ao Copilot para usar o servidor MCP, pois ele costuma identificá-lo sozinho. Mesmo assim, indicar a ferramenta pode orientar o trabalho e economizar alguns tokens.

2. Observe as etapas que o Copilot executa no navegador.
3. Leia o relatório e confirme se tudo está funcionando como esperado.

O Copilot vai iniciar o servidor, usar o Playwright para interagir com o site, parar o servidor e apresentar um relatório.

## Resumo e próximos passos

Você usou o servidor Playwright MCP para explorar o recurso em um navegador real pelo Copilot CLI. Nesta lição, você:

- aprendeu o que é MCP e como o Copilot CLI o utiliza;
- adicionou o servidor Playwright MCP, caso ele ainda não estivesse disponível;
- pediu ao agente que controlasse um navegador e explorasse o recurso.

Em seguida, você vai [criar um agente personalizado de QA][next-lesson] que combina o skill e as ferramentas do navegador.

## Recursos

- [O que é MCP e por que todos estão falando sobre isso?][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [Adicionar servidores MCP ao Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
