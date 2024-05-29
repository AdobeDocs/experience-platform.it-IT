---
title: Ordinazione marca temporale cliente
description: Scopri come aggiungere l’ordine delle marche temporali dei clienti ai set di dati per garantire la coerenza dei dati del profilo.
badgePrivateBeta: label="Versione beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Ordine timestamp cliente

In Adobe Experience Platform, l’ordine dei dati non è garantito automaticamente al momento dell’acquisizione dei dati tramite acquisizione in streaming nell’archivio profili. Con l’ordine della marca temporale del cliente, puoi garantire che l’ultimo messaggio, in base alla marca temporale del cliente fornita, verrà mantenuto nell’archivio profili. Tutti i messaggi non aggiornati verranno quindi eliminati e **non** essere disponibile per l’utilizzo in servizi a valle che utilizzano dati di profilo come segmentazione e destinazioni. Di conseguenza, questo consente ai dati del profilo di essere coerenti e di rimanere sincronizzati con i sistemi di origine.

Per abilitare l’ordinamento delle marche temporali dei clienti, utilizza `extSourceSystemAudit.lastUpdatedDate` campo all&#39;interno del [Tipo di dati Attributi di controllo del sistema di sorgente esterna](../xdm/data-types/external-source-system-audit-attributes.md) e contatta il tuo Adobe Technical Account Manager o Adobe Customer Care con le informazioni sulla sandbox e sui set di dati.

## Vincoli

Durante questa versione beta privata, quando si utilizza l’ordine con marca temporale del cliente si applicano i seguenti vincoli:

- È possibile utilizzare l’ordinamento delle marche temporali dei clienti solo con **attributi profilo** acquisito con **acquisizione in streaming** nell’archivio Profili.
   - Ci sono **no** ordinare garanzie fornite per i dati nel data lake o nel servizio Identity.
- Puoi utilizzare l’ordinamento con marca temporale del cliente solo il **non produzione** sandbox.
- Puoi applicare l’ordine di marca temporale del cliente solo a **5** set di dati per sandbox.
- Tu **non può** utilizza gli aggiornamenti streaming per inviare aggiornamenti parziali delle righe in un set di dati in cui è abilitato l’ordinamento delle marche temporali dei clienti.
- Il `extSourceSystemAudit.lastUpdatedDate` campo **deve** essere nel [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato. Quando si utilizza il formato ISO 8601, **deve** essere come data/ora completa nel formato `yyyy-MM-ddTHH:mm:ss.sssZ` (ad esempio, `2028-11-13T15:06:49.001Z`).
- Tutte le righe di dati acquisite **deve** contengono `extSourceSystemAudit.lastUpdatedDate` come gruppo di campi di livello superiore. Questo significa che questo campo **deve** non essere nidificato all’interno dello schema XDM. Se questo campo è mancante o in un formato non corretto, il record non valido **non** vengono acquisiti e viene inviato un messaggio di errore corrispondente.
- Qualsiasi set di dati abilitato per l’ordine delle marche temporali dei clienti **deve** essere un nuovo set di dati senza dati precedentemente acquisiti.
- Per un dato frammento di profilo, solo le righe che contengono una più recente `extSourceSystemAudit.lastUpdatedDate` verranno acquisiti. Se la riga non contiene un elemento più recente `extSourceSystemAudit.lastUpdatedDate`, la riga verrà eliminata.

## Consigli

Quando implementi l’ordinamento della marca temporale del cliente, tieni presenti le seguenti considerazioni:

- Sei responsabile della sincronizzazione degli orologi su tutti i sistemi interni che inviano dati all’archivio profili.
- La precisione a livello di millisecondi deve essere presente nei timestamp in formato ISO 8061.
