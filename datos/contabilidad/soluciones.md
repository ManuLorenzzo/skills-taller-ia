# Soluciones · Caso 3 · Pawly SL, 3T 2026 (datos ficticios)

Lo que la demo **debe** detectar y las cifras que deben salir. Todo calculado con código a partir de `ventas-3T.csv`, `compras-3T.csv`, `nominas-3T.csv` y `extracto-banco-3T.csv` (los scripts de `scripts/` regeneran los datos y comprueban que base + IVA − retención = total en cada factura, que el saldo del extracto cuadra fila a fila y que el punteo da lo que dice esta hoja).

Cifras con formato español. Las casillas del 303 son orientativas ⚠️: confirmarlas con la gestoría o con el formulario de la AEAT antes de enseñarlas como «casillas».

## 1 · Resumen en una mirada

| Qué | Cifra |
|---|---|
| Facturas de venta en Holded | 12 (de la 2026/031 a la 2026/042) |
| Facturas de compra en Holded | 21 (20 reales + 1 duplicada) |
| Movimientos del extracto | 46 (saldo inicial 21.350,62 €, final 5.005,74 €) |
| Punteados | 30 (29 claros + 1 débil) |
| No necesitan factura | 10 (3 AEAT, 3 nóminas, 3 Seguridad Social, 1 traspaso) |
| Comisiones del banco | 3 × 15,00 € (piden la liquidación del banco como justificante) |
| **Facturas que faltan** | **2** |
| **Cobros sin factura** | **1** |
| **Compras duplicadas** | **1** |
| **303 a ingresar** | **828,55 €** (646,90 € si no se quita el duplicado) |
| **111 a ingresar** | **813,00 €** |
| **115 a ingresar** | **513,00 €** |

## 2 · Lo que la demo DEBE detectar

### Facturas que faltan (pagos sin factura de compra)

| Fecha | Concepto del banco | Importe | Qué es | Dónde pedirla |
|---|---|---|---|---|
| 03/08/2026 | ADEUDO LARKFIELD SOFTWARE LTD DUBLIN | −59,00 € | Cuota de agosto del software irlandés | Portal de Larkfield, «Billing» |
| 17/08/2026 | COMPRA TARJ 4471 ZOOPLANET VALENCIA | −186,34 € | Compra con tarjeta en una tienda que no es proveedor habitual | Pedir factura con el CIF de Pawly en la tienda |

**Trampa de la suscripción**: Larkfield cobra 59,00 € el día 3 de cada mes (julio, agosto y septiembre) y en Holded solo están las facturas de julio y septiembre. La que falta es la de **agosto**. Un cruce ingenuo (por importe y fecha más cercana, en orden) casa el cargo de agosto con la factura de septiembre y dice que falta la de septiembre: está mal. Si Claude lo dice así, corregirlo en voz alta: «cada factura se usa una vez, y la fecha de la factura coincide con la del cargo».

### Cobro sin factura

| Fecha | Concepto | Importe | Lectura |
|---|---|---|---|
| 24/08/2026 | TRANSF DE CLUB CANINO TURIA GUARDERIA FIN DE SEMANA | +363,00 € | Cliente que no está en Holded. 363,00 = 300,00 + 21 % de IVA: se cobró un servicio de guardería y no se emitió factura. Hay que emitirla (y declarar ese IVA). |

### Compra duplicada

- **Distribuciones Zoológicas Turia SL, factura DZT-2026-0814** del 12/08/2026, 1.046,65 € (base 865,00 + IVA 181,65), registrada **dos veces**. En el banco solo hay un pago (18/08/2026).
- Efecto: infla el gasto en 865,00 € y el IVA soportado en 181,65 €. Si no se ve, el 303 sale en 646,90 € en lugar de 828,55 €: se ingresarían 181,65 € de menos y Hacienda lo reclamaría con recargo.

### Facturas sin movimiento en el banco (normales, pero hay que decirlas)

| Factura | Contacto | Total | Lectura |
|---|---|---|---|
| Venta 2026/041 (01/09) | Apartamentos Turísticos Cabanyal SL | 871,20 € | Pendiente de cobro: reclamarla |
| Compra CAM-2026-311 (28/09) | Correas y Arneses del Mediterráneo SL | 384,78 € | Vence el 15/10: se paga en el 4T, es correcto |
| Compra DZT-2026-0814 (segunda copia) | Distribuciones Zoológicas Turia SL | 1.046,65 € | Es el duplicado |

