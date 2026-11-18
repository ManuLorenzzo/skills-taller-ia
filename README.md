# Skills del taller «Pon a la IA a currar por ti»

**Versión visual:** [manulorenzzo.github.io/skills-taller-ia](https://manulorenzzo.github.io/skills-taller-ia/) · enlace corto: [is.gd/kowiikia](https://is.gd/kowiikia)

Cinco skills para Claude que hacen trabajo de oficina por ti: contestar correo, vigilar tu sector, contabilizar gastos, puntear el banco y preparar el trimestre.

Es el material del taller «Del chat al sistema» (KowiikLab, 19 de noviembre de 2026). Está pensado para pymes y autónomos en España, sin conocimientos técnicos.

## Antes de empezar (solo una vez)

1. En Claude, ve a **Ajustes > Capacidades**.
2. Activa **Ejecutar código en la nube** y **Artefactos con IA integrada**.

Qué plan necesitas:

- **Las skills funcionan en el plan gratis.**
- **Las tareas programadas** (que algo se haga solo cada lunes) **necesitan un plan de pago**.

## Cómo instalar una skill

1. Descarga el ZIP de la skill que quieras desde la carpeta [`zips/`](zips/) (botón de descarga de GitHub). No hace falta descomprimirlo.
2. En Claude, ve a **Personalizar > Skills**, pulsa **+** y elige **Subir una skill**. Selecciona el ZIP.
3. Comprueba que la skill aparece en la lista y que está **activada**.

> Si en tu app los menús se llaman distinto, busca **Skills** dentro de **Personalizar**. En algunas versiones, «Subir una skill» está dentro de «Crear skill».

**La primera vez que la uses, te hará unas preguntas** sobre ti: «Mi empresa», «Mi estilo» o «Lo que vigilo», según la skill. Contesta con calma; cuanto mejor la rellenes, mejor trabaja. Si le dejas guardarlo en su memoria, no te lo vuelve a preguntar.

## Las cinco skills

| Skill | Para qué sirve | Qué necesita | Cómo pedírselo |
|---|---|---|---|
| **responder-correo** | Lee tu correo, separa lo que necesita respuesta y te deja borradores con tu estilo. Nunca envía nada. | Conector de Gmail u Outlook | «Revisa mi correo de hoy y déjame borradores» |
| **vigilante-semanal** | Resume lo nuevo de tu sector cada semana (normativa, ayudas, competencia), con fuente y fecha. | Nada extra. Plan de pago si quieres programarla | «Hazme el resumen semanal de mi sector» |
| **contabilizar-gasto** | Lee una factura o un ticket, propone el asiento y, si se lo confirmas, lo registra en Holded. | Conector de Holded (o solo te da un Excel) | «Contabiliza esta factura» (y la adjuntas) |
| **puntear-facturas** | Cruza el extracto del banco con tus facturas y te dice cuáles faltan y qué no cuadra. | Extracto del banco en CSV. Conector de Holded (o exportación en Excel) | «Puntea el banco de octubre: ¿qué facturas me faltan?» |
| **cierre-trimestre** | Prepara el trimestre: punteo, revisión de facturas y borrador de IVA y retenciones para tu gestoría. | Extracto del banco en CSV. Conector de Holded (o exportaciones en Excel) | «Prepárame el cierre del tercer trimestre» |

### Cómo conectar Holded

1. En Claude, ve a **Personalizar > Conectores > Añadir conector personalizado**.
2. Pega esta dirección: `https://mcp.holded.com/mcp`
3. Inicia sesión con tu cuenta de Holded cuando te lo pida.

Necesitas un plan de Holded que incluya API (desde el plan Basic). Cada vez que Claude vaya a escribir algo en Holded, te pedirá permiso: es lo normal, revísalo y acepta.

## Cómo dejar una tarea programada

Con un plan de pago, díselo en una conversación normal:

> «Cada lunes a las 8, ejecuta el vigilante semanal.»

> «Cada día laborable a las 8, revisa mi correo y déjame borradores. No envíes nada.»

Claude te enseña cómo queda la tarea y te pide que la confirmes. Corre en la nube, aunque tengas el ordenador apagado.

## Antes de instalar una skill que encuentres por internet

Una skill son instrucciones que Claude sigue al pie de la letra, con acceso a lo que tú le hayas conectado. En febrero de 2026, Snyk analizó 3.984 skills públicas: **el 13,4 % tenía fallos críticos y 76 eran directamente maliciosas** ([estudio de Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)).

Antes de instalar una, repasa esto:

1. **¿De dónde viene?** Mejor de alguien que conoces o de una fuente oficial.
2. **Abre el ZIP y lee el `SKILL.md`.** Es texto normal; si no entiendes qué hace, no la instales.
3. **¿Lleva carpetas con scripts (código)?** Que lo mire alguien técnico antes.
4. **¿Habla de enviar datos a webs o tiene texto raro u oculto?** Fuera.
5. **¿Te pide contraseñas o claves?** Fuera.
6. **Pruébala primero con datos inventados**, nunca con los de tus clientes.

Las cinco skills de este repo son solo texto, sin código. Puedes leerlas en la carpeta [`skills/`](skills/).

## Lo oficial que merece la pena

- **Plugins oficiales de Anthropic**: paquetes de skills y conectores por tipo de trabajo (ventas, finanzas, marketing, legal...). [github.com/anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins). Dentro de Claude están en **Personalizar > Plugins**, solo en planes de pago. Ojo: el de legal parte del derecho de EE. UU., no del español.
- **Skills oficiales de Anthropic**: [github.com/anthropics/skills](https://github.com/anthropics/skills). Las de Word, Excel, PowerPoint y PDF ya vienen dentro de la app; no hace falta instalarlas.

## Aviso importante

- Las skills de contabilidad **preparan borradores**. No sustituyen a tu gestoría ni presentan nada a Hacienda.
- **Prueba primero con datos inventados** y revisa lo que te devuelven antes de fiarte.
- Si vas a trabajar con datos de clientes, mejor en un **plan de empresa** (Team o similar), que incluye un acuerdo de tratamiento de datos.

## Datos de prueba

En la carpeta [`datos/`](datos/) tienes datos ficticios (facturas, extractos, correos) para repetir las demos del taller sin tocar nada real.

## Licencia y autoría

Creado por Manu Lorenzo. Licencia [MIT](LICENSE): puedes usarlo, copiarlo y adaptarlo a tu empresa libremente.
