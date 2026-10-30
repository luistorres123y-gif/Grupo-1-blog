# Development Workflow & Git Conventions

Guía de estándares para mantener un flujo de trabajo consistente,
facilitar la colaboración y asegurar la trazabilidad entre tickets,
ramas, commits y Pull Requests.

## 1. Objetivo

Este documento define las convenciones que debe seguir el equipo al
trabajar con Git y desarrollar nuevas funcionalidades, corregir errores
o mantener el proyecto.

La regla principal es que cada cambio tenga un propósito identificable,
un ticket asociado, una rama dedicada, commits descriptivos y un Pull
Request revisable antes de integrarse.

## 2. Convenciones generales

  -------------------------------------------------------------------------------------
  Elemento                Convención                            Idioma
  ----------------------- ------------------------------------- -----------------------
  Tickets                 `TYPE-123: Short description`         Inglés recomendado

  Ramas Git               `prefix/TYPE-123-short-description`   Inglés

  Commits                 Conventional Commits                  Inglés

  Pull Requests           `[TYPE-123] Short description`        Inglés

  Clases                  `PascalCase`                          Inglés

  Métodos y variables     `camelCase`                           Inglés

  Constantes              `UPPER_SNAKE_CASE`                    Inglés

  Archivos y carpetas     Según el lenguaje y framework         Inglés recomendado
  -------------------------------------------------------------------------------------

## 3. Nomenclatura de ramas

### Formato

``` text
prefix/TICKET-ID-short-description
```

Ejemplo:

``` text
feature/PROJ-123-user-authentication
```

### Prefijos permitidos

  -----------------------------------------------------------------------------------------
  Prefijo                 Uso                     Ejemplo
  ----------------------- ----------------------- -----------------------------------------
  `feature/`              Nueva funcionalidad     `feature/PROJ-123-user-profile`

  `bugfix/`               Corrección de errores   `bugfix/PROJ-124-invalid-email`
                          no urgente              

  `hotfix/`               Corrección crítica en   `hotfix/PROJ-125-payment-failure`
                          producción              

  `refactor/`             Reestructuración        `refactor/PROJ-126-auth-service`
                          interna sin cambio      
                          funcional esperado      

  `test/`                 Incorporar o corregir   `test/PROJ-127-user-service-tests`
                          pruebas                 

  `docs/`                 Documentación           `docs/PROJ-128-api-documentation`

  `chore/`                Mantenimiento,          `chore/PROJ-129-update-dependencies`
                          dependencias o          
                          configuración           

  `perf/`                 Mejoras de rendimiento  `perf/PROJ-130-optimize-query`

  `build/`                Compilación o           `build/PROJ-131-update-build-config`
                          empaquetado             

  `ci/`                   Pipelines y             `ci/PROJ-132-github-actions`
                          automatizaciones CI/CD  

  `revert/`               Revertir cambios        `revert/PROJ-133-remove-payment-change`
                          integrados              
  -----------------------------------------------------------------------------------------

### Reglas

1.  Utilizar un prefijo válido de la tabla.
2.  Incluir el identificador del ticket.
3.  Escribir la descripción en inglés.
4.  Utilizar `kebab-case`: minúsculas y palabras separadas por guiones.
5.  No utilizar espacios, acentos ni caracteres especiales.
6.  Mantener cada rama vinculada a un único ticket de trabajo.
7.  Crear la rama desde la rama base correspondiente al flujo del
    proyecto.

**Correcto:**

``` text
feature/PROJ-245-password-reset
```

**Incorrecto:**

``` text
newFeaturePassword
PROJ-245
feature/password reset
fix/245
```

Para correcciones convencionales se utiliza `bugfix/`; `hotfix/` queda
reservado para problemas críticos en producción.

### Rama base

-   `main`: código estable o listo para producción.
-   `develop`: integración de funcionalidades, si el proyecto utiliza
    esta rama.
-   `feature/*`, `bugfix/*`, etc.: ramas temporales de trabajo.

Si el equipo utiliza GitHub Flow, puede trabajar directamente desde
`main` sin mantener una rama `develop`. Los hotfixes deben partir de la
rama que represente la versión afectada en producción.

## 4. Tickets

