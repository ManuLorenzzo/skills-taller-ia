# Cargar Pawly SL en la cuenta demo de Holded (antes del evento)

Objetivo: que la cuenta demo tenga **todo el tercer trimestre menos lo que debe faltar**, para que el paso 2 (punteo) y el paso 3 (cierre) encuentren exactamente lo que dice `soluciones.md`. Hacerlo la víspera, con tiempo para un ensayo completo y una limpieza después.

> Empresa, contactos y cifras son ficticios. Usar solo la cuenta demo, nunca una empresa real.

## 0 · La empresa

En la cuenta demo, configurar la empresa con los datos de `empresa.md`: Pawly SL, CIF B67314823, Carrer de les Mascotes, 7, bajo, 46020 València, régimen general de IVA, ejercicio 2026. ⚠️ Comprobar que la prueba de Holded deja usar la API y el conector (si no, «0 herramientas visibles» en Claude).

## 1 · Qué se carga y qué NO

| Se carga | Cuántos | De dónde |
|---|---|---|
| Contactos: 5 clientes y 11 proveedores, con NIF y cuenta por defecto | 16 | `empresa.md`, `ventas-3T.csv`, `compras-3T.csv` |
| Facturas de compra del 3T, **incluida la duplicada** (DZT-2026-0814 dos veces) | 21 | `compras-3T.csv` |
| Pagos de las compras que tienen `fecha_pago` (opcional, da realismo) | 19 | `compras-3T.csv` |
| Facturas de venta del 3T | 12 | `ventas-3T.csv` |
| Cobros de las ventas que tienen `fecha_cobro` (opcional) | 11 | `ventas-3T.csv` |

| NO se carga (es lo que la demo tiene que encontrar) |
|---|
| Factura de agosto de Larkfield (59,00 €) |
| Factura de Zooplanet (186,34 €) |
| Factura al Club Canino Turia (363,00 €) |
| Las nóminas (van en `nominas-3T.csv`, que se adjunta en el chat) |
| El extracto del banco: **no** importarlo ni conectar el banco en Holded; se sube en el chat |
| Los tres documentos de `documentos-demo/`: se registran en directo en el paso 1 |

## 2 · Cuentas e impuestos en Holded

- Cuentas de gasto que deben existir: 600, 621, 622, 623, 624, 625, 627, 628 y 629 (Holded usa números largos, tipo 62900000 ⚠️). Si falta alguna, crearla a mano en el cuadro de cuentas antes de cargar compras. La skill no crea cuentas: solo avisa.
- Impuestos que se usan: IVA 21 %, IVA 10 %, exento (seguro), **IVA de adquisición intracomunitaria de servicios con inversión del sujeto pasivo** (Larkfield), **retención IRPF 15 %** (gestoría) y **retención de alquileres 19 %** (local). ⚠️ Los nombres exactos de estos impuestos en Holded no están confirmados: mirarlos en Configuración > Impuestos ⚠️ y apuntarlos aquí.

## 3 · Cómo cargarlo

### Vía recomendada: pedírselo a Claude con el conector (compras y contactos)

En una conversación aparte de Claude Desktop (no la de la demo), con el conector de Holded conectado y permisos de escritura, adjuntar `compras-3T.csv`, `ventas-3T.csv` y `empresa.md` y pegar:

> «Esto es una carga de datos de prueba en una cuenta demo de Holded, no un gasto real: no uses la skill contabilizar-gasto ni me enseñes propuestas una a una. Con el conector de Holded:
> 1. Crea los contactos que no existan (clientes de ventas-3T.csv y proveedores de compras-3T.csv) con su NIF y, en los proveedores, la cuenta de gasto de la columna cuenta_pgc.
> 2. Crea las 21 compras de compras-3T.csv, una por fila, **también las dos filas con el mismo número DZT-2026-0814**: es intencionado. Usa número, fecha, proveedor, concepto, base, tipo de IVA y retención tal como vienen. regimen_iva «exenta» es exento, no IVA 0 %; «intracomunitaria_isp» es inversión del sujeto pasivo.
> 3. Aprueba cada compra y comprueba con get_purchase que el total coincide con la columna total.
> 4. Registra el pago de las que tienen fecha_pago, con esa fecha.
> 5. Al final, dame una tabla con lo creado y cualquier fila que haya fallado. Si una llamada falla, antes de reintentar mira con list_purchases si ya se creó.»

Son unas 80 llamadas con confirmación: en el selector, permitir siempre para esta conversación ⚠️ (nombre exacto de la opción sin confirmar) o se eterniza.

**Si Holded rechaza el duplicado** (mismo proveedor y mismo número) ⚠️: crear la segunda copia con el número `DZT-2026-O814` (letra O en lugar del cero). La skill está avisada de esa confusión y debe marcarla igual como duplicada. Apuntarlo en `soluciones.md` si pasa.

### Ventas: importación o a mano

- **Importación de Holded**: Holded permite importar facturas desde un Excel con su propia plantilla (Ventas > Facturas > Importar ⚠️). **No conozco las columnas exactas de esa plantilla**: descargarla desde Holded y copiar en ella las columnas de `ventas-3T.csv` (que va en CSV estándar: coma como separador, punto decimal, fechas AAAA-MM-DD, UTF-8). Lo mismo vale para compras si se prefiere importar.
- **A mano**: son 12 facturas de una línea, unos 15 minutos.
- **Con el conector**: solo si muestra una herramienta para crear facturas de venta ⚠️ (en el ensayo, preguntar a Claude «¿qué herramientas de Holded tienes para crear facturas de venta?»).
- Numeración: las ventas deben llevar los números 2026/031 a 2026/042. Configurar una serie que permita esos números o editarlos al crear ⚠️.
- La venta 2026/041 (Apartamentos Cabanyal) **no** se marca como cobrada.

## 4 · Comprobación después de cargar

Pedir a Claude, en la misma conversación de carga: «Lista las compras y ventas de Holded entre el 01/07/2026 y el 30/09/2026 y dame los totales».

| Debe salir | Cifra |
|---|---|
| Compras | 21, bases 9.817,05 €, IVA 1.913,11 € (con el duplicado) |
| Ventas | 12, bases 12.190,50 €, IVA 2.560,01 € |
| Retenciones en compras | 513,00 € (alquiler) y 81,00 € (gestoría) |

Si Holded tiene su propio informe del 303 ⚠️, con el duplicado debería dar 646,90 € a ingresar (si la autorrepercusión de Larkfield está bien configurada). Si da otra cifra, revisar el impuesto de Larkfield.

## 5 · Después del ensayo (importante)

- **Borrar las tres compras creadas en el ensayo del paso 1** (DZT-2026-1107, CEM-7912664 y T-0045821) y sus pagos, y el contacto Esmorzaret Patraix SL. Si se quedan, en directo la skill dirá «ya existe» y se pierde el momento.
- No tocar nada del 3T: el punteo y el cierre son de solo lectura.
- Volver a pasar la comprobación del punto 4.
