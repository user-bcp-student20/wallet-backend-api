# HU-4: Mostrar un mensaje de bienvenida al usuario

**Estado:** Borrador para revisión; no aprobado para implementación.

## Fuente y trazabilidad

- **Feature:** [Registro y activación del MVP de wallet](../epics/FEATURES-1.md).
- **Épica:** MVP de wallet en Perú.
- **Parte relacionada:** onboarding guiado con señales claras del siguiente paso y acceso al punto de entrada a pagos tras la activación.

## Historia de usuario

Como usuario que completó el onboarding de la wallet, quiero ver un mensaje de bienvenida claro, para confirmar que el alta terminó y saber cuál es el siguiente paso.

## Contexto y resultado esperado

El mensaje debe confirmar el resultado del onboarding. La feature fuente dispone el acceso al punto de entrada de pagos de bajo monto al completar el flujo; esta HU no implica ejecutar un pago.

## Alcance

### Incluye

- Mostrar una confirmación de bienvenida al usuario cuando el onboarding haya finalizado correctamente.
- Comunicar el siguiente paso disponible y presentar el punto de entrada a pagos si la wallet está activa.
- Mantener el mensaje coherente con el estado real del onboarding y de la wallet.

### No incluye

- Definir el canal, diseño visual, texto comercial ni estrategia de notificaciones fuera del flujo.
- Permitir pagos si la wallet no está activa.

## Criterios de aceptación

1. **Bienvenida tras completar:** Dado que el onboarding finalizó correctamente y la wallet está activa, cuando el usuario llega a la confirmación, entonces ve un mensaje que confirma el alta.
2. **Siguiente paso:** Dado que la wallet está activa, entonces la confirmación presenta el punto de entrada disponible a pagos de bajo monto, sin afirmar que un pago ya fue realizado.
3. **Onboarding incompleto:** Dado que el onboarding no se completó o la wallet no está activa, entonces no se muestra una confirmación que indique que el alta terminó; se comunica el siguiente paso pendiente.
4. **Datos de presentación:** Si el mensaje usa el nombre del usuario, entonces utiliza únicamente un dato disponible y aprobado; si no está disponible, la bienvenida sigue siendo comprensible sin ese dato.
5. **Analítica:** La visualización del mensaje se registra solo si forma parte de los eventos aprobados para el MVP y sin incluir datos personales no necesarios.

## Comportamiento y contratos a preservar

- La bienvenida no debe cambiar el estado de la wallet ni sustituir los pasos de autenticación, KYC o verificación.
- Solo se ofrece el acceso a pagos cuando la wallet está activa, de acuerdo con la feature fuente.
- El mensaje debe reflejar el estado confirmado por el flujo, no inferir éxito a partir de una pantalla visitada.

## Dependencias y riesgos

- Depende de una señal fiable de finalización del onboarding y activación de wallet.
- Mostrar bienvenida antes de completar verificaciones puede inducir al usuario a creer que su cuenta está habilitada.
- El uso de nombre u otros datos personales requiere confirmar su fuente y presentación aprobada.

## Preguntas abiertas para la spec

- ¿En qué pantalla o canal se mostrará la bienvenida y cuándo se considera que el usuario la vio?
- ¿Se personalizará con el nombre del usuario? ¿Qué fuente y formato se usarán?
- ¿Cuál es el texto aprobado y cuál es el siguiente paso que debe presentarse?
- ¿La bienvenida aparece cada vez que el usuario entra o solo al completar el onboarding?
- ¿Debe registrarse un evento de visualización? ¿Qué atributos están permitidos?

## Validación y evidencia para la spec

- Confirmación de Producto del texto, canal, momento de presentación y siguiente paso.
- Casos de prueba para wallet activa, onboarding incompleto y nombre no disponible.
- Evidencia de que el acceso a pagos solo aparece para una wallet activa.