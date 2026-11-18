# Mi empresa · Pawly SL (EMPRESA FICTICIA)

> Todo lo de este fichero es inventado para la demo de KowiikLab: la empresa, el CIF, la dirección, los clientes, los proveedores, sus NIF y las cuentas bancarias. Los NIF tienen formato válido, pero no corresponden a nadie a propósito. No usar fuera de la formación.

Bloque pensado para la sección «Mi empresa» de las skills `contabilizar-gasto`, `puntear-facturas` y `cierre-trimestre`. En la demo se adjunta este fichero en el primer mensaje (ver `../../caso-3-contabilidad.md`).

## Datos generales

- **Nombre fiscal**: Pawly SL
- **CIF**: B67314823 (ficticio). NIF-IVA intracomunitario: ESB67314823.
- **Dirección**: Carrer de les Mascotes, 7, bajo, 46020 València (ficticia).
- **Actividad**: servicios para mascotas: paseos, guardería de perros y una tienda online pequeña de pienso y accesorios.
- **Forma**: sociedad limitada (SL).
- **Régimen de IVA**: general. Declaración trimestral (modelo 303).
- **Alta en el ROI** (operadores intracomunitarios): sí.
- **Programa de contabilidad y facturación**: Holded, con conector.
- **Banco**: una sola cuenta operativa en «Banco Ficticio del Turia», terminada en 4417. Extracto en CSV (separador `;`, decimales con coma, cinco filas de cabecera antes de la tabla). Hay además una cuenta de ahorro propia terminada en 9921: los traspasos entre las dos no necesitan factura.
- **Pasarelas de cobro**: ninguna. Los clientes pagan por transferencia.

## Personas, alquiler y profesionales

- **Empleados con nómina**: 2. Las nóminas no están en Holded: van en `nominas-3T.csv`.
- **Alquila un local**: sí, a Inmuebles Patraix SL. Se le retiene el 19 % (modelo 115).
- **Profesionales con retención**: la gestora, Elena Navarro Climent (autónoma, Asesoría Navarro). Se le retiene el 15 % (modelo 111).
- **Operaciones con la UE**: compra de software a Larkfield Software Ltd (Irlanda), que factura sin IVA: inversión del sujeto pasivo y modelo 349. No vende fuera de España.
- **Gestoría**: Asesoría Navarro. Quiere un Excel con una pestaña por modelo (303, 111, 115 y 349) y la lista de facturas pendientes, por correo antes del día 10 del mes siguiente al trimestre.

## Proveedores habituales y su cuenta

| Proveedor | NIF | Cuenta PGC | Qué vende | Dónde está su factura |
|---|---|---|---|---|
| Inmuebles Patraix SL | B67333096 | 621 Arrendamientos | Alquiler del local (IVA 21 %, retención 19 %) | Correo, el día 1 de cada mes |
| Elena Navarro Climent (Asesoría Navarro) | 73958214N | 623 Profesionales | Gestoría fiscal, contable y laboral (IVA 21 %, retención 15 %) | Correo, el día 1 de cada mes |
| Larkfield Software Ltd (Irlanda) | IE3874521KH | 629 Otros servicios | Software de reservas, 59 € al mes sin IVA (inversión del sujeto pasivo) | Portal de Larkfield, apartado «Billing», el día 3 de cada mes |
| Distribuciones Zoológicas Turia SL | B67100461 | 600 Compras de mercaderías | Pienso, snacks y arena para revender en la tienda online | Correo, con cada pedido |
| Correas y Arneses del Mediterráneo SL | B67220814 | 600 Compras de mercaderías | Accesorios para revender | Correo, con cada pedido |
| Comercializadora Eléctrica Mediterránea SL (marca LuzMed) | B67266981 | 628 Suministros | Luz del local, recibo domiciliado | Área de clientes de LuzMed |
| Mutua Aseguradora del Turia | V67411371 | 625 Primas de seguros | Seguro de responsabilidad civil y de animales en custodia (exento de IVA) | Correo, una vez al año |
| Envíos Exprés Levante SL | B67162743 | 624 Transportes | Envíos de la tienda online, factura mensual | Portal del transportista |
| Gráficas Benimaclet SL | B67499038 | 627 Publicidad | Folletos y carteles | Correo |
| Reparaciones Martí Ferrer SL | B67055129 | 622 Reparaciones | Mantenimiento del local | Correo |
| Hotel Castellana Norte SL | B67388207 | 629 Otros servicios | Hotel en viajes a ferias (IVA 10 %) | Recepción del hotel |

Clientes habituales: Hotel Mascotas Albufera SL, Coworking Ruzafa Hub SL, Apartamentos Turísticos Cabanyal SL, Clínica Veterinaria Benimaclet SL y Escuela de Adiestramiento Horta Nord SL.

## Gastos que la gestoría trata de forma especial

- Tickets de comida sin el CIF de Pawly: gasto sin IVA deducible (629). Si es posible, pedir factura completa.
- Comisiones del banco (626): exentas; el justificante es la liquidación mensual del banco.

## Notas sobre los datos de Holded (cuenta de demo)

- La serie de facturas de venta de 2026 empieza en 2026/001. En la cuenta de demo solo están cargadas las del tercer trimestre (de la 2026/031 a la 2026/042): las anteriores existen, pero no se han cargado. No es un hueco de numeración.
- Los impuestos del segundo trimestre se pagaron el 20/07/2026: 303 por 1.284,37 €, 111 por 813,00 € y 115 por 513,00 €.
