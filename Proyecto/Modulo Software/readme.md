# Módulo software

## Estado actual

- Se han realizado pruebas preliminares de **transmisión y recepción LoRa** entre placas Heltec V4 a **915 MHz**.
- Se ha probado la **visualización en la pantalla OLED**. El código unificado con todos los sensores aún está en desarrollo.

## Flujo previsto

1. Encender los sensores una vez por hora.
2. Tomar cinco lecturas, comprobar valores inválidos y consolidar los datos.
3. Transmitir las mediciones por LoRa a la placa receptora.
4. Incorporar posteriormente almacenamiento, app y avisos por WhatsApp, una vez validados los pasos anteriores.

## Pendientes

- Confirmar la configuración definitiva de pines, bibliotecas y formato de mensajes.
- Integrar y probar simultáneamente sensores, OLED, LoRa y control de energía.
- Definir registro de fecha/hora, tratamiento de cortes de comunicación y manejo de errores.
- Desarrollar y validar backend, aplicación y notificaciones. AWS y Meta WhatsApp son integraciones **propuestas, no terminadas**.

**Aún no se publica aquí una versión definitiva del firmware ni de la aplicación.**
