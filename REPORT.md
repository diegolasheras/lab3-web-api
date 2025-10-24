# Lab 3 Complete a Web API -- Project Report

## Description of Changes
Se implementó la lógica de *setup* y *verify* en `ControllerTests.kt` para demostrar la **Seguridad** e **Idempotencia** de los métodos HTTP:

| Método | Propiedades | Resumen de Implementación |
| :--- | :--- | :--- |
| **POST** | **No Seguro/No Idempotente** | Mockea `save()` para devolver IDs secuenciales (`1` y `2`). Verifica que `save()` se llama **dos veces**. |
| **GET** | **Seguro/Idempotente** | Mockea `findById()` para devolver `Employee` o `Optional.empty()`. Verifica que `save()` y `deleteById()` se llaman **cero veces**. |
| **PUT** | **No Seguro/Idempotente** | Mockea `findById()` para simular Creación (`empty`) seguida de Actualización (`Employee`). Verifica que `findById()` y `save()` se llaman **dos veces**. |
| **DELETE** | **No Seguro/Idempotente** | Usa **`justRun`** en `deleteById()`. Verifica que `deleteById()` se llama **dos veces** (reflejando la lógica del controlador) y que no hay efectos secundarios (`save`/`findById`). |


## Technical Decisions
1.  **MockK Secuencial:** Se usó **`answers { ... } andThenAnswer { ... }`** en `POST` y `PUT` para simular secuencias de llamadas y probar la **no-idempotencia** (POST) y el **cambio de estado** (PUT).
2.  **Manejo de Métodos Void:** Se empleó **`justRun`** para mockear `deleteById()`, que no devuelve valor, simulando una ejecución exitosa sin efectos secundarios.

## Learning Outcomes
Se reforzó la comprensión sobre la diferencia entre **Seguridad** (no modificar estado, verificado con `verify(exactly = 0)`) e **Idempotencia** (resultado final consistente tras múltiples llamadas, verificado con secuencias de MockK).

## AI Disclosure
### AI Tools Used
- [List specific AI tools used]

### AI-Assisted Work
- **Reporte y Nomenclatura:** La IA asistió en la redacción y estructuración final del presente **`REPORT.md`** y en la revisión de la **nomenclatura de los *commits*** (e.g., `feat(METHOD): description`) para garantizar que cumpliera con los requisitos de la práctica.

- **Porcentaje de Trabajo Asistido:** Aproximadamente **10%**.


### Original Work
- El **100% del código de prueba** en `ControllerTests.kt` fue escrito y desarrollado por mí.
- El conocimiento fundamental sobre qué métodos mockear y qué `verify` aplicar para cada propiedad HTTP fue desarrollado y ejecutado por mí, tras sintetizar la información leída en la Sección 5.2 del PDF.