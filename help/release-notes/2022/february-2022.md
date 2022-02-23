---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 07dc417cbeb5ac0a59d2405986e9bb771b0735f2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 8%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 23 febbraio 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network, da cui arricchire, trasformare e distribuire a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Miglioramento del flusso di lavoro dell&#39;interfaccia utente per la configurazione del datastream | Il flusso di lavoro per la creazione di un nuovo datastream nell’interfaccia utente Raccolta dati è stato aggiornato. Quando aggiungi servizi a un datastream, solo i servizi a cui hai accesso verranno inclusi nell’elenco delle opzioni. Consulta la guida su [configurazione di un datastream](../../edge/fundamentals/datastreams.md) per ulteriori informazioni. |
| Preparazione per la raccolta dei dati | Se utilizzi Adobe Experience Platform Web SDK, ora puoi sfruttare le funzionalità di preparazione dei dati per mappare i dati su Experience Data Model (XDM) sul lato server. Vedi la sezione su [Preparazione per la raccolta dei dati](../../edge/fundamentals/datastreams.md#data-prep) nella guida datastreams per ulteriori informazioni. |
| ID dispositivo di prime parti | Ora puoi inviare i tuoi ID dispositivo a Adobe Experience Platform Edge Network quando raccogli i dati dei clienti tramite l’SDK per web di Platform, fornendo una soluzione alle recenti restrizioni del browser per la durata dei cookie di terze parti. Consulta la guida su [ID dispositivo di prime parti](../../edge/identity/first-party-device-ids.md) per ulteriori informazioni. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).


## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Data Prep] supporto per il connettore sorgente Adobe Analytics | Il connettore di origine Adobe Analytics supporta ora le funzioni di preparazione dei dati, che consentono di mappare i dati della suite di rapporti di Analytics su uno schema XDM di destinazione durante la creazione di un flusso di dati. Guarda l’esercitazione su [creazione di un connettore sorgente Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento delle identità tra dispositivi e sistemi, per offrire in tempo reale esperienze digitali personali di impatto.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Nuova autorizzazione per `view-identity-graph` | Ora puoi utilizzare la `view-identity-graph` autorizzazione per controllare se gli utenti della tua organizzazione sono in grado di visualizzare i dati del grafico delle identità. Agli utenti che non dispongono di questa autorizzazione verrà impedito di accedere al visualizzatore del grafico di identità nell’interfaccia utente o quando accederanno [!DNL Identity Service] API che restituiscono le identità. Consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home.md) per ulteriori informazioni sulle autorizzazioni. |

Per informazioni più generali su [!DNL Identity Service], fare riferimento alla [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
