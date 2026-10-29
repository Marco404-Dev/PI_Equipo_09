# Puntos pendientes para validar con el equipo

**Equipo 09 · Lista de revisión, no aprobación de requisitos**

Este seguimiento acompaña la [lista de exigencias del curso](../Proyecto%20Integrador/Entregables/Lista%20de%20exigencias.md), edición Rev. 2. **No modifica ni aprueba exigencias de otros integrantes.**

- [ ] **Sensores:** confirmar modelos comerciales exactos de pH, TDS, BME280 adaptador y flotador P45; obtener hojas técnicas.
- [ ] **Variable conductividad:** decidir si el módulo TDS puede sustentar la variable del modelo de OD tras calibración, o si se requiere una sonda de conductividad identificada.
- [ ] **Montaje V4:** seleccionar GPIO viables y documentar niveles lógicos/voltajes con la placa real [1].
- [ ] **Muestreo:** validar el ciclo de una sesión/hora y cinco lecturas/sesión mediante consumo y estabilidad del sensor.
- [ ] **LoRa:** acordar alcance de prueba y cómo calcular tasa de pérdida; registrar los parámetros de cada ensayo.
- [ ] **Energía:** verificar la autonomía de la batería y la compatibilidad de panel USB 5 W/UPS antes de incorporarlos.
- [ ] **Carcasa/estanqueidad:** evaluar si el diseño y los materiales disponibles cumplen las condiciones ambientales propuestas.
- [ ] **Metas exigentes:** revisar con fuentes y ensayos el viento de 80 km/h, protección IP68, precisión ±0,5 %, disponibilidad >98 % y pérdidas <2 %; **no declarar cumplimiento sin medir**.
- [ ] **Servicio de datos:** decidir equipo y mecanismo de registro de fecha/hora, almacenamiento y conexión del receptor a Internet.
- [ ] **Avisos e interfaz:** determinar cuándo se considera una alerta válida y el tratamiento de datos personales en WhatsApp; no está integrado.
- [ ] **Trabajo en campo:** asignar responsables y aprobaciones para seguridad, ubicación, muestreo y retiro de la boya.

**Estado:** lista para discusión del Equipo 09. Los cambios de exigencias o metas requieren acuerdo del grupo y de su asesor.

## Referencias (formato IEEE)

[1] Heltec Automation, “WiFi LoRa 32,” *Documentación del fabricante*. [En línea]. Disponible: https://docs.heltec.org/en/node/esp32/wifi_lora_32/index.html. [Accedido: 29-oct-2026].

[2] U.S. Geological Survey, “Chapter A6.3. Specific Conductance,” *Techniques and Methods*, libro 9, cap. A6.3, 2019, doi: 10.3133/tm9A6.3.
