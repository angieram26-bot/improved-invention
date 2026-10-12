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

## Alcance

Ingreso manual de productos y fletes. No extrae automáticamente facturas PDF ni se conecta a OneDrive. Las facturas empresariales no forman parte de este repositorio público.

## Verificación

Se verificaron sintaxis JavaScript, reparto de una factura de referencia, cálculo del precio de venta, reparto por peso, cantidades fraccionarias, validación de entradas, validación de registros de respaldo y conciliación de centavos en 500 casos. La revisión visual e interacción final se deben comprobar en navegador.
