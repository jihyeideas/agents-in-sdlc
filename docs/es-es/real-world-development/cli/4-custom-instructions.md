---
title: "Lección 4: Guía a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es fundamental cuando se trabaja con IA generativa. Si una tarea debe realizarse de una manera concreta, conviene proporcionar esa orientación a Copilot. Los [archivos de instrucciones][instruction-files] describen no solo *qué* código quieres, sino también *cómo* debe estructurarse. Ahora que has creado el filtrado, explorarás las instrucciones que usó Copilot, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección:

- explorarás cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas para rutas;
- actualizarás el archivo de instrucciones para exigir el cumplimiento de los estándares de código;
- observarás el efecto de los archivos de instrucciones en el código.

## Escenario

Tailspin Toys tiene directrices para sus prácticas de desarrollo. Entre ellas:

- Los comentarios deben explicar la intención y las decisiones no evidentes, no repetir el código.
- Las funciones exportadas de `db/` y `src/lib/` deben documentar su propósito, parámetros y valores devueltos con TSDoc/JSDoc; también deben documentar el argumento `db` inyectable, si existe.
- Los componentes Astro reutilizables deben documentar sus contratos `Props`, y los comentarios deben mantenerse actualizados cuando cambie el código relacionado.
- Se deben conservar las directrices de formato y lint existentes.

Con los archivos de instrucciones, te asegurarás de que Copilot disponga del contexto correcto para seguir estas prácticas.

## Archivos de instrucciones

Las instrucciones personalizadas proporcionan contexto y preferencias para que Copilot comprenda mejor tus requisitos y tu estilo de desarrollo. Puedes indicar convenciones de código, bibliotecas y los comentarios que quieres incluir. Puedes crear instrucciones para todo el repositorio o para tipos de archivos concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un archivo único que se envía a Copilot en **todas** las solicitudes del repositorio y debe contener orientación general sobre el proyecto.
- `.github/instructions/*.instructions.md`, archivos que proporcionan directrices para lenguajes, tipos de archivo o tareas concretos.

> [!NOTE]
> Otros formatos de instrucciones pueden variar según el entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support] antes de depender de un formato concreto.

## Explora los archivos de instrucciones personalizadas del proyecto

El proyecto inicial incluye varios archivos de instrucciones. Explóralos antes de modificarlos para entender su efecto.

1. Vuelve a Codespace.
2. En el editor de Codespaces (no en el terminal), abre `.github/copilot-instructions.md`.
3. Lee la breve descripción del proyecto y las directrices de código. Estas instrucciones se aplican a todas las interacciones con Copilot en este repositorio.
4. Explora los archivos de la carpeta `.github/instructions`, incluidos los de Astro, Drizzle y pruebas.
5. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`: el glob determina a qué archivos se aplican las instrucciones.
6. Abre `.github/instructions/drizzle.instructions.md` y revisa sus vínculos a otros archivos de instrucciones y a archivos existentes del proyecto.

> [!NOTE]
> Las instrucciones de este proyecto incluyen estándares de desarrollo, pero todavía no exigen comentarios TSDoc para TypeScript. En los pasos siguientes añadirás ese requisito.

## Explora los archivos de instrucciones personalizadas del proyecto

El proyecto inicial ya incluye un archivo `copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas. Explóralos antes de hacer cambios.

1. Vuelve a Codespace.
2. En el editor de Codespaces (no en el terminal), abre `.github/copilot-instructions.md`.
3. Lee la breve descripción del proyecto y las directrices. Se aplican a todas las interacciones con Copilot en este repositorio.
4. Explora los archivos de `.github/instructions`, que incluyen instrucciones para Astro, la capa de datos de Drizzle, las pruebas y otros temas.
5. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`: el glob determina a qué archivos se aplican las instrucciones. En este caso, coincide con archivos de prueba TypeScript, por ejemplo, los que cumplen `**/*.test.ts`.
6. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos del proyecto. Así puedes dividir instrucciones extensas en archivos reutilizables y mostrar ejemplos a Copilot.

> [!NOTE]
> En el IDE, los archivos de instrucciones se usan para generar código en Copilot Chat, no para las finalizaciones ni las sugerencias de siguiente edición. Copilot Chat, Copilot CLI y Copilot cloud agent usan tanto las instrucciones del repositorio como los archivos `*.instructions.md` que incluyan el frontmatter `applyTo`. Copilot también admite otros formatos, como AGENTS.md y CLAUDE.md.

## Actualiza las instrucciones para reflejar los estándares del equipo

Los archivos iniciales son un buen punto de partida, pero falta una regla. Actualiza `.github/copilot-instructions.md` para exigir comentarios TSDoc en el nuevo TypeScript.

1. Abre `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting guidance**, que debería estar cerca de la línea 35.
3. Añade este elemento al final de la sección:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

El archivo se guardará automáticamente.

## Aplica las instrucciones actualizadas

Copilot CLI carga las instrucciones del repositorio cuando comienza una conversación. Sal y reanuda la conversación de filtrado para que Copilot use las nuevas instrucciones sin perder el contexto de la funcionalidad.

1. Si la conversación de filtrado sigue abierta, escribe `/exit`. Copilot CLI guarda las conversaciones automáticamente.
2. Desde la raíz del repositorio y en la rama `game-filters-cli`, reanuda la conversación guardada:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado y confirma que está seleccionada la rama `game-filters-cli`.
3. Pide a Copilot que aplique las instrucciones actualizadas:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Escribe `/diff` y revisa los archivos TypeScript modificados. Comprueba que los comentarios TSDoc nuevos describen el código correctamente.

## Resumen y siguientes pasos

Has explorado cómo Copilot usa las instrucciones del repositorio y has aplicado un estándar nuevo. En esta lección:

- exploraste cómo llegan al agente las instrucciones del repositorio y las específicas para rutas;
- actualizaste las instrucciones para exigir los estándares de código;
- observaste su efecto en el código.

A continuación, personalizarás y ejecutarás la habilidad reutilizable `quality-checks` para ejecutar lint y pruebas de forma coherente.

## Recursos

- [Añadir instrucciones personalizadas para Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: colección de instrucciones y otros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