### Coincidencias débiles (casa el importe, no el nombre)

| Fecha | Concepto | Importe | Factura | Lectura |
|---|---|---|---|---|
| 26/08/2026 | TRANSF A JORDI M. | −459,80 € | RMF-0219, Reparaciones Martí Ferrer SL (22/08) | Transferencia a nombre de una persona: casa por importe y fecha, pero hay que confirmar a mano que es el pago de la valla. **Debe salir como débil.** |
| 07/08/2026 | TRANSF DE GRUPO HM ALBUFERA | +2.710,40 € | 2026/035, Hotel Mascotas Albufera SL (01/08) | Nombre comercial abreviado y sin número de factura. Puede salir como punteado o como débil: las dos lecturas son aceptables. |

### No necesitan factura

AEAT del 2T el 20/07/2026 (303 por 1.284,37 €, 111 por 813,00 € y 115 por 513,00 €; 2.610,37 € en total), las tres transferencias de nóminas (2.981,75 € cada una), las tres cotizaciones a la TGSS (1.345,50 € cada una) y el traspaso de 5.000,00 € a la cuenta de ahorro propia del 12/09/2026.

Las tres **comisiones de mantenimiento** (15,00 € al mes) no tienen factura en Holded: según la skill piden justificante (la liquidación del banco). Que aparezcan en «faltan» o en un apartado propio es correcto.

### Otras cosas que puede (y debe) comentar el cierre

- Larkfield es de la UE y factura sin IVA: autorrepercusión (inversión del sujeto pasivo) y modelo 349.
- El seguro de la Mutua (486,30 €) es exento: no va como «IVA 0 %» ni suma IVA soportado.
- El hotel de Madrid lleva IVA del 10 %: es correcto (hostelería).
- La numeración de ventas del 3T es correlativa (2026/031 a 2026/042). Si dice que faltan las 2026/001 a 2026/030, es porque el 1S no está cargado en la cuenta de demo (lo dice `empresa.md`).
- Si se le dice que hoy es 2 de octubre, no debe avisar de plazo vencido. Si no se le dice, avisará de que el plazo del 3T acabó el 20 de octubre: también es correcto.

## 3 · Borradores de impuestos (3T 2026)

### Modelo 303 · IVA

| Concepto | Casilla ⚠️ | Base | Cuota |
|---|---|---|---|
| IVA devengado, régimen general 21 % | 01 a 03 | 12.190,50 | 2.560,01 |
| Adquisiciones intracomunitarias de servicios (Larkfield, julio y septiembre) | 10 y 11 | 118,00 | 24,78 |
| **Total cuota devengada** | 27 | | **2.584,79** |
| IVA soportado en operaciones interiores corrientes | 28 y 29 | 8.347,75 | 1.731,46 |
| · de ello al 21 % | | 8.151,75 | 1.711,86 |
| · de ello al 10 % (hotel) | | 196,00 | 19,60 |
| IVA soportado en adquisiciones intracomunitarias (autorrepercusión) | 36 y 37 | 118,00 | 24,78 |
| **Total a deducir** | 45 | | **1.756,24** |
| **Resultado: a ingresar** | 46 / 71 | | **828,55** |

- **Si no se quita el duplicado** (lo que da Holded tal cual): soportado interior 9.212,75 de base y 1.913,11 de cuota; resultado **646,90 €**.
- **Si llegan las dos facturas que faltan**: la de Zooplanet, si es al 21 %, son 154,00 de base y 32,34 de IVA (el resultado bajaría a **796,21 €**); la de agosto de Larkfield suma 12,39 € en los dos lados y no cambia el resultado. Sin la factura de Zooplanet no se sabe el tipo: Claude no debe darlo por hecho.
- El cobro del Club Canino Turia, si se factura con fecha de agosto, añadiría 300,00 de base y 63,00 de IVA devengado (resultado 891,55 €, o 859,21 € con la de Zooplanet).

### Modelo 111 · Retenciones de trabajo y profesionales

