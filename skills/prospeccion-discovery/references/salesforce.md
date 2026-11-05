# Operación en Salesforce

Regla base: **mostrar el cambio y esperar el OK del comercial** antes de cualquier escritura. Solo campos vacíos. Nunca Propietario, Estado, Rating ni Tipo de registro sin pedido explícito.

## Quién es el comercial
Usa el usuario conectado: sus leads son los de `OwnerId` = su usuario (o `Owner.Email` = su correo). No trabajes leads de otro comercial sin avisar.

## Detalles técnicos que evitan problemas
- **Regla de asignación:** al crear o actualizar leads por REST manda el header `Sforce-Auto-Assign: FALSE`. Sin él la regla puede reasignar los leads a otra persona. Después de actualizar, consulta `OwnerId` y confirma que no cambió.
- `OwnerId` no se puede cambiar por API en este org: si hay que reasignar, el comercial lo hace a mano en la interfaz.
- **Tareas:** el `Subject` es una lista restringida en la API REST estándar (Call, Email, Other…). Si un asunto libre como "Llamada primer toque – …" falla, usa una herramienta o conector que acepte asunto libre o avisa al comercial; no cambies el asunto a un valor genérico sin decirlo (los informes filtran por "WhatsApp…" y "Llamada…").
- **Duplicados:** las reglas de duplicados están inactivas. Antes de crear un lead o contacto, busca por nombre, correo y teléfono en Lead y Contact.
- **Celular:** suele venir en `Phone` y no en `MobilePhone`. Reconócelo por patrón: CO 3xxxxxxxxx (10 dígitos), PE 9xxxxxxxx (9), MX 10 dígitos.
- **Montos:** las oportunidades mezclan COP y USD. Nunca sumes como una sola moneda; muestra moneda y totales por moneda.
- Listas restringidas con tipos de registro: si un valor no está habilitado, no lo fuerces; usa "Otra" y explica en el detalle.

## Campos del Lead que usa la skill
| Campo (API) | Tipo | Uso |
|---|---|---|
| UsaSalesforce__c / UsaSAP__c | Casilla | Tecnología confirmada (solo con evidencia) |
| CRMActual__c / NombreCRM__c | Lista / texto | CRM actual |
| ERPActual__c / NombreERP__c | Lista / texto | ERP actual |
| Inter_s_Principal__c | Lista | Venta que abre la señal |
| CompetenciaIdentificada__c | Texto | Partner actual |
| RequiereIntegraciones__c | Casilla | Integración pendiente |
| LinkedIn_URL__c | URL | Perfil del contacto |
| Senal_Compra__c | Lista | Tipo de señal (ver investigacion-senales.md) |
| Senal_Detalle__c | Texto largo | Qué pasó, en una o dos frases |
| Senal_Fuente__c | URL | Link de la señal |
| Senal_Fecha__c | Fecha | Fecha de la señal |
| Estado_IA__c | Lista | Pendiente → Investigando → Para revisar → Aprobado → Enviado, o Descartado |
| Fecha_Revision_IA__c | Fecha | Día en que se redactó o revisó |
| Mensaje_IA_Original__c | Texto largo | Primer borrador sin tocar (asunto + cuerpo) |
| Mensaje_Personalizado__c | Texto largo | Versión que aprueba o edita el comercial |
| Mensaje_WhatsApp__c | Texto largo (4000) | WhatsApp de segundo toque |
| Description | Texto largo | Notas fechadas `[Prospección AAAA-MM-DD] … (fuente)` y `[Pausa AAAA-MM-DD]` |

Estado_IA__c = "Descartado" cuando la empresa ya es cliente, tiene oportunidad abierta, la persona dijo "No interesado" o no hay SAP/Salesforce tras investigar; el motivo va en la Descripción.

## Campañas por lote
- Una campaña por lote. El nombre **empieza con "Prospección Lote"** (por ejemplo "Prospección Lote Dic 2026 – [iniciales del comercial]"), para que salga en los dashboards.
- Estados de miembro: **Pendiente** (por defecto) → **Enviado** → **Respondida** → **Reunión**.
- Arma el lote de mayor a menor valoración, por empresa completa, y revisa que ningún lead esté ya en otra campaña activa de prospección.
- Al confirmar un envío: miembro → Enviado; lead "Nuevo" → "Contactado o Trabajado"; `Estado_IA__c` → "Enviado".
- Cuando responde: miembro → Respondida. Con reunión agendada: miembro → Reunión.

## Tareas
| Tarea | Asunto | Estado | Detalle |
|---|---|---|---|
| WhatsApp de segundo toque | `WhatsApp segundo toque – [Nombre] ([Empresa])` | Abierta, vence al día siguiente del correo | Descripción con el mensaje y el link wa.me |
| WhatsApp enviado | mismo asunto | Completed cuando el comercial confirma | |
| Intento de llamada | `Llamada [primer/segundo/tercer] toque – [Nombre] ([Empresa])` | Completed siempre, conteste o no | Subtipo Llamada, `CallDisposition`, hora y número en Descripción |
| Retomar | `Retomar – [Empresa]` | Abierta, en la fecha acordada | Motivo y quién respondió |

Valores de `CallDisposition`: `No contestó` · `Contestó` · `Reunión agendada` · `No interesado` · `Número equivocado` · `Buzón`.

Los correos que el comercial envía desde Gmail se registran solos como tarea (TaskSubtype = Email) por Einstein Activity Capture o Salesforce Inbox, casi siempre en un minuto. Valida que exista antes de marcar el miembro como Enviado.

## Pausa por no interés
Cuando alguien responde "no estamos interesados", "ahora no" o similar:
1. Su lead → "No interesado/No Calificado" (si dijo que no) y su miembro de campaña → Respondida.
2. **Todos los leads de esa empresa** llevan en la Descripción `[Pausa AAAA-MM-DD] [quién] dijo "[qué]". No contactar hasta AAAA-MM-DD.`
3. Se cancelan o aplazan las tareas abiertas de la empresa y se crea **una** tarea "Retomar" a 3 meses (o en la fecha que dio el cliente).
4. Al retomar, solo con una señal nueva.

Todo esto se propone en una tabla y se aplica con el OK del comercial.
