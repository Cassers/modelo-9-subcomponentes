# Modelo de nueve subcomponentes — paquete protegido

Paquete versión 2.7 actualizado el 13 de octubre de 2026. Incluye el Word corregido del modelo y el registro detallado de cambios, junto con el Python y las instrucciones de ejecución. El registro distingue los cambios aplicados, las decisiones posteriores y los ajustes técnicos pendientes.

## Contenido del paquete

- `Modelo_9_Subcomponentes_Entregable.docx`: documento del modelo con los ajustes de la entrega.
- `Detalle_de_cambios_del_modelo.docx`: registro de cambios por componente y estado de los pendientes.
- `aplicar_modelo.py`: script para aplicar el modelo sobre una base SQLite local.
- `LEEME.txt`: instrucciones de ejecución.

Esta actualización sincroniza el Python, el Word y el registro de cambios. La versión 2.7 utiliza PorcCtaInic como porcentaje exacto registrado (0,4987 equivale a 49,87 %). Cuando falta ese dato, utiliza RPorcCtaInic como respaldo. CtaInic solo distingue cero de positivo; no se reconstruye el porcentaje desde importes. Las discrepancias con el rango quedan señaladas en el motivo, con prioridad para el porcentaje exacto válido. Conserva la recuperación de segmentos inequívocos, la identificación de puntajes estimados y las 24 columnas derivadas. Supera 65 pruebas vigentes. Los pendientes de otros componentes siguen identificados en los documentos.

## Descargar y abrir

1. [Descargar el ZIP protegido](https://github.com/Cassers/modelo-9-subcomponentes/raw/refs/heads/main/Modelo_9_Subcomponentes_protegido.zip).
2. Abrirlo con una herramienta compatible con **ZIP AES-256**, como 7-Zip o WinRAR.
3. Introducir la contraseña recibida por separado y extraer los archivos.
4. Seguir las instrucciones de `LEEME.txt`.

La contraseña se entrega por separado y no está publicada en GitHub. Este repositorio no contiene bases de datos. El script requiere Python 3.10 o posterior y procesa la base SQLite localmente.

El archivo `SHA256SUMS` permite comprobar la integridad de la descarga. Los archivos fuente y el documento se distribuyen dentro del ZIP cifrado.
