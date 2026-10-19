# Modelo de nueve subcomponentes — paquete protegido

Paquete versión 3.2 actualizado el 19 de octubre de 2026. Incluye el Python autocontenido, el documento del modelo, el registro de cambios y las instrucciones de ejecución.

## Cambios de esta versión

- Limita el porcentaje de plazo transcurrido a **100 %** en SQLite. Los créditos que alcanzaron o superaron su vencimiento quedan en **100 — Plazo cumplido**. Al repetir la ejecución corrige también porcentajes anteriores superiores a 100.

- Acepta entradas que ya contienen algunas o todas las columnas derivadas. Las recalcula desde las variables de negocio y deja una sola copia de cada una de las 26 salidas, con sus nombres canónicos. Un resultado NULL sustituye igualmente el valor anterior.

- Permite repetir el proceso sobre la misma salida reconocida del modelo. Prepara el resultado completo, guarda un respaldo SQLite `.db.bak` y actualiza la tabla en una transacción. Un fallo conserva la salida anterior.
- Añade `porcentaje_plazo_transcurrido` (REAL) y `segmento_plazo_transcurrido` (TEXT), después de las 24 derivadas anteriores: **26 en total**.
- Usa el corte fijo **2026-08-09**, configurable mediante `--fecha-corte AAAA-MM-DD`. Calcula días reales transcurridos sobre días hasta el vencimiento teórico según el plazo en meses de calendario.
- Segmenta en Inicio (0–25 %), En desarrollo (>25–50 %), Avanzado (>50–75 %), Tramo final (>75–<100 %) y Plazo cumplido (100 %). El valor guardado tiene máximo de 100 %; datos inválidos quedan sin porcentaje y con una incidencia explícita.
- Mantiene los subperfiles de Riesgo por CIFIN 776 y de Vehículo por carrocería, junto con las reglas de Protección, Prepago y cuota inicial.

El indicador mide tiempo contractual, no capital ni cuotas pagadas; «Plazo cumplido» no acredita cancelación, mora o prepago. Las fechas de desembolso admiten ISO o día/mes/año, sin inferir seriales de Excel.

Supera **111 pruebas automatizadas**, incluidas 10.920 combinaciones de regresión de Riesgo, entradas con 24 o 26 derivadas, columnas parciales y encabezados equivalentes, comparación de las salidas anteriores, fronteras temporales y tope de 100 %, fin de mes y bisiestos, repetición del script, respaldo con WAL y rollback durante la actualización. La distribución final requiere ejecutar esta versión sobre la base original.

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

Para procesar una entrada ya segmentada, usar `python aplicar_modelo.py --db base_ya_segmentada.db --salida resultado_actualizado.db`. La salida debe ser un archivo distinto de la entrada.

El origen se abre en modo de solo lectura. El programa omite créditos vacíos y conserva las columnas originales. Admite resultados ya segmentados como entrada cuando conservan las variables de negocio necesarias. Recalcula únicamente las 26 derivadas conocidas; el resto de columnas se conserva. No reemplaza bases ajenas.

La contraseña se entrega por separado. Este repositorio distribuye los fuentes y documentos dentro del ZIP cifrado y no contiene bases de datos. `SHA256SUMS` permite comprobar la integridad de la descarga.