Cada ticket debe representar un objetivo claro, verificable y
suficientemente acotado para poder desarrollarse y revisarse.

### Plantilla de ticket

``` markdown
# [TYPE-123] Short and descriptive title

## Type
Feature / Bug / Refactor / Task / Documentation / Technical Debt

## Summary
Briefly describe what needs to be implemented or corrected and why.

## Context
Explain the business or technical context behind the request.

## User Story
As a [user or role],
I want [functionality],
so that [expected benefit].

## Scope
- Describe what is included.
- Describe the expected behavior.
- Identify relevant modules or services.

## Acceptance Criteria
- Given [initial context], when [action], then [expected result].
- Given [initial context], when [action], then [expected result].
- Relevant error scenarios are handled.
- Automated tests are added or updated where applicable.

## Technical Notes
- Relevant architecture or implementation details.
- Dependencies, API contracts, or database changes.
- Security, performance, and compatibility considerations.

## Out of Scope
- Explicitly list what this ticket will not cover.

## Dependencies
- Related tickets, services, or external requirements.

## Definition of Done
- [ ] Implementation completed.
- [ ] Automated tests pass.
- [ ] Code follows project conventions.
- [ ] Pull Request approved.
- [ ] CI checks pass.
- [ ] Documentation updated when necessary.
```

### Reglas para tickets

-   Un ticket debe tener un único objetivo; no mezclar funcionalidades
    independientes.
-   El título debe describir el resultado esperado.
-   Los criterios de aceptación deben poder comprobarse.
-   Todo ticket debe tener un identificador único, por ejemplo
    `PROJ-123`.
-   Especificar qué queda fuera del alcance.
-   Indicar el tipo de trabajo y la prioridad según las convenciones del
    gestor utilizado.

Ejemplos:

-   `[PROJ-123] Implement password reset flow`
-   `[PROJ-124] Fix invalid email validation`
-   `[PROJ-125] Refactor authentication service`

## 5. Relación entre tickets y ramas

La convención general es **un ticket de desarrollo por rama principal de
trabajo**.

Ejemplo de trazabilidad:

``` text
Ticket:
PROJ-123 — Implement password reset

Branch:
feature/PROJ-123-password-reset

Commits:
Uno o varios commits relacionados con el ticket

Pull Request:
[PROJ-123] Implement password reset

Merge:
Integración en la rama base correspondiente
```

Reglas:

-   Cada ticket de implementación tiene una rama dedicada.
-   La rama no debe contener cambios ajenos al ticket.
-   Una rama puede contener varios commits.
-   El flujo estándar contempla un Pull Request por ticket.
-   No crear varias ramas paralelas para el mismo objetivo, salvo que
    exista una justificación técnica.

### Excepciones

Se permiten excepciones cuando:

-   Una tarea se divide en subtareas con entregables independientes.
-   Una funcionalidad requiere cambios coordinados en varios
    repositorios.
-   Un ticket padre agrupa varias tareas técnicas.
-   Se necesita una rama temporal de integración.

Cuando sea posible, crear tickets específicos por entregable y
relacionarlos con el ticket padre. Cada ticket de implementación
mantiene su propia rama.

## 6. Conventional Commits

Todos los mensajes de commit deben escribirse en inglés y seguir este
formato:

``` text
type(scope): imperative description
```

Ejemplo:

``` text
feat(auth): add password reset endpoint
```

### Tipos de commit

  ---------------------------------------------------------------------------------------------
  Tipo                    Uso                     Ejemplo
  ----------------------- ----------------------- ---------------------------------------------
  `feat`                  Nueva funcionalidad     `feat(users): add profile endpoint`

  `fix`                   Corrección de errores   `fix(auth): handle expired tokens`

  `refactor`              Reestructuración sin    `refactor(users): extract validation logic`
                          cambio funcional        
                          intencional             

  `test`                  Pruebas                 `test(auth): add login unit tests`

  `docs`                  Documentación           `docs(api): document error responses`

  `style`                 Formato sin cambios     `style(users): format service methods`
                          funcionales             

  `perf`                  Optimización de         `perf(db): reduce query count`
                          rendimiento             

  `build`                 Compilación y           `build(deps): update framework version`
                          dependencias            

  `ci`                    Integración continua    `ci(pipeline): add test coverage check`

  `chore`                 Mantenimiento general   `chore(config): remove unused settings`

  `revert`                Revertir cambios        `revert: revert user profile endpoint`
  ---------------------------------------------------------------------------------------------

