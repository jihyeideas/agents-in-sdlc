---
title: "Lección 8: Crea y combina el PR de la funcionalidad"
description: "Revisa conjuntamente el filtrado, las instrucciones, la habilidad, el perfil de QA y las pruebas; después crea un PR y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las instrucciones actualizadas, la habilidad personalizada, el perfil de control de calidad (QA) y las pruebas están guardados en una rama. Ahora revisarás todos los cambios y abrirás un pull request. Combinaste manualmente el PR de valoración con estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente separaríamos la funcionalidad, las instrucciones, la habilidad y el agente de QA en varios PR. Para simplificar el taller, hemos mantenido todo el trabajo de filtrado y control de calidad en una conversación y una rama, y lo combinaremos en un único PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de un PR;
- inspeccionarás todos los cambios y las evidencias de verificación;
- crearás el PR de filtrado;
- habilitarás Agent Merge solo después de la revisión y confirmarás que el PR se ha combinado.

## Escenario

Durante el flujo de filtrado has usado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante del PR, sin perder el control del desarrollador sobre la autorización para combinarlo.

## Introducción a Agent Merge

**Agent Merge** automatiza el trabajo restante para integrar un pull request. Al habilitarlo, Copilot resuelve los bloqueos del PR —por ejemplo, corrige fallos de integración continua (CI), responde a comentarios de revisión y vuelve a basar los cambios cuando hace falta— y después habilita la combinación automática de GitHub si el repositorio lo permite.

Hasta ahora has seleccionado **Merge pull request**. Agent Merge puede encargarse de esa responsabilidad, pero primero revisa el trabajo y decide si está listo.

## Usa Agent Merge para gestionar el PR

Con el código listo, revisa los cambios, crea el PR y deja que Agent Merge gestione el resto.

1. Vuelve a Codespace.
2. Escribe `/agent` para abrir el cuadro de diálogo del agente.
3. Selecciona **Default** y pulsa <kbd>Enter</kbd>.
4. Crea un PR con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará la integración continua del PR y lo combinará cuando todo se haya superado.
7. Comprueba que Copilot indique algo parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no elude las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni la falta de permisos. Si se bloquea, lee el motivo e, cuando el repositorio lo permita, completa manualmente la combinación tras revisarla.

## Resumen y siguientes pasos

Has automatizado varias partes del desarrollo: la generación de código, las pruebas y la validación, y ahora el proceso del pull request. En esta lección:

- aprendiste qué es Agent Merge y cómo automatiza el ciclo de vida de un PR;
- inspeccionaste los cambios de la funcionalidad y las evidencias de verificación;
- creaste el PR de filtrado;
- habilitaste Agent Merge tras revisar el trabajo y confirmaste que el PR se combinó.

A continuación, [explorarás comandos slash de Copilot CLI][next-lesson] para gestionar contexto, modelos, sesiones compartidas y delegación opcional a un agente en la nube.

## Recursos

- [Administrar pull requests con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
