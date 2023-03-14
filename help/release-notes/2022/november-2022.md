---
title: Note sulla versione di Adobe Experience Platform, novembre 2022
description: Note sulla versione di novembre 2022 per Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 23 novembre 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!DNL AWS] estensione per l’inoltro di eventi | Ora puoi inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL AWS] panoramica dell’estensione](../../tags/extensions/server/aws/overview.md) per ulteriori informazioni. |
| [!DNL Google Ads Enhanced Conversions] estensione per l’inoltro di eventi | Ora puoi inviare i dati di conversione a [!DNL Google Ads] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Google Ads Enhanced Conversions] panoramica dell’estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per ulteriori informazioni. |
| [!DNL Microsoft Azure] estensione per l’inoltro di eventi | Ora puoi inviare dati a [!DNL Microsoft Azure] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Microsoft Azure] panoramica dell’estensione](../../tags/extensions/server/azure/overview.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle funzionalità di raccolta dati di Platform, consulta [panoramica sulla raccolta dati](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Assegnare campi alle classi personalizzate quando si aggiunge direttamente a uno schema | Quando [aggiunta diretta di un singolo campo a uno schema](../../xdm/ui/resources/schemas.md#add-individual-fields), in precedenza era possibile assegnare il campo solo a un gruppo di campi come risorsa principale. Ora, oltre ai gruppi di campi, puoi [assegnare il campo a una classe personalizzata](../../xdm/ui/resources/schemas.md#add-to-class) come risorsa principale. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- | 
| Disponibilità beta dell’origine Oracle Service Cloud | Utilizza l’origine Oracle Service Cloud per acquisire i dati dall’account Oracle Service Cloud all’Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [Origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).
