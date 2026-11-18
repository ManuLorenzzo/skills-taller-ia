---
name: puntear-facturas
description: Puntea el extracto del banco contra las facturas de compra y venta (Holded u otro programa) de una pyme o autónomo en España y dice qué facturas faltan y qué no cuadra.
---

# Puntear facturas

Úsala cuando el usuario diga cosas como «puntea el banco», «qué facturas me faltan», «concilia el extracto», «cuadra el banco con Holded» o «qué cobros no tienen factura». También la usa la skill `cierre-trimestre` como primer paso.

## Mi empresa (rellénalo una vez)

Antes de preguntar, mira si ya los tienes en tu memoria del usuario. Si no, pregúntalos al empezar y propón guardarlos en tu memoria para no volver a preguntarlos. Quien prefiera, puede escribirlos aquí mismo antes de subir la skill.

- Banco o bancos que usa y formato del extracto (CSV o Excel).
- Programa de facturación: Holded (con conector), otro, o ninguno.
- Pasarelas de cobro (Stripe, PayPal, TPV del banco) si las hay.
- Proveedores habituales y dónde se descargan sus facturas (portal, correo).

## Reglas que no se rompen

1. **Solo lectura.** En el programa de facturación no creas, cambias ni borras nada. Lo que haya que corregir, se apunta.
2. **Nunca inventes una factura ni un importe.** Lo que no está, se marca como pendiente.
3. **Usa código para cruzar**, no lo hagas a ojo: con decenas de movimientos, a ojo se escapan.

## Paso 1 · Periodo

Por defecto, el mes o trimestre que diga el usuario. Si no lo dice, pregúntalo. Para las facturas, mira el periodo con 15 días más por cada lado: hay facturas que se pagan después y cobros que llegan antes.

## Paso 2 · Datos

- **Banco**: el extracto en CSV o Excel. Detecta tú las columnas (fecha, concepto, importe, o Debe y Haber) y salta las filas que el banco pone antes de la tabla. Si hay varios bancos, júntalos indicando de cuál viene cada movimiento.
- **Facturas** (con el conector de Holded, si está conectado): facturas de compra y de venta del periodo con colchón, y los contactos. Si el conector no está, pide la exportación en Excel.
- Comprueba que los datos cubren todo el periodo. Si un mes viene vacío o muy por debajo de lo normal, pregúntalo antes de seguir.

## Paso 3 · Puntear

- Cada **salida** del banco se casa con una factura de compra; cada **entrada**, con una factura de venta.
- Casan si: importe igual con tolerancia de 0,50 € o del 2 % (cambio de divisa), fechas a menos de 45 días y nombre del proveedor o cliente parecido al concepto del banco.
- **Coincidencia débil**: casa el importe pero no el nombre. Se marca para revisar a mano.
- **Varias facturas en un pago**: si el concepto cita números de factura, casa por referencia aunque una transferencia pague varias.
- **Cargos mensuales del mismo importe** (suscripciones, alquiler): cuidado con casar el cargo de este mes con la factura del mes anterior. Cada factura se usa una sola vez.
- **Pasarelas de cobro**: los cobros llegan agrupados y con la comisión ya descontada. Casa el ingreso con el conjunto de ventas y no esperes ver la comisión en el banco.

## Paso 4 · Lo que no casa

Por defecto, **todo movimiento necesita su factura o justificante**. Solo se libran:

- Pagos de impuestos (AEAT) y de la Seguridad Social o cuota de autónomo.
- Nóminas.
- Traspasos entre cuentas propias.
- Devoluciones.

Los **pagos con tarjeta** y las **comisiones del banco** sí piden justificante. Los **cobros sin factura** se preguntan siempre.

Busca también al revés: **facturas sin movimiento en el banco** (pendientes de pago o cobro, o pagadas por otra vía) y **facturas duplicadas** (mismo proveedor y mismo número).

## Paso 5 · Entregables

1. **Resumen en el chat**:
   - Cuántos movimientos hay, cuántos punteados y cuántos pendientes.
   - **Facturas que faltan**, agrupadas por proveedor, con fecha, importe y dónde suele descargarse. Es la lista para ir a pedirlas.
   - Coincidencias débiles para revisar.
   - Cobros sin factura.
   - Facturas sin movimiento y duplicadas.
2. **Excel** con todos los movimientos y una columna de estado (Punteado, Débil, Falta factura, No necesita, Cobro sin factura) y la factura asociada.
3. Cuando el usuario suba o registre lo que falta, **vuelve a puntear** hasta que la lista quede vacía.