### Buenas prácticas

1.  Escribir los mensajes en inglés.
2.  Utilizar el imperativo: `add`, `fix`, `remove`, `update`,
    `implement`.
3.  Describir el cambio realizado, no el tiempo invertido.
4.  Mantener cada commit enfocado en un cambio lógico.
5.  Evitar mensajes genéricos como `changes`, `fix`, `update code` o
    `final version`.
6.  Incluir el identificador del ticket en el cuerpo cuando sea útil
    para la trazabilidad.

Ejemplo con cuerpo:

``` text
feat(auth): add password reset endpoint

- Add password reset request handler
- Validate reset token expiration
- Add unit tests for invalid tokens

Refs: PROJ-123
```

El prefijo `feature/` identifica el tipo de rama; `feat` clasifica el
cambio registrado en el commit. No son intercambiables.

## 7. Pull Requests

### Formato del título

``` text
[TICKET-ID] Short description
```

Ejemplos:

``` text
[PROJ-123] Implement password reset
[PROJ-124] Fix invalid email validation
[PROJ-125] Refactor authentication service
```

El equipo puede optar por títulos con Conventional Commits, por ejemplo
`feat(auth): implement password reset`, pero debe elegir un formato y
mantenerlo consistentemente.

### Plantilla de Pull Request

``` markdown
# [PROJ-123] Implement password reset

## Summary
Briefly describe the changes introduced by this Pull Request.

## Related Ticket
- PROJ-123

## Changes Made
- Describe the main implementation changes.
- List relevant modules, services, or components modified.
- Mention API, database, or configuration changes.

## Motivation
Explain why these changes are needed and what problem they solve.

## Testing
- [ ] Unit tests added or updated.
- [ ] Integration tests added or updated where applicable.
- [ ] Manual testing completed where necessary.
- [ ] All relevant tests pass locally.

## Screenshots / API Examples
Include screenshots, request/response examples, or other evidence when relevant.

## Breaking Changes
- [ ] No breaking changes.
- [ ] Breaking changes are documented below.

Details:
Describe any incompatible changes and required migration steps.

## Checklist
- [ ] The PR is linked to the corresponding ticket.
- [ ] The implementation follows project conventions.
- [ ] No unrelated changes are included.
- [ ] Tests and CI checks pass.
- [ ] Documentation is updated when necessary.
- [ ] The PR is ready for review.

## Reviewer Notes
Highlight areas that require special attention from reviewers.
```

### Reglas para Pull Requests

-   Un PR debe resolver el objetivo de un ticket.
-   El título debe incluir el identificador del ticket.
-   Explicar qué cambió, por qué cambió y cómo se probó.
-   No mezclar refactorizaciones no relacionadas con funcionalidades
    nuevas.
-   Cumplir las aprobaciones y validaciones automáticas requeridas por
    el repositorio.
-   Eliminar la rama después del merge si el flujo del equipo lo
    permite.
-   Marcar como Draft los PR que todavía no estén listos para revisión.

Se prefieren PR pequeños y enfocados. Si un ticket genera un PR
demasiado grande, evaluar dividirlo en subtareas con entregables claros.

## 8. Convenciones de código

### Nomenclatura

  Elemento          Convención           Ejemplo
  ----------------- -------------------- -------------------------
  Clase             `PascalCase`         `UserService`
  Interfaz          `PascalCase`         `PaymentGateway`
  Clase abstracta   `PascalCase`         `BaseRepository`
  Excepción         `PascalCase`         `InvalidTokenException`
  DTO               `PascalCase`         `CreateUserRequestDto`
  Entidad           `PascalCase`         `UserAccount`
  Enumeración       `PascalCase`         `OrderStatus`
  Método            `camelCase`          `findUserById()`
  Variable          `camelCase`          `userAccount`
  Parámetro         `camelCase`          `accessToken`
  Constante         `UPPER_SNAKE_CASE`   `MAX_LOGIN_ATTEMPTS`

### Ejemplo