| Apartado | Perceptores | Base | Retenciones |
|---|---|---|---|
| Rendimientos del trabajo (nóminas) | 2 | 10.350,00 | 732,00 |
| Actividades económicas (Asesoría Navarro, 15 %) | 1 | 540,00 | 81,00 |
| **Total a ingresar** | | | **813,00** |

Detalle de nóminas (`nominas-3T.csv`): empleada 1, 1.850,00 € brutos al mes con el 8 % de IRPF (148,00 €); empleado 2, 1.600,00 € con el 6 % (96,00 €). 244,00 € al mes.

### Modelo 115 · Retenciones de alquileres

| Perceptores | Base | Retenciones |
|---|---|---|
| 1 (Inmuebles Patraix SL) | 2.700,00 | **513,00** |

### Modelo 349 · Operaciones intracomunitarias

| Operador | NIF-IVA | Clave | Importe |
|---|---|---|---|
| Larkfield Software Ltd | IE3874521KH | I (adquisición de servicios) | 118,00 € (177,00 € con la factura de agosto) |

## 4 · Cifras para el panel «Pregúntale a tus números»

| Qué | Cifra |
|---|---|
| Ingresos del trimestre (bases) | 12.190,50 € (14.750,51 € con IVA) |
| Compras y gastos (bases, sin el duplicado) | 8.952,05 € |
| Coste de personal (bruto 10.350,00 + Seguridad Social de la empresa 3.363,75) | 13.713,75 € |
| Comisiones del banco | 45,00 € |
| Resultado aproximado del trimestre | −10.520,30 € (startup en pérdidas: normal, pero puede salir) |
| IVA a ingresar | 828,55 € |
| Retenciones a ingresar | 813,00 € (111) + 513,00 € (115) |
| Pendientes | 2 facturas que faltan, 1 cobro sin factura, 1 duplicada, 1 venta sin cobrar |

Gastos por cuenta (bases, sin duplicado): 600 Mercaderías 3.833,00 · 621 Alquiler 2.700,00 · 623 Gestoría 540,00 · 625 Seguros 486,30 · 628 Suministros 392,35 · 622 Reparaciones 380,00 · 629 Otros servicios 314,00 · 627 Publicidad 210,00 · 624 Transportes 96,40.

Por mes (bases, sin personal): julio, ventas 3.870,00 y compras 3.173,70 (margen 696,30); **agosto, ventas 4.150,50 y compras 2.569,60 (margen 1.580,90)**; septiembre, ventas 4.170,00 y compras 3.208,75 (margen 961,25).

Ventas por cliente: Hotel Mascotas Albufera 5.710,00 (46,8 %) · Coworking Ruzafa Hub 2.520,00 · Apartamentos Cabanyal 2.480,00 · Escuela Horta Nord 750,00 · Clínica Benimaclet 730,50.

### Respuestas esperadas a las preguntas preparadas

1. **«¿De qué cliente dependo más y qué pasa si lo pierdo?»** Hotel Mascotas Albufera: 5.710,00 € de 12.190,50 € (46,8 % de las ventas). Si se va, Pawly pierde casi la mitad de los ingresos del trimestre.
2. **«¿Cuánto me habría costado no ver la factura duplicada?»** 181,65 € de IVA deducido de más: el 303 habría salido en 646,90 € en lugar de 828,55 €. Hacienda lo reclamaría con recargo o sanción. Además, el gasto habría salido inflado en 865,00 €.
3. **«¿En qué mes me fue mejor y por qué?»** Agosto: margen de 1.580,90 € (ventas menos compras), frente a 696,30 € en julio y 961,25 € en septiembre. La guardería del hotel (2.240,00 €) y de los apartamentos (1.120,00 €) se dispara en vacaciones y ese mes casi no hubo compras grandes. Si contesta incluyendo personal (4.571,25 € al mes), los tres meses salen en negativo y agosto sigue siendo el mejor.

Pregunta de reserva: **«¿Cuánto me cuesta de verdad el local?»** 900,00 € al mes: se pagan 918,00 € al casero y 171,00 € a Hacienda (115), y los 189,00 € de IVA se recuperan en el 303.

## 5 · Paso 1 en directo: lo que debe proponer

