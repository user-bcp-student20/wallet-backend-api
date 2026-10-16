# HU-3: Registrar y verificar el número de celular mediante OTP

**Estado:** Borrador para revisión; no aprobado para implementación.

## Fuente y trazabilidad

- **Feature:** [Registro y activación del MVP de wallet](../epics/FEATURES-1.md).
- **Épica:** MVP de wallet en Perú.
- **Parte relacionada:** validar datos obligatorios durante el onboarding y registrar la finalización de cada paso.

## Historia de usuario

Como persona que realiza el onboarding de la wallet, quiero registrar mi número de celular y verificarlo con un código OTP, para confirmar que puedo recibir mensajes en ese número y continuar con el alta.

## Contexto y resultado esperado

El número solo se considera verificado después de que la persona introduce un código válido asociado a ese número. La verificación del celular no equivale por sí sola a completar el KYC ni a activar la wallet.

## Alcance

### Incluye

- Solicitar y capturar el número de celular.
- Enviar un OTP por el canal aprobado y permitir su ingreso.
- Aceptar o rechazar el código e informar al usuario del resultado.

### No incluye

- Definir canal de envío, formato internacional, vigencia, límites de intentos, reenvíos o proveedor; requieren decisión previa.
- Considerar el teléfono como prueba suficiente de identidad o como sustituto de otros pasos KYC.

## Criterios de aceptación

1. **Solicitud de código:** Dado que la persona ingresó un número con formato aceptado y solicita verificarlo, cuando el servicio de envío está disponible, entonces se envía un OTP al destino indicado por el canal aprobado y se muestra cómo continuar.
2. **Código válido:** Dado que la persona ingresó el OTP vigente y asociado al número solicitado, cuando se valida correctamente, entonces el número queda verificado y el onboarding puede continuar.
3. **Código inválido o vencido:** Dado que el código es incorrecto, venció o no corresponde a la solicitud vigente, cuando se intenta validar, entonces el número no queda verificado y se muestra un mensaje accionable.
4. **Límites de seguridad:** Dado que se alcanzan los límites aprobados de intentos o solicitudes, entonces el sistema aplica la respuesta definida por Seguridad y no permite eludir esos límites mediante reenvíos.
5. **Cambio de número:** Dado que la persona cambia el número después de verificarlo, entonces el número nuevo no se considera verificado hasta completar una nueva validación.
6. **Analítica y privacidad:** Se registran los eventos aprobados de inicio y finalización del paso, sin incluir el OTP ni exponer el número completo en analítica.

## Comportamiento y contratos a preservar

- El estado verificado debe corresponder al mismo número para el que se emitió y validó el OTP.
- La verificación de teléfono no activa la wallet antes de completar todos los pasos requeridos.
- Los límites de solicitudes y validación deben seguir las reglas de seguridad acordadas, no valores inventados en esta HU.

## Dependencias y riesgos

- Depende de la selección del canal de entrega y de la definición de las reglas antifraude y de seguridad.
- Reenvíos o intentos ilimitados pueden facilitar abuso, enumeración o costos excesivos.
- El teléfono es dato personal; su exposición en mensajes, logs o eventos debe limitarse conforme a la política aprobada.

## Preguntas abiertas para la spec

- ¿Qué canales y países se soportan para enviar el OTP?
- ¿Qué formatos de teléfono se aceptan y cómo se normalizan?
- ¿Cuál es la vigencia del código, el máximo de intentos y la política de reenvío/bloqueo?
- ¿Puede un número estar asociado a más de una cuenta? ¿Cómo se resuelve un número ya registrado?
- ¿Qué mensajes se muestran ante demora, fallo de entrega o límite alcanzado?
- ¿Qué atributos de eventos se permiten y cómo se enmascara el número?

## Validación y evidencia para la spec

- Decisiones aprobadas por Producto y Seguridad sobre canal, formato, vigencia, reintentos y números existentes.
- Casos de prueba para código válido, inválido, vencido, cambio de número, límite alcanzado y fallo de entrega.
- Revisión de privacidad de los datos de teléfono en almacenamiento, mensajes y analítica.