# HU-2: Validación facial de identidad

**Estado:** Borrador para revisión; sujeto a definición de KYC y aprobación de Cumplimiento antes de elaborar la spec.

## Fuente y trazabilidad

- **Feature:** [Registro y activación del MVP de wallet](../epics/FEATURES-1.md).
- **Épica:** MVP de wallet en Perú.
- **Parte relacionada:** pasos requeridos del onboarding y requisitos KYC, aún pendientes de definición con Producto y Cumplimiento.

## Historia de usuario

Como persona que realiza el onboarding de la wallet, quiero completar la validación facial requerida, para acreditar mi identidad y continuar con el alta.

## Contexto y resultado esperado

La feature fuente condiciona la implementación de KYC y documentación a una definición previa de Producto y Cumplimiento. Esta HU no presupone método biométrico, proveedor, umbral de coincidencia ni documento de comparación.

## Alcance

### Incluye

- Presentar el paso de validación facial según la política KYC aprobada.
- Permitir continuar únicamente cuando el resultado cumpla los criterios aprobados.
- Comunicar un resultado fallido, indeterminado o técnicamente no disponible con el siguiente paso autorizado.

### No incluye

- Definir por sí sola requisitos legales, consentimiento, prueba de vida, documento de comparación, proveedor, retención o umbral de aceptación.
- Activar la wallet por completar únicamente este paso.

## Criterios de aceptación

1. **Requisitos previos:** Dado que Producto y Cumplimiento aprobaron los requisitos KYC, cuando la persona llega al paso facial, entonces se le presentan las instrucciones y avisos requeridos por esa política.
2. **Resultado aprobado:** Dado que la validación devuelve un resultado que satisface los criterios aprobados, cuando el sistema procesa ese resultado, entonces marca el paso como completado y permite continuar el onboarding.
3. **Resultado no aprobado:** Dado que el resultado es fallido o indeterminado, cuando se procesa, entonces el paso no se marca como completado y se muestra la acción siguiente aprobada, como reintento o revisión alternativa.
4. **Falla técnica:** Dado que el servicio de validación no está disponible o no entrega un resultado confiable, entonces el sistema no considera la identidad validada y comunica cómo continuar según la política aprobada.
5. **Analítica y privacidad:** Cuando se inicia o completa el paso, se registran únicamente los eventos y atributos aprobados; imágenes faciales, plantillas biométricas y datos sensibles no se incluyen en analítica salvo aprobación explícita de Cumplimiento y Seguridad.

## Comportamiento y contratos a preservar

- No se debe avanzar a la activación de la wallet si la validación facial es un paso obligatorio y no ha sido aprobada.
- El estado reportado por este paso debe distinguir, como mínimo, éxito de resultado no aprobado o no disponible; los estados finales se definirán en la spec.
- Los eventos deben respetar las reglas aprobadas de minimización y tratamiento de datos.

## Dependencias y riesgos

- Bloqueada para diseño detallado e implementación hasta recibir los requisitos KYC de Producto y Cumplimiento.
- El tratamiento de datos biométricos puede implicar obligaciones de privacidad y retención que deben determinarse antes de especificar el flujo.
- No definir reintentos, umbrales o revisión manual sin decisión aprobada.

## Preguntas abiertas para la spec

- ¿Qué significa exactamente “validación facial”: prueba de vida, comparación con documento, ambas u otro método?
- ¿Qué consentimiento, avisos, datos y períodos de retención exige la política aprobada?
- ¿Cuáles son los resultados posibles, umbrales, número de intentos y alternativa ante rechazo?
- ¿Qué servicio o responsable aporta el resultado y cómo se manejarán indisponibilidad y revisión manual?
- ¿Qué eventos pueden registrarse sin exponer datos biométricos?

## Validación y evidencia para la spec

- Requisitos KYC documentados y aprobación de Producto y Cumplimiento.
- Revisión de privacidad y seguridad sobre captura, transmisión, almacenamiento, retención y eliminación.
- Matriz aprobada de resultados y casos de prueba para éxito, rechazo, indeterminado e indisponibilidad.