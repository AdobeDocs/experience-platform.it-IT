---
title: Ordinazione marca temporale cliente
description: Scopri come aggiungere l’ordine delle marche temporali dei clienti ai set di dati per garantire la coerenza dei dati del profilo.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Ordine timestamp cliente

In Adobe Experience Platform, l’ordine dei dati non è garantito per impostazione predefinita quando si acquisiscono i dati tramite l’acquisizione in streaming nell’archivio profili. Con l’ordine della marca temporale del cliente, puoi garantire che l’ultimo messaggio, in base alla marca temporale del cliente fornita, verrà mantenuto nell’archivio profili. Tutti i messaggi non aggiornati verranno quindi eliminati e **non** saranno disponibili per l&#39;utilizzo in servizi a valle che utilizzano dati di profilo come segmentazione e destinazioni. Di conseguenza, questo consente ai dati del profilo di essere coerenti e di rimanere sincronizzati con i sistemi di origine.

Per abilitare l&#39;ordinamento delle marche temporali dei clienti, utilizzare il campo `extSourceSystemAudit.lastUpdatedDate` all&#39;interno del gruppo di campi [Attributi di controllo del sistema di Source esterni](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) e contattare l&#39;Adobe Technical Account Manager o l&#39;Adobe Customer Care con le informazioni sulla sandbox e sul set di dati.

## Vincoli

Durante questa versione beta privata, quando si utilizza l’ordine con marca temporale del cliente si applicano i seguenti vincoli:

- Puoi utilizzare solo l&#39;ordinamento con marca temporale del cliente con **attributi di profilo** acquisiti con **acquisizione in streaming** nell&#39;archivio profili.
   - **no** sono state fornite garanzie per l&#39;ordinamento dei dati nel data lake o nel servizio Identity.
- Puoi utilizzare l&#39;ordinamento timestamp del cliente solo per le sandbox **non di produzione**.
- È possibile applicare l&#39;ordinamento timestamp cliente solo a **5** set di dati per sandbox.
- **impossibile** utilizzare gli upsert di streaming per inviare aggiornamenti di riga parziali in un set di dati in cui l&#39;ordinamento timestamp del cliente è abilitato.
- Il campo `extSourceSystemAudit.lastUpdatedDate` **deve** essere nel formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). Quando si utilizza il formato ISO 8601, **deve** essere come data/ora completa nel formato `yyyy-MM-ddTHH:mm:ss.sssZ` (ad esempio, `2028-11-13T15:06:49.001Z`).
- Tutte le righe di dati acquisiti **must** contengono il campo `extSourceSystemAudit.lastUpdatedDate` come gruppo di campi di livello principale. Questo significa che il campo **deve** non essere nidificato all&#39;interno dello schema XDM. Se questo campo manca o è in un formato non corretto, il record non valido **non** verrà acquisito e verrà inviato un messaggio di errore corrispondente.
- Qualsiasi set di dati abilitato per l&#39;ordine di marca temporale del cliente **deve** essere un nuovo set di dati senza dati precedentemente acquisiti.
- Per un determinato frammento di profilo, verranno acquisite solo le righe che contengono un `extSourceSystemAudit.lastUpdatedDate` più recente. Le righe che contengono un `extSourceSystemAudit.lastUpdatedDate` più vecchio o della stessa età verranno eliminate.

## Raccomandazioni

Quando implementi l’ordinamento della marca temporale del cliente, tieni presenti le seguenti considerazioni:

- Sei responsabile della sincronizzazione degli orologi su tutti i sistemi interni che inviano dati all’archivio profili.
- La precisione a livello di millisecondi deve essere presente nei timestamp in formato ISO 8061.
