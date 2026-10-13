# SOINGES · Compras, fletes y precios

Aplicación: https://angieram26-bot.github.io/improved-invention/

## Registrar cada compra

1. Identifica el envío con proveedor, fecha, facturas y guía.
2. Ingresa una sola vez el transporte total, incluidos manejo y cargos asociados. Si no hay flete, ingresa 0; un campo vacío queda pendiente.
3. Agrega los productos realmente recibidos en ese envío: cantidad, costo base unitario después de descuentos, otros costos unitarios e IVA de venta.
4. Elige reparto por valor de compra, unidades comparables o peso total de cada fila.
5. Revisa los resultados y pulsa Guardar envío.

El costo base se ingresa con un criterio consistente. El sistema no determina el tratamiento tributario del IVA de compra. El IVA de venta es un dato independiente por producto. No incluye liquidación tributaria ni retenciones.

## Cálculos

El flete se asigna proporcionalmente a la base seleccionada. Los centavos residuales se asignan a las filas con mayor residuo para conciliar exactamente el total del transporte.

Costo unitario = costo base + otros costos unitarios + flete asignado / cantidad.

Venta unitaria antes de IVA = costo unitario / (1 - margen / 100).

El margen se expresa sobre la venta antes de IVA, no como recargo sobre el costo. Las cantidades pueden ser fraccionarias. Máximo 100 productos por envío. Los valores unitarios visualizados se redondean a dos decimales.

## Historial y respaldo

Los envíos se guardan en localStorage del navegador y dispositivo utilizados. No se suben a GitHub, no hay cuentas ni sincronización automática entre equipos, y borrar datos del navegador puede eliminar el historial.

- Historial permite buscar, abrir, actualizar y eliminar compras.
- Exportar productos descarga el envío actual como CSV con separador punto y coma, compatible con Excel. Este CSV no reemplaza el respaldo del historial.
- Descargar respaldo exporta todas las compras guardadas a JSON. No incluye cambios pendientes.
- Importar respaldo agrega compras nuevas. Si ya existe el mismo identificador, conserva la compra local; no sobrescribe ni duplica ese registro.

Haz respaldos periódicos y antes de cambiar de equipo o limpiar el navegador.

## Importar facturas PDF o imágenes

En Productos del envío, pulsa Adjuntar factura PDF o imagen y selecciona el archivo.

- PDF de hasta 25 MB: muestra la primera página y permite elegir un rango de hasta 20 páginas por lectura. Si tiene más páginas, selecciona sucesivos rangos sin repetirlos.
- JPG, PNG y WebP de hasta 15 MB y 32 megapíxeles.
- Pulsa Leer productos del archivo. En PDF, el modo automático extrae texto ordenando las columnas por posición. Si una página no produce candidatos de productos, intenta OCR de esa página. También puedes elegir Leer todas como imagen.
- Revisa las filas propuestas, corrige las cantidades y costos y desmarca líneas incorrectas. Confirma la revisión antes de agregar los productos al envío.
- También puedes pegar texto copiado de una factura.

Los archivos se procesan en el navegador y no se conservan en el historial ni en el respaldo. PDF.js 4.10.38 y Tesseract.js 6.0.1 se descargan desde CDN bajo demanda, por lo que se necesita internet. El contenido de la factura no se envía a un servicio de análisis. No se conecta automáticamente a OneDrive.

Las sugerencias no garantizan detectar todas las líneas ni interpretar el IVA. La detección básica espera descripción, cantidad, precio unitario y total opcional. Las filas con más columnas dejan cantidad y costo pendientes para su revisión. Los productos reciben el IVA de venta por defecto y otros costos en cero, editables después.

Si una página falla, se muestra un aviso de resultado incompleto con sus números. Los PDF protegidos requieren una copia sin contraseña. Importar el mismo rango dos veces puede duplicar productos; revisa antes de agregarlos. Cada envío admite hasta 100 filas.

## Verificación

Se verificaron la sintaxis JavaScript, los cálculos de precio y flete, la conciliación de centavos y el separador de productos con formatos numéricos colombiano e inglés. PDF.js de la misma versión utilizada por la aplicación extrajo productos de un PDF de prueba de dos páginas. Se probó mediante simulación el flujo de un PDF mixto (texto e imagen), cierre del lector y avisos de páginas fallidas.

La lectura OCR completa de facturas reales y la interfaz requieren prueba final en el navegador del usuario.
