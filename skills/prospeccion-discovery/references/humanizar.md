# Humanizar los textos para clientes

Todo correo, WhatsApp o guion que va a un cliente pasa por la skill **humanizer** antes de mostrarlo. Viene en este mismo repo (`skills/humanizer`).

## Cómo usarla
1. Redacta el borrador.
2. Pásalo por la skill humanizer: que lo reescriba para que suene a la persona que escribe, sin cambiar lo que dice ni agregar datos.
3. Revisa que siga cumpliendo la guía (señal en la primera línea, qué hacemos, una pregunta, largo) y muestra solo la versión final.

## Si la skill humanizer no está instalada
Avisa al comercial en una línea y dale cómo instalarla:
- **Claude Code / Cowork:** ya viene con el plugin `discovery-prospecting`; si no aparece, `/plugin install discovery-prospecting@discovery-partners` otra vez.
- **Claude web o escritorio:** subir `humanizer.zip` (está en el repo, o comprimir la carpeta `skills/humanizer`) en Ajustes → Capacidades → Skills.
- **Slackbot o Salesforce:** pegar el contenido de `skills/humanizer/SKILL.md` como otra habilidad.

Mientras tanto, aplica tú esta lista antes de mostrar el texto.

## Lista mínima (lo que más delata un texto de IA en español)
- Contrastes de relleno: "no es X, es Y", "no se trata de…, sino de…". Di solo lo que es.
- Tríadas forzadas ("rápido, simple y efectivo") y listas de tres por costumbre.
- Guiones largos (—) en medio de las frases. Usa punto o coma.
- Arranques preparados: "Te cuento algo:", "La verdad es que…", "Imagínate…".
- Frases de cierre que repiten la idea: "Al final, lo importante es…".
- Palabras infladas: "clave", "fundamental", "potenciar", "robusto", "sinergia", "transformar", "llevar al siguiente nivel", "solución integral".
- Lenguaje de venta: "única oportunidad", "no te lo puedes perder", urgencia inventada.
- Muletillas repetidas entre mensajes: "te dejo una pregunta corta", "sin compromiso".
- Negritas, emojis o mayúsculas para dar énfasis.
- Halagos genéricos: "me impresionó mucho su trayectoria".
- Frases que suponen la situación del cliente: "sé que les cuesta…", "suele pasar que…".

Prueba final: léelo en voz alta como si lo dijera el comercial por teléfono. Si una frase no la diría, se cambia.
