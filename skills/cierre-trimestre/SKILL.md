---
name: cierre-trimestre
description: Prepara el cierre del trimestre de una pyme o autónomo en España. Concilia banco y Holded, revisa facturas y deja el borrador de IVA y retenciones para la gestoría.
---

# Cierre del trimestre

Úsala cuando el usuario diga cosas como «haz el trimestre», «cierra el trimestre», «prepara el 303», «qué me falta para la gestoría» o «revisa que esté todo contabilizado».

## Mi empresa (rellénalo una vez)

Antes de preguntar, mira si ya los tienes en las instrucciones o ficheros del proyecto, o en tu memoria del usuario. Si están, úsalos sin preguntar. Si no, pregúntalos al empezar y propón guardarlos en tu memoria para no volver a preguntarlos. Quien prefiera, puede escribirlos aquí mismo antes de subir la skill.

- Forma: sociedad (SL) o autónomo.
- Régimen de IVA: general (por defecto), recargo de equivalencia, exento u otro.
- ¿Tiene empleados con nómina? ¿Paga a profesionales con retención (abogados, asesores)? ¿Alquila un local?
- ¿Compra o vende a empresas de otros países de la UE o de fuera de la UE?
- Banco o bancos que usa.
- Gestoría: nombre y cómo le gusta recibir la documentación.

## Reglas que no se rompen

1. **Solo lectura.** En el programa de contabilidad (Holded u otro) no creas, cambias ni borras nada en esta skill. Si algo hay que corregir, lo apuntas en el informe.
2. **No presentas nada a Hacienda.** Preparas borradores para que la gestoría o el usuario los revisen.
3. **Nunca inventes un dato.** Si falta una factura, un importe o un tipo de IVA, se marca como pendiente.
4. **Pregunta lo que no sepas** en vez de suponer, y agrupa las preguntas al final.

## Paso 1 · Qué trimestre

Por defecto, el trimestre natural que acaba de cerrar según la fecha de hoy, salvo que el usuario diga otro. Trabaja con tres rangos:

- El trimestre exacto (para los impuestos).
- El trimestre con 15 días más (para compras del trimestre que se pagan después).
- El año entero hasta hoy (para revisar la numeración de las facturas y, si es autónomo, el pago fraccionado).

Plazos habituales de presentación: 1T del 1 al 20 de abril, 2T del 1 al 20 de julio, 3T del 1 al 20 de octubre y 4T del 1 al 30 de enero. Si hoy está cerca del límite, avísalo arriba del informe.

## Paso 2 · Reunir los datos

- **Banco**: pide el extracto del trimestre en CSV o Excel. Detecta tú las columnas (fecha, concepto, importe, o Debe y Haber) y salta las filas de cabecera que el banco pone antes de la tabla.
- **Programa de contabilidad** (con el conector de Holded, si está conectado): compras del rango con colchón, facturas de venta y rectificativas del año, contactos, cuentas de gasto y libro diario del trimestre. Si el conector no está, pide exportaciones en Excel.
- Antes de seguir, comprueba que los datos cubren el periodo entero. Si un mes viene vacío o muy por debajo de lo normal, pregúntalo.

## Paso 3 · Puntear el banco

Usa la skill `puntear-facturas` para el trimestre. Si no está instalada, cruza con código cada salida del banco con una compra y cada entrada con una venta (importe con 0,50 € o 2 % de margen, fechas a menos de 45 días, nombre parecido) y marca las coincidencias dudosas para revisar a mano.

## Paso 4 · Revisar las facturas emitidas (año entero)

- Numeración correlativa por serie, sin huecos ni duplicados.
- Fechas coherentes con el orden de los números.
- Cada factura anulada tiene su rectificativa.
- No quedan borradores antiguos sin emitir.

## Paso 5 · Revisar las compras

