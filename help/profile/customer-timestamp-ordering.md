---
title: Ordinazione marca temporale cliente
description: Scopri come aggiungere l’ordine delle marche temporali dei clienti ai set di dati per garantire la coerenza dei dati del profilo.
badgePrivateBeta: label="Versione beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Ordine timestamp cliente

In Adobe Experience Platform, l’ordine dei dati non è garantito automaticamente al momento dell’acquisizione dei dati tramite acquisizione in streaming nell’archivio dei profili. Con l’ordine della marca temporale del cliente, puoi garantire che l’ultimo messaggio, in base alla marca temporale del cliente fornita, verrà mantenuto nell’archivio profili. Di conseguenza, questo consente ai dati del profilo di essere coerenti e di rimanere sincronizzati con i sistemi di origine.

Per abilitare l’ordinamento delle marche temporali dei clienti, è necessario utilizzare `lastUpdatedDate` campo all&#39;interno del [Tipo di dati Attributi di controllo del sistema di sorgente esterna](../xdm/data-types/external-source-system-audit-attributes.md) e contatta il tuo Adobe Technical Account Manager o Adobe Customer Care con le informazioni sulla sandbox e sui set di dati.

## Vincoli

Durante questa versione beta privata, quando si utilizza l’ordine con marca temporale del cliente si applicano i seguenti vincoli:

- È possibile utilizzare l’ordinamento delle marche temporali dei clienti solo con **attributi profilo** acquisito con **acquisizione in streaming**.
- Puoi utilizzare l’ordinamento con marca temporale del cliente solo il **non produzione** sandbox.
- Puoi applicare l’ordine di marca temporale del cliente solo a **5** set di dati per sandbox.
- Il `lastUpdatedDate` il campo deve essere nel [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato.
- Tutte le righe di dati acquisite **deve** contengono `lastUpdatedDate` campo. Se questo campo manca o è in un formato errato, l’acquisizione non riuscirà.
- Qualsiasi set di dati abilitato per l’ordine delle marche temporali dei clienti **deve** essere un nuovo set di dati senza dati precedentemente acquisiti.
- Per un dato frammento di profilo, solo le righe che contengono una più recente `lastUpdatedDate` verranno acquisiti. Se la riga non contiene un elemento più recente `lastUpdatedDate`, la riga verrà eliminata.

## Consigli

Quando implementi l’ordinamento della marca temporale del cliente, tieni presenti le seguenti considerazioni:

- È tua responsabilità sincronizzare gli orologi su tutti i sistemi interni che inviano dati all’archivio dei profili.
- La precisione a livello di millisecondi deve essere presente nei timestamp in formato ISO 8061.
- L’utilizzo della preparazione dati in coordinamento con l’ordinamento delle marche temporali del cliente è **altamente consigliato**, crea una copia di tutte le righe acquisite con i relativi timestamp, che consente un debug migliore in caso di problemi.