``` typescript
export class UserService {
  private readonly MAX_LOGIN_ATTEMPTS = 5;

  public findUserById(userId: string): UserAccount | null {
    // Implementation
    return null;
  }

  public resetPassword(userId: string): void {
    // Implementation
  }
}
```

La forma de declarar constantes y modificadores debe adaptarse al
lenguaje y framework. En TypeScript, por ejemplo, una constante de clase
`static readonly` suele escribirse en `UPPER_SNAKE_CASE` si esa es la
convención elegida.

### Reglas adicionales

-   Los nombres de las clases deben describir su responsabilidad.
-   Evitar nombres genéricos como `Manager`, `Helper` o `Utils` cuando
    exista una alternativa más descriptiva.
-   Los nombres de clases, métodos, variables y archivos deben utilizar
    inglés.
-   No agregar prefijos artificiales como `CUserService` o
    `IUserService`, salvo que el lenguaje o la arquitectura lo
    establezcan.
-   Respetar las convenciones del framework: por ejemplo, clases e
    interfaces en `PascalCase` y archivos en `kebab-case` cuando
    corresponda.

Ejemplos:

-   `AuthenticationService`
-   `PaymentProcessor`
-   `UserRepository`
-   `CreateOrderRequest`
-   `OrderStatus`
-   `InvalidCredentialsException`

## 9. Idioma del proyecto

El inglés será el idioma técnico estándar para los elementos que forman
parte del código y del historial de desarrollo.

  Elemento                      Idioma recomendado
  ----------------------------- ----------------------------------------
  Tickets                       Inglés
  Nombres de ramas              Inglés
  Commits                       Inglés
  Pull Requests                 Inglés
  Clases, métodos y variables   Inglés
  Comentarios de código         Inglés
  Documentación técnica         Inglés
  Comunicación interna          Según el idioma acordado por el equipo

Esto no impide que la comunicación interna sea en español. El objetivo
es mantener consistentes los artefactos técnicos.

## 10. Flujo de trabajo

1.  **Create the ticket:** definir el alcance, los criterios de
    aceptación y el identificador único.
2.  **Create the branch:** crear una rama exclusiva para el ticket.
3.  **Implement and commit:** desarrollar, probar y registrar cambios
    lógicos con mensajes en inglés.
4.  **Open the Pull Request:** vincular el ticket, explicar los cambios
    y solicitar revisión.
5.  **Review and merge:** completar las aprobaciones y validaciones
    automáticas antes de integrar.
6.  **Close the ticket:** verificar que el cambio integrado cumple los
    criterios de aceptación y actualizar el estado del ticket.

## 11. Resumen rápido

  -----------------------------------------------------------------------------------------------------
  Elemento                Formato                                 Ejemplo
  ----------------------- --------------------------------------- -------------------------------------
  Branch                  `prefix/TICKET-ID-short-description`    `feature/PROJ-123-user-profile`

  Ticket                  `TYPE-ID: Short description`            `PROJ-123: Implement user profile`

  Commit                  `type(scope): imperative description`   `feat(users): add profile endpoint`

  Pull Request            `[TICKET-ID] Short description`         `[PROJ-123] Implement user profile`

  Clase                   `PascalCase`                            `UserProfileService`

  Método / variable       `camelCase`                             `findUserById`

  Constante               `UPPER_SNAKE_CASE`                      `MAX_LOGIN_ATTEMPTS`

  Relación ticket-rama    Un ticket por rama                      `feature/PROJ-123-user-profile`
  -----------------------------------------------------------------------------------------------------

## 12. Aplicación en el repositorio

Para que estas reglas se apliquen de manera consistente, se recomienda:

-   Incorporar este documento al repositorio como `README.md` o
    mantenerlo en `CONTRIBUTING.md` / `docs/development-workflow.md`.
-   Crear plantillas de tickets y Pull Requests.
-   Configurar validaciones automáticas para nombres de ramas y commits
    cuando las herramientas lo permitan.
-   Establecer reglas de protección de ramas, aprobaciones y CI.
-   Mantener enlaces entre tickets, ramas y Pull Requests.

------------------------------------------------------------------------

**Regla fundamental:** cada cambio debe tener un propósito
identificable, un ticket asociado, una rama dedicada, commits
descriptivos en inglés y un Pull Request revisable antes de integrarse.
