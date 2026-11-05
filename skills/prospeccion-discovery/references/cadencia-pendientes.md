# Cadencia y pendientes del día

## Cadencia por persona
| Día | Toque | Regla |
|---|---|---|
| 1 | Correo | Lo envía el comercial, nunca automático |
| 2 | WhatsApp de segundo toque | Solo a quien recibió correo. Si no tiene WhatsApp, pasa a llamada |
| 3 a 6 | Llamada | Máximo 3 intentos en días y horas distintos; tras cada intento sin respuesta, WhatsApp corto de "te acabo de llamar" |
| 10 | Correo de cierre de ciclo | Corto; después no se insiste |

Sin respuesta tras 3 toques en 10 días hábiles: "No decisión" con fecha; se retoma solo con una señal nueva. Una persona por empresa al día. El comercial avisa cuándo envió; no programes envíos.

## "¿Qué hago hoy?"
Consulta (solo lectura) y responde con una lista de máximo 10 líneas, en este orden, cada una con la acción y el link al registro:

1. **Respuestas sin atender:** miembros en Respondida o correos de prospectos sin contestar.
2. **Reuniones por confirmar o preparar** hoy y mañana (ofrece el brief de llamada).
3. **WhatsApp de hoy:** tareas "WhatsApp…" abiertas que vencen hoy o antes. Entrega la tabla: nombre, empresa, teléfono, mensaje, link wa.me, Id de tarea, ¿Enviado?
4. **Llamadas de hoy:** personas con WhatsApp enviado hace 1 día o más sin respuesta y menos de 3 intentos; indica el número de intento y la última hora probada para cambiarla.
5. **Cierres de ciclo:** personas en el día 10 sin respuesta.
6. **Retomar:** tareas "Retomar…" que vencen hoy y pausas que terminan (`[Pausa` con fecha ≤ hoy).
7. **Leads en `Estado_IA__c` = "Para revisar"**: borradores esperando aprobación.
8. **Leads con señal de menos de 30 días sin contactar.**
9. **Vencidos:** tareas abiertas con fecha pasada.

Consultas de referencia (ajusta al usuario):
```sql
-- Tareas abiertas vencidas o de hoy del comercial
SELECT Id, Subject, ActivityDate, Who.Name, What.Name FROM Task
WHERE OwnerId = :usuario AND IsClosed = false AND ActivityDate <= TODAY ORDER BY ActivityDate
-- Miembros de campañas de prospección por estado
SELECT Campaign.Name, Status, LeadId, Lead.Name, Lead.Company FROM CampaignMember
WHERE Campaign.Name LIKE 'Prospección Lote%' AND Campaign.IsActive = true
-- Intentos de llamada por persona
SELECT WhoId, COUNT(Id) FROM Task WHERE OwnerId = :usuario AND Subject LIKE 'Llamada%' AND IsClosed = true GROUP BY WhoId
-- Borradores para revisar
SELECT Id, Name, Company, Fecha_Revision_IA__c FROM Lead WHERE OwnerId = :usuario AND Estado_IA__c = 'Para revisar'
```

## Cuando el comercial avisa que envió
1. Verifica en Salesforce la tarea del correo (TaskSubtype = Email) de cada persona; si falta, revisa en Gmail enviados.
2. Propón: miembro → Enviado, lead Nuevo → "Contactado o Trabajado", `Estado_IA__c` → Enviado, tarea de WhatsApp para mañana con mensaje y link wa.me.
3. Con su OK, aplica y confirma qué quedó hecho.

Cuando avisa qué WhatsApp envió: marca esas tareas como Completed. Antes de preparar un WhatsApp, pide revisar el chat para no duplicar.

## Medir
Cada viernes: respuestas y reuniones con fecha por cada 20 empresas contactadas, por tipo de señal y tecnología; intentos de llamada por conversación (por `CallDisposition`). Si una señal no convierte, se dice y se propone ajustar.