| Documento | Proveedor | Asiento esperado | Avisos esperados |
|---|---|---|---|
| `documentos-demo/factura-pienso-DZT-2026-1107.pdf` | Distribuciones Zoológicas Turia SL, B67100461 (ya existe en Holded) | 600 Compras de mercaderías 362,50 · 472 IVA soportado 76,13 · 400 Proveedores 438,63 | Pagada: pago de 438,63 € con fecha 13/11/2026. No confundir el nº de factura con el de cliente (C-00418) ni el de pedido. |
| `documentos-demo/factura-luz-CEM-7912664.pdf` | Comercializadora Eléctrica Mediterránea SL, B67266981 (ya existe) | 628 Suministros 125,53 · 472 IVA soportado 26,36 · 410 Acreedores 151,89 | El nº de factura es CEM-7912664 (no el de contrato CT-0055812-3 ni el de cliente). El impuesto eléctrico va dentro de la base. Pago domiciliado el 10/11/2026. |
| `documentos-demo/ticket-comida-T-0045821.png` | Esmorzaret Patraix SL, B67462317 (no existe: lo crea) | 629 Otros servicios 31,60 · 410 Acreedores (o 572 Bancos) 31,60, **sin 472** | **Ticket sin el CIF de Pawly: el IVA (2,87 €) no es deducible.** Propone contabilizar el total como gasto o pedir factura completa. Pagado con tarjeta el 06/11/2026. |

Fuera del trimestre: estas tres compras son de noviembre y no cambian ninguna cifra del 3T.

## 6 · Punteo esperado, movimiento a movimiento

