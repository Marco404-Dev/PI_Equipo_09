# Registro de evidencias y resultados

**Equipo 09 · 29/10/2026**

Este archivo distingue **observaciones reportadas** de **pruebas documentadas con archivos adjuntos**. No se crean fotos ni resultados de laboratorio ficticios.

## Avances comunicados por el equipo

| Elemento | Observación reportada | Evidencia pendiente de anexar | Estado |
|---|---|---|---|
| Comunicación LoRa | Se consiguió transmitir y recibir entre dos Heltec V4 a 915 MHz | Fotos, configuración y conteo de paquetes | Reportado; ensayo cuantitativo pendiente |
| Pantalla OLED | Se visualizaron valores en la pantalla durante pruebas | Foto legible y versión del sketch | Reportado |
| DS18B20 | Lectura de temperatura conseguida en pruebas individuales | Serie de datos y comparación con patrón | Reportado |
| Módulo de pH | Se verificó por multímetro una salida analógica aprox. de hasta 3 V en ensayos | Modelo, solución usada, lectura calibrada | Reportado; no calibrado |
| BME280 | Módulo detectado por I²C en una prueba previa | Foto de la placa, tensión real y serie de lecturas | Reportado; montaje V4 pendiente |
| Interruptor flotador P45 | Se identificaron estados de contacto abierto/cerrado en pruebas anteriores | Registro de 10 cambios y conexión final | Reportado; montaje V4 pendiente |
| Autonomía, panel, integración total | No se dispone de evidencia consolidada | Ensayos P07–P13 | Pendiente |

## Ficha reutilizable de ensayo

Copiar este bloque **debajo** cada vez que se complete una prueba:

```text
Ensayo ID:
Fecha y hora:
Responsable:
Componente y modelo:
Placa / versión de firmware:
Conexión y alimentación verificadas:
Condiciones de prueba:
Lecturas y unidades:
Referencia/patrón:
Incidencias:
Resultado: completado / incompleto / fallido
Enlace a evidencia:
Próximo ajuste:
```

## Organización sugerida de archivos

Si el equipo dispone de fotos/videos/CSV y acuerda subirlos, usar nombres sencillos como:

- `2026-10-29_P02_DS18B20_lecturas.csv`
- `2026-10-29_P08_LoRa_recepcion.jpg`
- `2026-10-29_P09_OLED_prueba.mp4`

**Importante:** no subir claves de API, tokens, contraseñas, archivos `.env`, identificadores privados ni grabaciones que expongan datos personales.

Los criterios están en [Plan de pruebas](Plan_de_pruebas.md); los datos técnicos verificables y sus fuentes IEEE en [Sensores](Modulo%20Electronico/Sensores.md).
