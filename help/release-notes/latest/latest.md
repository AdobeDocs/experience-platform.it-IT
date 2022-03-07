---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b714a5cf0f4bdf2c0f010664bfef96c5b6641c22
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 7 marzo 2022**

>[!NOTE]
>
>Questa versione è stata spostata dalla data originale del 23 febbraio al 7 marzo.

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [Raccolta dati](#data-collection)
- [[!DNL Identity Service]](#identity)
- [Origini](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più [!DNL dashboards] attraverso cui puoi visualizzare informazioni importanti sui dati della tua organizzazione, come acquisiti durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovi widget per destinazioni standard | I seguenti widget standard consentono di visualizzare diverse metriche correlate alle destinazioni.<ul><li>Segmenti attivati di recente per destinazione. Questo widget visualizza i primi cinque segmenti attivati più di recente in ordine decrescente in base alla destinazione scelta.</li><li>Tendenza della dimensione del pubblico. Questo widget rappresenta la relazione del conteggio del profilo in un periodo di tempo per un segmento mappato a tale account di destinazione.</li><li>Segmenti non mappati per identità. Questo widget elenca i primi cinque segmenti non mappati classificati per numero di identità decrescente per una determinata destinazione e identità.</li><li>Segmenti mappati per identità. Questo widget elenca i primi cinque segmenti mappati. I segmenti sono ordinati da alti a bassi in base ai rispettivi conteggi degli ID sorgente che corrispondono all’ID di destinazione selezionato dal menu a discesa del widget.</li><li>Tipi di pubblico comuni. Questo widget fornisce un elenco dei primi cinque segmenti attivati nell’account di destinazione scelto nella parte superiore della pagina e della destinazione selezionata nel menu a discesa del widget.</li></ul> Per ulteriori informazioni sui widget standard disponibili, consulta la sezione [documentazione del dashboard delle destinazioni.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Per ulteriori informazioni su [!DNL Dashboards], vedi [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network, da cui arricchire, trasformare e distribuire a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Miglioramento del flusso di lavoro dell&#39;interfaccia utente per la configurazione del datastream | Il flusso di lavoro per la creazione di un nuovo datastream nell’interfaccia utente Raccolta dati è stato aggiornato. Quando aggiungi servizi a un datastream, solo i servizi a cui hai accesso verranno inclusi nell’elenco delle opzioni. Consulta la guida su [configurazione di un datastream](../../edge/fundamentals/datastreams.md) per ulteriori informazioni. |
| Preparazione per la raccolta dei dati | Se utilizzi Adobe Experience Platform Web SDK, ora puoi sfruttare le funzionalità di preparazione dei dati per mappare i dati su Experience Data Model (XDM) sul lato server. Vedi la sezione su [Preparazione per la raccolta dei dati](../../edge/fundamentals/datastreams.md#data-prep) nella guida datastreams per ulteriori informazioni. |
| ID dispositivo di prime parti | Ora puoi inviare i tuoi ID dispositivo a Adobe Experience Platform Edge Network quando raccogli i dati dei clienti tramite l’SDK per web di Platform, fornendo una soluzione alle recenti restrizioni del browser per la durata dei cookie di terze parti. Consulta la guida su [ID dispositivo di prime parti](../../edge/identity/first-party-device-ids.md) per ulteriori informazioni. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento delle identità tra dispositivi e sistemi, per offrire in tempo reale esperienze digitali personali di impatto.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova autorizzazione per `view-identity-graph` | Ora puoi utilizzare la `view-identity-graph` autorizzazione per controllare se gli utenti della tua organizzazione sono in grado di visualizzare i dati del grafico delle identità. Agli utenti che non dispongono di questa autorizzazione verrà impedito di accedere al visualizzatore del grafico di identità nell’interfaccia utente o quando accederanno [!DNL Identity Service] API che restituiscono le identità. Consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home.md) per ulteriori informazioni sulle autorizzazioni. |

Per informazioni più generali su [!DNL Identity Service], fare riferimento alla [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
