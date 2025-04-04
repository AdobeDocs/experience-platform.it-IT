---
title: Note sulla versione di Adobe Experience Platform di novembre 2022
description: Note sulla versione di Adobe Experience Platform di novembre 2022.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 23 novembre 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Estensione [!DNL AWS] per l&#39;inoltro degli eventi | È ora possibile inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL AWS] - Panoramica dell’estensione](../../tags/extensions/server/aws/overview.md). |
| Estensione [!DNL Google Ads Enhanced Conversions] per l&#39;inoltro degli eventi | È ora possibile inviare i dati di conversione a [!DNL Google Ads] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL Google Ads Enhanced Conversions] - Panoramica dell’estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md). |
| Estensione [!DNL Microsoft Azure] per l&#39;inoltro degli eventi | È ora possibile inviare dati a [!DNL Microsoft Azure] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL Microsoft Azure] - Panoramica dell’estensione](../../tags/extensions/server/azure/overview.md). |

Per ulteriori informazioni sulle funzionalità di raccolta dati di Experience Platform, vedi [panoramica sulla raccolta dati](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Assegnare campi alle classi personalizzate quando si aggiunge direttamente a uno schema | Quando [aggiungi un singolo campo direttamente a uno schema](../../xdm/ui/resources/schemas.md#add-individual-fields), in precedenza era possibile assegnare il campo solo a un gruppo di campi come risorsa principale. Ora, oltre ai gruppi di campi, puoi [assegnare il campo a una classe personalizzata](../../xdm/ui/resources/schemas.md#add-to-class) come risorsa principale. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Experience Platform, consulta la [Panoramica del sistema XDM](../../xdm/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi di Experience Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- | 
| Disponibilità Beta dell’origine Oracle Service Cloud | Utilizza l’origine Oracle Service Cloud per acquisire i dati dall’account Oracle Service Cloud ad Experience Platform. Per ulteriori informazioni, consulta la documentazione sull&#39;[origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).
