# Modelo de nueve subcomponentes — paquete protegido

Paquete versión 2.9 actualizado el 19 de octubre de 2026. Incluye el Python autocontenido, el documento del modelo, el registro de cambios y las instrucciones de ejecución.

## Cambios de esta versión

- El antiguo grupo favorable de Riesgo se divide por CIFIN 776 en «Cliente sólido con respaldo externo» y «Cliente favorable con respaldo externo limitado». Los otros cuatro perfiles y la prioridad de fuentes se conservan.
- El antiguo «Práctico Funcional» de Vehículo se divide en «Práctico sedán/hatchback» y «Práctico SUV», usando la carrocería registrada y conservando las demás prioridades.
- Protección mantiene sus categorías. Se conservan las reglas de cuota inicial de la versión 2.8, los pesos y las mismas 24 columnas derivadas.

Supera 87 pruebas automatizadas, incluidas 10.920 combinaciones de regresión de Riesgo y ejecución SQLite del script independiente. La distribución final requiere ejecutar esta versión sobre la base original. Los documentos detallan los criterios y los pendientes de los demás componentes.

## Contenido del paquete

- `aplicar_modelo.py`: Python 3.10 o posterior, sin dependencias externas.
- `Modelo_9_Subcomponentes_Entregable.docx`: reglas de aplicación vigentes.
- `Detalle_de_cambios_del_modelo.docx`: historial y alcance de la actualización.
- `LEEME.txt`: instrucciones de ejecución.

## Descargar y ejecutar

1. [Descargar el ZIP protegido](https://github.com/Cassers/modelo-9-subcomponentes/raw/refs/heads/main/Modelo_9_Subcomponentes_protegido.zip).
2. Extraerlo con una herramienta compatible con **ZIP AES-256**, como 7-Zip o WinRAR, y la contraseña recibida por separado.
3. Colocar el script junto a la base SQLite original y ejecutar `python aplicar_modelo.py`.
4. Si existe una salida anterior, usar un nombre nuevo, por ejemplo `python aplicar_modelo.py --db cartera.db --salida resultado_v29.db`.

El origen se abre en modo de solo lectura y la salida conserva las columnas originales. El script omite créditos vacíos y no sobrescribe resultados existentes.

La contraseña se entrega por separado. Este repositorio distribuye los fuentes y documentos dentro del ZIP cifrado y no contiene bases de datos. `SHA256SUMS` permite comprobar la integridad de la descarga.