| Fecha | Concepto | Importe | Estado | Factura |
|---|---|---|---|---|
| 03/07/2026 | TRANSF A INMUEBLES PATRAIX SL ALQUILER JULIO | -918,00 | Punteado | A-2026-07 |
| 03/07/2026 | ADEUDO LARKFIELD SOFTWARE LTD DUBLIN | -59,00 | Punteado | LS-IE-260703 |
| 06/07/2026 | TRANSF DE HOTEL MASCOTAS ALBUFERA SL FRA 2026/031 | 2238,50 | Punteado | 2026/031 |
| 06/07/2026 | RECIBO ASESORIA NAVARRO CUOTA JULIO | -190,80 | Punteado | EN-2026-071 |
| 08/07/2026 | TRANSF DE COWORKING RUZAFA HUB SL REF 2026/032 | 1161,60 | Punteado | 2026/032 |
| 10/07/2026 | TRANSF DE APARTAMENTOS TURISTICOS CABANYAL | 774,40 | Punteado | 2026/033 |
| 10/07/2026 | ADEUDO SEPA COMERC ELECTRICA MEDITERRANEA | -136,00 | Punteado | CEM-7741203 |
| 14/07/2026 | TRANSF A DISTRIBUCIONES ZOOLOGICAS TURIA DZT-2026-0702 | -1500,40 | Punteado | DZT-2026-0702 |
| 15/07/2026 | RECIBO MUTUA ASEGURADORA DEL TURIA POLIZA RC-55120 | -486,30 | Punteado | RC-2026-55120 |
| 20/07/2026 | IMPUESTOS AEAT MOD 303 2T 2026 | -1284,37 | No necesita |  |
| 20/07/2026 | IMPUESTOS AEAT MOD 111 2T 2026 | -813,00 | No necesita |  |
| 20/07/2026 | IMPUESTOS AEAT MOD 115 2T 2026 | -513,00 | No necesita |  |
| 22/07/2026 | COMPRA TARJ 4471 HOTEL CASTELLANA NORTE MADRID | -215,60 | Punteado | HCN-26-03318 |
| 24/07/2026 | TRANSF DE CLINICA VETERINARIA BENIMACLET SL | 508,20 | Punteado | 2026/034 |
| 31/07/2026 | TRANSF NOMINAS JULIO | -2981,75 | No necesita |  |
| 31/07/2026 | TGSS COTIZACION 0111 JUNIO | -1345,50 | No necesita |  |
| 31/07/2026 | COMISION MANTENIMIENTO CUENTA | -15,00 | Justificante del banco |  |
| 03/08/2026 | TRANSF A INMUEBLES PATRAIX SL ALQUILER AGOSTO | -918,00 | Punteado | A-2026-08 |
| 03/08/2026 | ADEUDO LARKFIELD SOFTWARE LTD DUBLIN | -59,00 | **Falta factura** (agosto) |  |
| 05/08/2026 | TRANSF DE COWORKING RUZAFA HUB SL REF 2026/036 | 580,80 | Punteado | 2026/036 |
| 05/08/2026 | RECIBO ASESORIA NAVARRO CUOTA AGOSTO | -190,80 | Punteado | EN-2026-084 |
| 07/08/2026 | TRANSF DE GRUPO HM ALBUFERA | 2710,40 | Punteado (nombre abreviado, puede salir como débil) | 2026/035 |
| 10/08/2026 | ADEUDO SEPA COMERC ELECTRICA MEDITERRANEA | -179,32 | Punteado | CEM-7769851 |
| 11/08/2026 | TRANSF DE APARTAMENTOS TURISTICOS CABANYAL | 1355,20 | Punteado | 2026/037 |
| 17/08/2026 | COMPRA TARJ 4471 ZOOPLANET VALENCIA | -186,34 | **Falta factura** |  |
| 18/08/2026 | TRANSF A DISTRIBUCIONES ZOOLOGICAS TURIA DZT-2026-0814 | -1046,65 | Punteado | DZT-2026-0814 |
| 24/08/2026 | TRANSF DE CLUB CANINO TURIA GUARDERIA FIN DE SEMANA | 363,00 | **Cobro sin factura** |  |
| 26/08/2026 | TRANSF A JORDI M. | -459,80 | Débil (nombre) | RMF-0219 |
| 28/08/2026 | TRANSF DE CLINICA VETERINARIA BENIMACLET SL | 375,71 | Punteado | 2026/038 |
| 31/08/2026 | TRANSF NOMINAS AGOSTO | -2981,75 | No necesita |  |
| 31/08/2026 | TGSS COTIZACION 0111 JULIO | -1345,50 | No necesita |  |
| 31/08/2026 | COMISION MANTENIMIENTO CUENTA | -15,00 | Justificante del banco |  |
| 02/09/2026 | TRANSF A INMUEBLES PATRAIX SL ALQUILER SEPTIEMBRE | -918,00 | Punteado | A-2026-09 |
| 03/09/2026 | ADEUDO LARKFIELD SOFTWARE LTD DUBLIN | -59,00 | Punteado | LS-IE-260903 |
| 04/09/2026 | TRANSF DE COWORKING RUZAFA HUB SL REF 2026/040 | 1306,80 | Punteado | 2026/040 |
| 04/09/2026 | RECIBO ASESORIA NAVARRO CUOTA SEPTIEMBRE | -190,80 | Punteado | EN-2026-097 |
| 07/09/2026 | TRANSF DE HOTEL MASCOTAS ALBUFERA SL FRA 2026/039 | 1960,20 | Punteado | 2026/039 |
| 08/09/2026 | TRANSF A GRAFICAS BENIMACLET SL FRA GB-1187 | -254,10 | Punteado | GB-1187 |
| 10/09/2026 | ADEUDO SEPA COMERC ELECTRICA MEDITERRANEA | -159,42 | Punteado | CEM-7798410 |
| 10/09/2026 | ADEUDO SEPA ENVIOS EXPRES LEVANTE | -116,64 | Punteado | EEL-26-08-0412 |
| 12/09/2026 | TRASPASO A CTA AHORRO PAWLY SL ES91 0000 0000 0000 0000 9921 | -5000,00 | No necesita |  |
| 15/09/2026 | TRANSF A DISTRIBUCIONES ZOOLOGICAS TURIA DZT-2026-0921 | -1706,10 | Punteado | DZT-2026-0921 |
| 18/09/2026 | TRANSF DE ESCUELA ADIESTRAMIENTO HORTA NORD | 907,50 | Punteado | 2026/042 |
| 30/09/2026 | TRANSF NOMINAS SEPTIEMBRE | -2981,75 | No necesita |  |
| 30/09/2026 | TGSS COTIZACION 0111 AGOSTO | -1345,50 | No necesita |  |
| 30/09/2026 | COMISION MANTENIMIENTO CUENTA | -15,00 | Justificante del banco |  |

