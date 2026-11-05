# Discovery Prospecting

Skill de Claude para el equipo comercial de Discovery Partners. Acompaña la prospección de punta a punta: investigar cuentas y señales de compra, redactar correos y WhatsApp, preparar llamadas, crear campañas "Prospección Lote" y tareas en Salesforce, registrar intentos de llamada, usar los campos IA del Lead y revisar los pendientes del día.

Uso interno de Discovery Partners. No compartir fuera de la empresa.

## Qué trae

```
skills/prospeccion-discovery/
├── SKILL.md                       reglas, flujo y a qué referencia ir en cada caso
└── references/
    ├── discovery-icp.md           quiénes somos, servicios, cliente ideal y ángulo por tecnología
    ├── investigacion-senales.md   qué revisar en Salesforce y en la web; tipos de señal; ficha
    ├── correos-whatsapp.md        estructura, qué no va, plantillas, ejemplo y lista de chequeo
    ├── llamadas.md                guion, preguntas orientadas al "no", objeciones, registro
    ├── salesforce.md              campos, campañas, tareas, CallDisposition, pausa, detalles técnicos
    └── cadencia-pendientes.md     cadencia y "¿qué hago hoy?"
```

## Requisitos
- Claude con los conectores de **Salesforce** (lectura y escritura) y **Gmail**, y búsqueda web activa.
- Recomendado: la skill **humanizer** (los textos para clientes pasan por ella).

## Instalación

**Claude (web o escritorio)**
1. Descarga este repo (Code → Download ZIP) y descomprímelo.
2. Comprime solo la carpeta `skills/prospeccion-discovery` en un .zip.
3. En Claude: Ajustes → Capacidades → Skills → Subir skill, y elige ese .zip. Actívala.

Si Discovery tiene plan Team o Enterprise, el dueño de la organización puede subirla una vez para todo el equipo.

**Claude Code / Cowork**
```
/plugin marketplace add sebastianperez-discovery/DiscoveryProspecting
/plugin install discovery-prospecting@discovery-partners
```
El repo es privado: necesitas acceso en GitHub.

**Slackbot o Salesforce (Habilidades de Agentforce)**
Crea la habilidad y pega el contenido de `SKILL.md`; si permite adjuntar archivos, agrega también los de `references/`.

## Cómo se usa
Pídele en lenguaje natural, por ejemplo:
- "Investiga a Proquinal y dime si le escribimos."
- "Arma el correo y el WhatsApp para el lead de Bryan Moreno."
- "Prepárame la llamada con Tecnoglass."
- "Ya envié los correos de hoy, regístralos."
- "¿Qué hago hoy?"

La skill nunca envía mensajes ni cambia Salesforce sin tu OK.

## Cambios
Las mejoras se proponen por pull request. Cambios de reglas comerciales, con aprobación de Sebastián Pérez.
