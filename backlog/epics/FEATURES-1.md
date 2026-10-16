# Feature: Registro y activación del MVP de wallet

## Resumen

Como usuario de smartphone que realiza transferencias diarias de bajo monto, quiero completar el onboarding de la wallet mediante un flujo guiado, con indicaciones claras del siguiente paso, para poder comenzar a pagar sin abandonar el proceso.

**Épica:** MVP de wallet en Perú.

La feature busca reducir la mediana del tiempo de finalización del onboarding de 8 a 3 minutos durante el trimestre posterior al lanzamiento, y habilitar el seguimiento de activación, MAU y CAC durante los primeros tres meses.

## Alcance

### Dentro del alcance

- Mostrar los pasos requeridos del onboarding y el paso actual.
- Validar la información requerida y orientar al usuario para corregir datos faltantes o inválidos.
- Activar la wallet al completar correctamente el onboarding y habilitar el punto de entrada a pagos de bajo monto.
- Registrar eventos de inicio, finalización de cada paso y cierre del flujo para analítica del MVP.
- Producir datos de onboarding y adquisición que permitan evaluar los objetivos de MAU y CAC, una vez acordadas sus definiciones.

### Fuera del alcance o pendiente de delimitación

- Los requisitos concretos de KYC y la documentación requerida; deben definirse con Producto y Cumplimiento antes de implementar.
- La ejecución de transferencias y el diseño de los rieles de pago, que no están especificados en esta feature.

## Supuestos

- La cohorte objetivo del MVP corresponde a Perú.
- La línea base de tiempo mediano de onboarding es de 8 minutos.
- El Product Owner definió como objetivos un MAU entre 1,000 y 2,000 y un CAC de PEN 10 por usuario nuevo para los primeros tres meses.
- Los criterios de KYC y documentación se acordarán con Producto y Cumplimiento antes de implementar.

## Decisiones técnicas por tomar

- Definir los eventos, sus atributos y el mecanismo de atribución de gasto; no se prescribe una solución técnica en esta feature.
- Acordar cómo se calcularán los usuarios únicos activos y el gasto de adquisición antes de construir la salida analítica.
- Confirmar los límites de datos personales que pueden incluirse en los eventos y reportes.

## Criterios de aceptación

1. **Pasos visibles:** Dado que el usuario está realizando el onboarding, cuando avanza por el flujo, entonces puede identificar la secuencia requerida y el paso actual.
2. **Validación accionable:** Dado que falta información obligatoria o hay datos inválidos, cuando el usuario intenta avanzar, entonces el flujo bloquea el avance e indica cómo corregirlo.
3. **Activación:** Dado que el usuario completó correctamente todos los pasos, cuando finaliza el onboarding, entonces el estado de la wallet cambia a activo y queda disponible el punto de entrada a pagos de bajo monto.
4. **Eventos del flujo:** Cuando el usuario inicia el onboarding, completa cada paso y cierra el flujo, entonces se registran los eventos correspondientes para la analítica del MVP.
5. **Tiempo de finalización:** Para la cohorte MVP en Perú, durante el trimestre posterior al lanzamiento, la mediana del tiempo de finalización del onboarding es de 3 minutos o menos, tomando como referencia la línea base de 8 minutos.
6. **Seguimiento de adquisición y activación:** Durante los primeros tres meses, la salida analítica presenta conteos mensuales de usuarios activos y gasto de adquisición atribuible, con los que se pueden evaluar el objetivo de MAU de 1,000 a 2,000 y CAC de PEN 10 por usuario nuevo.

## Riesgos y mitigaciones

| Riesgo | Mitigación |
| --- | --- |
| La definición de usuario activo, el período del objetivo de MAU y el conteo de usuarios nuevos no están precisados; los resultados podrían interpretarse de distintas maneras. | Producto debe aprobar definiciones, período de medición y reglas de deduplicación antes de implementar la analítica. |
| No está definida la fórmula ni la fuente de atribución del CAC; el resultado podría no ser reproducible. | Producto debe acordar qué gasto se incluye, cómo se atribuye y cuál es el denominador antes de aceptar el reporte. |
| Los requisitos de KYC y documentación aún dependen de Producto y Cumplimiento. | Obtener su definición y aprobación antes de implementar los pasos correspondientes del onboarding. |

## Plan de validación

- **Pruebas unitarias:** comprobar las reglas de validación de pasos y la transición de la wallet a estado activo.
- **Pruebas funcionales:** recorrer el onboarding completo, verificar el bloqueo ante datos faltantes o inválidos y confirmar el acceso al punto de entrada a pagos tras la activación.
- **Analítica:** comprobar la emisión de eventos de inicio, finalización de cada paso y cierre; validar los conteos mensuales y la atribución contra definiciones aprobadas.
- **Seguridad y cumplimiento:** revisar con los responsables que la captura de datos y documentos respete los requisitos de KYC aprobados y que los eventos no incluyan datos personales no autorizados.
- **Evidencia requerida:** resultados de pruebas, definiciones aprobadas de MAU/CAC y evidencia de revisión de Producto y Cumplimiento para KYC.

## Tareas sugeridas por rol

- **Producto:** confirmar la definición de usuario activo y usuario nuevo; aprobar el período y rango de MAU; acordar la fórmula de CAC y coordinar los requisitos KYC con Cumplimiento.
- **Tech Lead:** revisar el impacto en los componentes y contratos existentes; definir, tras aprobación de producto, el contrato de eventos; revisar riesgos de datos y la estrategia de validación.
- **Backend:** implementar, una vez aprobados los detalles, las transiciones de estado del onboarding; registrar los eventos acordados; producir los datos necesarios para el reporte mensual.
- **Frontend:** presentar la secuencia y el paso actual; mostrar validaciones y mensajes accionables; habilitar el punto de entrada a pagos tras la activación.
- **QA:** probar caminos válidos e inválidos; verificar las transiciones y eventos; validar los resultados analíticos con datos de prueba y las definiciones aprobadas.
- **Cumplimiento/Seguridad:** definir y revisar los requisitos de KYC y documentación; revisar el tratamiento de datos personales en el flujo; confirmar controles aplicables antes de implementar.

## Preguntas abiertas

- ¿“MAU entre 1,000 y 2,000” es el total de usuarios activos o solo los nuevos usuarios activos? ¿Debe cumplirse cada mes o al cierre del tercer mes?
- ¿Qué acción define a un usuario como activo, y qué período, zona horaria y regla de deduplicación se usarán?
- ¿Qué costos, canales, período de atribución y denominador forman parte del cálculo de CAC de PEN 10?
- ¿Cuál es la fuente y el método para medir la línea base de 8 minutos y la mediana posterior al lanzamiento?
- ¿Qué documentos y verificaciones de KYC aplican a esta cohorte, y quién de Producto y Cumplimiento los aprobará?
- ¿Qué formato, audiencia y frecuencia debe tener la salida analítica?