- Cada compra está en una cuenta del Plan General Contable coherente con **quién es el proveedor y qué vende**, no con palabras sueltas de la línea.
- Busca **compras duplicadas** (mismo proveedor y mismo número de factura): inflan el gasto y el IVA soportado.
- Marca los gastos con **deducibilidad parcial** o dudosa (vehículo, combustible, móvil, suministros de casa): son la causa típica de descuadre con la gestoría.
- **Proveedores extranjeros**:
  - De la UE: normalmente inversión del sujeto pasivo (la factura viene sin IVA y se autorrepercute). Si la empresa no está dada de alta en el censo de operadores intracomunitarios (ROI), el proveedor puede cobrar IVA español y ese IVA puede no ser deducible: avísalo.
  - De fuera de la UE: también inversión del sujeto pasivo en servicios, pero sin modelo 349.
  - Comprueba en cada factura qué sociedad factura de verdad (algunas plataformas facturan unas veces desde EE. UU. y otras desde su filial en Irlanda).

## Paso 6 · Borradores de impuestos

Calcula solo lo que aplique según «Mi empresa» y enséñalo como **borrador para contrastar**:

- **IVA trimestral (303)**: IVA repercutido de las ventas menos IVA soportado deducible de las compras, incluida la autorrepercusión de las operaciones con inversión del sujeto pasivo (suman en los dos lados).
- **Retenciones de trabajo y profesionales (111)**: retenciones de nóminas y de facturas de profesionales del trimestre.
- **Retenciones de alquileres (115)**: si alquila un local y retiene al arrendador.
- **Pago fraccionado de autónomos (130)**: en estimación directa, en general el 20 % del rendimiento neto acumulado del año, menos los pagos de trimestres anteriores y las retenciones que le hayan practicado. Si casi todas sus facturas llevan retención, puede no estar obligado: pregúntalo.
- **Operaciones con la UE (349)**: lista de clientes y proveedores intracomunitarios del trimestre.

Si hay libro diario, contrasta tus cifras con los saldos de las cuentas de IVA soportado (472), IVA repercutido (477) y retenciones (4751), y con el saldo del banco (572) frente al extracto. Explica cualquier diferencia.

## Paso 7 · Entregables

1. **Informe** en el chat, en este orden:
   - Resumen en cinco líneas: qué está bien, cuánto falta y la cifra de cada borrador.
   - **Facturas que faltan**: proveedor, fecha, importe y dónde suele descargarse.
   - Movimientos que no necesitan documento.
   - Movimientos no identificados.
   - Cobros sin factura.
   - Compras sin movimiento en el banco y compras duplicadas.
   - Diferencias con el libro diario.
   - Preguntas para el usuario.
2. **Excel** con una pestaña por apartado y una pestaña «Para la gestoría» con los borradores.
3. Cuando el usuario suba lo que falta, **vuelve a pasar** el cierre hasta que la lista de pendientes quede vacía.

## Paso 8 · «Pregúntale a tus números» (artefacto, opcional)

Al terminar, ofrece: «¿Te hago un panel para preguntarle a tus números?». Si dice que sí, crea un **artefacto con IA integrada**:

- Arriba, cifras clave del trimestre: ingresos, gastos, IVA a pagar o a devolver, retenciones y número de pendientes.
- Gastos por cuenta en un gráfico de barras y, si hay datos, comparación con el trimestre anterior.
- La lista de pendientes (facturas que faltan, cobros sin factura).
- Una caja «Pregúntale a tus números» donde el usuario escribe en lenguaje normal («¿en qué he gastado más que el trimestre pasado?», «¿qué proveedor ha subido más?») y la IA responde usando **solo** los datos del panel, diciendo de dónde sale cada cifra y sin inventar.

Avisa de que el panel lleva datos de la empresa: si lo comparte, cualquiera con el enlace los verá.

## Recordatorios de cada trimestre (inclúyelos siempre)

- Las facturas del último mes de muchas plataformas llegan la primera semana del mes siguiente: sin ellas no se cierra.
- Pedir a la gestoría el borrador del 303 por casillas antes de presentar y explicar cualquier diferencia.
- Revisar seguros, alquiler y suministros: son recibos que se olvidan.

## Aviso final (siempre)

Termina con: «Esto es un borrador para revisar con tu gestoría. No sustituye a un asesor fiscal y no se ha presentado nada a Hacienda.»
