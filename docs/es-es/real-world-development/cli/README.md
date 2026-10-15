---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Crea, verifica y entrega dos cambios de Tailspin Toys mientras aprendes los modos de Copilot CLI, sus personalizaciones, las herramientas MCP y la automatización de pull requests."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** incorpora GitHub Copilot a tu terminal como asistente de programación con agentes. Explora bases de código, genera código, ejecuta comandos y se conecta a herramientas externas, todo desde la línea de comandos, para que puedas mantener el flujo sin cambiar a un editor gráfico.

El taller sigue un flujo de trabajo continuo de Tailspin Toys:

1. Prepararás el proyecto en GitHub Codespaces, instalarás Copilot CLI y te familiarizarás con él.
2. Harás un cambio acotado para añadir valoraciones con estrellas, lo revisarás en el navegador y combinarás manualmente tu primer pull request (PR).
3. Partirás de la incidencia de filtrado, definirás el enfoque en el modo Plan, lo implementarás con Autopilot y lo revisarás en Interactive.
4. Actualizarás las instrucciones del repositorio y las aplicarás al trabajo de filtrado.
5. Personalizarás la habilidad existente `quality-checks` y la usarás para ejecutar las comprobaciones del proyecto.
6. Añadirás el servidor Model Context Protocol (MCP) de Playwright y lo usarás para explorar el filtrado en un navegador.
7. Crearás un agente personalizado de control de calidad (QA) para revisar los requisitos, la cobertura y las evidencias de verificación.
8. Revisarás todos los cambios del filtrado y usarás Agent Merge para su PR.
9. Explorarás comandos slash para gestionar el contexto, los modelos, el uso compartido y la delegación opcional a la nube.

Para mantener el taller centrado, crearás dos PR: primero el de las valoraciones con estrellas y después el del filtrado, con las actualizaciones de instrucciones y habilidades, el perfil de QA y las pruebas. El trabajo de filtrado y calidad comparte una conversación y una rama para que puedas aprovechar lo que has creado mientras exploras cada herramienta.

## Lecciones

| Lección | Tema | Descripción |
| ------ | ----- | ----------- |
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y Codespace |
| [1. Instala Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI y familiarízate con él |
| [2. Añade valoraciones con estrellas][ex2] | Primer cambio | Muestra las valoraciones existentes y el estado sin valorar; después combina tu primer PR |
| [3. Modos del agente: Plan y Autopilot][ex3] | Modos del agente | Planifica la funcionalidad desde su incidencia, créala con Autopilot y revísala en Interactive |
| [4. Guía a Copilot con instrucciones personalizadas][ex4] | Contexto | Explora y actualiza las instrucciones y aplícalas al filtrado |
| [5. Personaliza y usa una habilidad quality-checks][ex5] | Comprobaciones repetibles | Explora la habilidad existente, cambia el formato del informe y ejecútala |
| [6. Valida la funcionalidad con Playwright MCP][ex6] | Observación del navegador | Configura MCP en CLI y examina el comportamiento del filtrado |
| [7. Crea y usa un agente de QA][ex7] | Requisitos y cobertura | Crea y selecciona un perfil especializado y reúne evidencias finales |
| [8. Crea y combina el PR de la funcionalidad][ex8] | Revisión y combinación | Revisa todos los cambios, crea el PR y usa Agent Merge |
| [9. Comandos slash de GitHub Copilot CLI][ex9] | Funciones de CLI | Explora el contexto, los modelos, el uso compartido y la delegación opcional al agente en la nube |
| [10. Resumen y siguientes pasos][ex10] | Resumen | Repasa el flujo, las personalizaciones reutilizables y otros recursos |
| [Opcional: incorpora Foundry][foundry] | Agentes hospedados | Prepara un modelo, despliega un agente basado en el catálogo y conéctalo al sitio |

## Requisitos previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo de **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Permiso para crear un repositorio y un Codespace
- [ ] Conocimientos básicos de operaciones de terminal o línea de comandos

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis a través de [GitHub Education][student-plan]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que utiliza este taller.

> [!NOTE]
> Si usas Copilot Business o Copilot Enterprise, asegúrate de que tu administrador haya habilitado Copilot CLI.

## Empieza

**[Empieza con los requisitos previos →][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
[student-plan]: https://github.com/education/students
