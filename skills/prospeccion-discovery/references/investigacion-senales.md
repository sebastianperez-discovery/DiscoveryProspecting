# Investigar una cuenta y sus señales

## 1. Primero en Salesforce (solo lectura)
- Lead o contacto: cargo, empresa, país, industria, sitio web, LinkedIn_URL__c, UsaSalesforce__c, UsaSAP__c, CRMActual__c, ERPActual__c, Inter_s_Principal__c, campos Senal_*, Estado_IA__c, Descripción.
- La Descripción puede traer notas previas (`[Investigación …`, `[Prospección …`, `[Sales Agent …`): parte de ahí y no repitas.
- Actividades (tareas y correos) del lead y de la empresa: si alguien de Discovery ya habló con ellos, el mensaje lo retoma.
- Otros leads, contactos, cuentas u oportunidades de la misma empresa (por nombre o dominio del correo) y de qué comercial son. Si es de otro comercial, o hay oportunidad abierta, o ya es cliente: avisa y no escribas sin coordinar.
- `[Pausa` en la Descripción de cualquier lead de la empresa: no se escribe hasta la fecha indicada.
- Duplicados del mismo contacto (nombre, correo, teléfono): avisa para unificarlos a mano.

## 2. Después en la web, en este orden
1. ¿Usa Salesforce y qué nubes? Vacantes que piden Salesforce, empleados con cargos de Salesforce en LinkedIn, rastros técnicos (my.site.com, force.com, Account Engagement, Marketing Cloud), casos publicados.
2. ¿Usa SAP y qué versión? Vacantes SAP, perfiles, noticias de S/4HANA.
3. Vacantes recientes de Salesforce o SAP.
4. Cambio de líder de TI o CRM (menos de 90 días).
5. Noticias de los últimos 12 meses: expansión, fusión, inversión, nuevo ERP, nuevo mercado.

Solo das por cierto lo que tiene fuente. Si no hay evidencia, se dice.

## Señal válida
Un hecho de los últimos 12 meses, con fecha y link. Tipos (valores de Senal_Compra__c; si no existe el valor en la lista, usa "Otra" y explica en Senal_Detalle__c):

| Señal | Qué buscamos | Venta que abre | Prioridad |
|---|---|---|---|
| Vacante Salesforce | Admin, desarrollador o consultor Salesforce | Horas de soporte, staffing | Alta |
| Un solo administrador o ninguno | Usa Salesforce con una persona a cargo, o la perdió | Horas de soporte | Alta |
| Implementado por otro partner | Implementación reciente con otra consultora, o salida de ese partner | Soporte, mejoras | Alta |
| Necesidad de otra nube | Usa Sales Cloud y habla de servicio, marketing, datos o IA | Service, Marketing, Data Cloud, Agentforce | Alta |
| Integración pendiente | Salesforce y SAP/NetSuite sin integrar | Integración, MuleSoft | Alta |
| Crecimiento con CRM básico | Nueva sede, mercado o línea y CRM básico o ninguno | Implementación desde cero | Media |
| Líder nuevo | CIO, gerente de TI o líder CRM con menos de 90 días | Diagnóstico, soporte, nubes | Media |
| Vacante SAP | Auxiliar SAP, ABAP, funcional | Staffing, AMS SAP | Media |
| Cambio de ERP | ECC cerca del fin de soporte, anuncio de S/4HANA u otro ERP | Migración, AMS, integración | Media |

## Ficha de salida
```
Empresa: … (país, industria, tamaño)
Tecnología: Salesforce [nubes] / SAP [versión] — fuente: …
Señal: [tipo] · [hecho en una línea] · [fecha] · [link]
Contactos: [nombre, cargo] → quién va primero y por qué
Historial: [contactos previos, otro comercial, pausa, duplicados]
Recomendación: escribir / esperar (qué falta) / descartar (por qué)
Campos a llenar (vacíos): …
```

## Por lotes
Si piden investigar un lote: ordena de mayor a menor valoración (Rating, Lead Score, señal), agrupa por empresa y entrega una tabla con una fila por empresa. Guarda el resultado donde el comercial indique (CSV o .md) antes de proponer cambios en Salesforce.
