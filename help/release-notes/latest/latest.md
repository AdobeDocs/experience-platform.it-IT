---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: aabf715475b3634ef134226f67b722f84e830556
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 9%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 23 novembre 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!DNL AWS] estensione per l&#39;inoltro eventi | Ora puoi inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL AWS] panoramica dell&#39;estensione](../../tags/extensions/server/aws/overview.md) per ulteriori informazioni. |
| [!DNL Google Ads Enhanced Conversions] estensione per l&#39;inoltro eventi | Ora puoi inviare i dati di conversione a [!DNL Google Ads] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Google Ads Enhanced Conversions] panoramica dell&#39;estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per ulteriori informazioni. |
| [!DNL Microsoft Azure] estensione per l&#39;inoltro eventi | Ora puoi inviare dati a [!DNL Microsoft Azure] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Microsoft Azure] panoramica dell&#39;estensione](../../tags/extensions/server/azure/overview.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle funzionalità di raccolta dati di Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Assegnare campi alle classi personalizzate quando si aggiunge direttamente a uno schema | Quando [aggiunta di un singolo campo direttamente a uno schema](../../xdm/ui/resources/schemas.md#add-individual-fields), in precedenza era possibile assegnare il campo solo a un gruppo di campi come risorsa principale. Ora, oltre ai gruppi di campi, è possibile [assegna il campo a una classe personalizzata](../../xdm/ui/resources/schemas.md#add-to-class) come risorsa principale. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- | 
| Disponibilità beta dell’origine Oracle Service Cloud | Utilizza l’origine Oracle Service Cloud per acquisire i dati dall’account Oracle Service Cloud all’Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [Origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
