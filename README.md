# Modelo de nueve subcomponentes — paquete protegido

Paquete versión 3.0 actualizado el 19 de octubre de 2026. Incluye el Python autocontenido, el documento del modelo, el registro de cambios y las instrucciones de ejecución.

## Cambios de esta versión

- Permite repetir el proceso sobre la misma salida reconocida del modelo. Prepara el resultado completo, guarda un respaldo SQLite `.db.bak` y actualiza la tabla en una transacción. Un fallo conserva la salida anterior.
- Añade `porcentaje_plazo_transcurrido` (REAL) y `segmento_plazo_transcurrido` (TEXT), después de las 24 derivadas anteriores: **26 en total**.
- Usa el corte fijo **2026-08-09**, configurable mediante `--fecha-corte AAAA-MM-DD`. Calcula días reales transcurridos sobre días hasta el vencimiento teórico según el plazo en meses de calendario.
- Segmenta en Inicio (0–25 %), En desarrollo (>25–50 %), Avanzado (>50–75 %), Tramo final (>75–<100 %) y Plazo cumplido (≥100 %). Conserva porcentajes superiores a 100 %; datos inválidos quedan sin porcentaje y con una incidencia explícita.
- Mantiene los subperfiles de Riesgo por CIFIN 776 y de Vehículo por carrocería, junto con las reglas de Protección, Prepago y cuota inicial.

El indicador mide tiempo contractual, no capital ni cuotas pagadas; «Plazo cumplido» no acredita cancelación, mora o prepago. Las fechas de desembolso admiten ISO o día/mes/año, sin inferir seriales de Excel.

Supera **100 pruebas automatizadas**, incluidas 10.920 combinaciones de regresión de Riesgo, comparación de las 24 salidas anteriores, fronteras temporales, fin de mes y bisiestos, repetición del script, respaldo con WAL y rollback durante la actualización. La distribución final requiere ejecutar esta versión sobre la base original.

## Contenido del paquete

- `aplicar_modelo.py`: Python 3.10 o posterior, sin dependencias externas.
- `Modelo_9_Subcomponentes_Entregable.docx`: reglas de aplicación vigentes.
- `Detalle_de_cambios_del_modelo.docx`: historial y alcance de la actualización.
- `LEEME.txt`: instrucciones de ejecución.

## Descargar y ejecutar

1. [Descargar el ZIP protegido](https://github.com/Cassers/modelo-9-subcomponentes/raw/refs/heads/main/Modelo_9_Subcomponentes_protegido.zip).
2. Extraerlo con una herramienta compatible con **ZIP AES-256**, como 7-Zip o WinRAR, y la contraseña recibida por separado.
3. Colocar el script junto a la base SQLite original y ejecutar `python aplicar_modelo.py`.
4. Para volver a generar la misma salida, repetir el comando. La ruta del respaldo anterior se informa en consola. Si un visor bloquea la base, cerrar su conexión y repetir.

Si existen varias bases o tablas compatibles, indicar `--db cartera.db --tabla-origen cartera`. Se puede elegir otra salida con `--salida resultado.db`.

El origen se abre en modo de solo lectura. El programa omite créditos vacíos y conserva las columnas originales. No reemplaza bases ajenas ni usa un resultado segmentado como origen.

La contraseña se entrega por separado. Este repositorio distribuye los fuentes y documentos dentro del ZIP cifrado y no contiene bases de datos. `SHA256SUMS` permite comprobar la integridad de la descarga.
