---
name: contabilizar-gasto
description: Contabiliza tickets y facturas de gasto de una pyme o autónomo en España. Lee el documento, propone el asiento en el Plan General Contable y, si hay conector, lo registra en Holded.
---

# Contabilizar un gasto

Úsala cuando el usuario suba una factura, un ticket o un recibo de gasto y diga cosas como «contabiliza esto», «mete este gasto», «pásalo a Holded» o «¿en qué cuenta va esto?». Si sube varios, trátalos uno a uno y al final da un resumen.

## Mi empresa (rellénalo una vez)

Antes de preguntar, mira si ya los tienes en las instrucciones o ficheros del proyecto, o en tu memoria del usuario. Si están, úsalos sin preguntar. Si no, pregúntalos al empezar y propón guardarlos en tu memoria para no volver a preguntarlos. Quien prefiera, puede escribirlos aquí mismo antes de subir la skill.

- Nombre fiscal y NIF de la empresa o del autónomo.
- Régimen de IVA: general (por defecto), recargo de equivalencia u otro.
- Programa de contabilidad: Holded (con conector), otro, o ninguno (solo Excel).
- Mis proveedores habituales y su cuenta (ejemplo: «Iberdrola → 628 Suministros», «Asesoría López → 623 Profesionales»).
- Gastos que mi gestoría trata de forma especial (ejemplo: vehículo al 50 %).

## Reglas que no se rompen

1. **El total impreso manda.** Copia el total tal como aparece; nunca lo calcules. Si las cifras no cuadran, se revisa la base, no el total.
2. **Transcribe, no deduzcas.** NIF y número de factura, carácter a carácter. Si no se leen bien, déjalos vacíos y pregúntalo. No confundas el número de factura con el de cliente, contrato o pedido.
3. **Nada se registra sin que el usuario lo vea.** Primero enseñas la propuesta; solo con su «sí» la registras.
4. **Ante la duda, pregunta.** Mejor una pregunta que un asiento mal hecho.

## Paso 1 · Leer el documento

- **Proveedor**: quien emite la factura (arriba, con su logo, NIF e IBAN). El cliente («Facturar a») es la empresa del usuario. Si el NIF del proveedor coincide con el de la empresa, te has equivocado de lado: revísalo.
- Datos a sacar: proveedor y NIF, número, fecha, concepto, base imponible, tipo y cuota de IVA, retención de IRPF si la hay, total y moneda.
- **IVA**: usa la cuota impresa. Solo si no viene desglosada (un ticket de bar), calcula base = total / (1 + tipo).
- **Recibo domiciliado del banco**: el número de recibo hace de número de factura.
- **Moneda extranjera**: guarda la moneda original y usa el cambio impreso o el del día de la factura, nunca el de hoy.

## Paso 2 · Comprobar

- **¿Está a nombre de la empresa?** Si la factura va a otra persona o empresa, no se contabiliza: avisa.
- **¿Factura completa o ticket?** El IVA de un ticket solo es deducible si es una factura simplificada con el NIF de la empresa y el IVA desglosado. Si es un ticket sin NIF, propone contabilizar el total como gasto sin IVA deducible, o pedir factura completa.
- **¿Cuadra?** Base + IVA − retención = total (con 2 céntimos de margen). Si no cuadra, dilo.
- **Valores raros** (avisa, no bloquees): IVA distinto de 0, 4, 10 o 21 %; retención distinta de 1, 2, 7, 15 o 19 %.
- **¿Duplicado?** Antes de registrar, busca si ya existe una compra del mismo proveedor con el mismo número, o con el mismo total y fecha a menos de 3 días. Ojo con las confusiones típicas al leer (O y 0, S y 5): pueden ser la misma factura. Dos números correlativos son facturas distintas.

## Paso 3 · Elegir la cuenta (Plan General Contable)

Orden para decidir:

1. La cuenta que el usuario haya fijado para ese proveedor (sección «Mi empresa» o ficha del proveedor en el programa).
2. **Lo que se ha comprado, no quién lo vende**: folios comprados en Amazon son material de oficina; un café en una cafetería es una comida.
3. Esta tabla orientativa:

| Cuenta | Para qué |
|---|---|
| 600 Compras de mercaderías | Lo que la empresa compra para revender |
| 621 Arrendamientos y cánones | Alquiler de local, renting |
| 622 Reparaciones y conservación | Arreglos, mantenimiento |
| 623 Servicios de profesionales independientes | Gestoría, abogados, notaría, consultores |
| 624 Transportes | Mensajería, envíos |
| 625 Primas de seguros | Seguros |
| 626 Servicios bancarios y similares | Comisiones del banco |
| 627 Publicidad, propaganda y relaciones públicas | Anuncios, imprenta publicitaria |
| 628 Suministros | Luz, agua, gas, combustible, teléfono e internet |
| 629 Otros servicios | Software y suscripciones, viajes y hoteles, comidas, formación, material de oficina |
| 631 Otros tributos | Tasas, IBI, impuestos que no son IVA |

4. Si nada encaja, usa 629 y márcalo como «revisar».

La contrapartida: **410 Acreedores por prestaciones de servicios** para servicios y suministros, **400 Proveedores** para mercaderías. Si ya está pagado, el pago va contra **572 Bancos**.

## Paso 4 · IVA según el tipo de proveedor

- **Proveedor español**: IVA soportado deducible a la **472**.
- **Proveedor de la UE que factura sin IVA** (servicios): adquisición intracomunitaria con inversión del sujeto pasivo. Se autorrepercute: 472 al debe y 477 al haber por el mismo importe (no cuesta dinero, pero tiene que constar).
- **Proveedor de fuera de la UE que factura sin IVA**: inversión del sujeto pasivo, mismo tratamiento.
- **Factura con IVA de otro país**: ese IVA no es deducible en España. Súmalo al gasto y nunca a la 472.
- **Seguros, servicios bancarios y tasas**: exentos o no sujetos; no los pongas como «IVA 0 %».
- **Recargo de equivalencia** (comercio minorista): el recargo no es deducible y va al gasto.
- Aplica estos regímenes **solo si la factura viene sin IVA**. Si trae IVA español, respeta la factura y avisa si te parece raro.

## Paso 5 · Enseñar la propuesta

Muestra, antes de registrar nada:

```
Proveedor: ...  NIF: ...  Factura nº: ...  Fecha: ...
Concepto: ...

Cuenta                                  Debe     Haber
628 Suministros                       100,00
472 HP IVA soportado                   21,00
410 Acreedores por prest. servicios             121,00

Avisos: ...
¿Lo registro?
```

Si hay retención de IRPF, añade la **4751 Hacienda Pública, acreedora por retenciones practicadas** al haber y reduce la 410 en ese importe.

## Paso 6 · Registrar

**Con el conector de Holded:**

1. **Proveedor**: búscalo con `search_contacts` por NIF (sin el prefijo ES) y, si no aparece, por nombre. Si no existe, créalo con `create_contact` con su NIF y su cuenta de gasto por defecto. No modifiques fichas de proveedores que ya existan.
2. **Cuenta**: con `list_expenses_accounts` (o `list_accounting_accounts`) traduce el número de cuenta del PGC a la cuenta de Holded. Si no existe, avisa en vez de crearla.
3. **Duplicados**: antes de crear nada, revisa con `list_purchases` las compras de ese proveedor de las últimas semanas.
4. **Compra**: créala con `create_purchase` (no un asiento manual) con proveedor, número, fecha, moneda y líneas con precio sin IVA, impuestos y cuenta. Nace en borrador.
5. **Aprobar y adjuntar**: apruébala con `approve_purchase` (sin aprobar no genera asiento) y adjunta el documento original con `attach_purchase_file`.
6. **Comprobar**: con `get_purchase`, verifica que el total que calcula Holded coincide con el de la factura (2 céntimos de margen). Si no coincide, avisa y no registres el pago.
7. **Pago**: si ya está pagada, regístralo con `create_purchase_payment` y la fecha del cargo en el banco. Un pago mal hecho no se edita: se borra y se vuelve a crear.
8. **Si una llamada falla o tarda, antes de reintentar busca con `list_purchases` si la compra ya se creó**: reintentar a ciegas crea duplicados.

Holded pedirá confirmación en cada herramienta que escribe: es lo esperado, revisa y acepta.

Si el usuario prefiere no dar permisos de escritura, usa la vía más prudente: sube el documento al buzón de Holded con `upload_inbox` para que lo procese su escáner.

**Sin conector:** entrega el asiento y un Excel con columnas Fecha, Nº factura, Proveedor, NIF, Concepto, Cuenta, Base, Tipo IVA, Cuota IVA, Retención, Total y Avisos, listo para importar o pasar a la gestoría.

## Al terminar

Resume en una tabla lo registrado, lo que queda pendiente y por qué. Termina con: «Revisa los avisos con tu gestoría: esta propuesta no sustituye a un asesor contable.»
