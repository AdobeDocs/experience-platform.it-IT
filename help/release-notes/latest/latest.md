---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Adobe Experience Platform di giugno 2023.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a3faca5e0a711f0d4f6bafb22bf3c4770f58db8e
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 63%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 21 giugno 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Autenticazione per le API di Experience Platform](#authentication-platform-apis)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio query](#query-service)
- [Origini](#sources)

## Autenticazione per le API di Experience Platform {#authentication-platform-apis}

Il metodo per ottenere i token di accesso necessari per l’autenticazione e per effettuare chiamate agli endpoint API è ora semplificato per gli utenti API di Experience Platform. Il metodo JWT per ottenere i token di accesso è obsoleto e sostituito da un metodo di autenticazione server-to-server OAuth più semplice.<p>![Quello evidenziato è il nuovo metodo di autenticazione OAuth per ottenere i token di accesso.](/help/landing/images/api-authentication/oauth-authentication-method.png "Quello evidenziato è il nuovo metodo di autenticazione OAuth per ottenere i token di accesso."){width="100" zoomable="yes"}</p>

Anche se le integrazioni API esistenti che utilizzano il metodo di autenticazione JWT continueranno a funzionare fino al 1° gennaio 2025, Adobe consiglia vivamente di migrare le integrazioni esistenti al nuovo metodo server-to-server OAuth prima di tale data. Leggi la guida sulla [migrazione dalle credenziali dell’account di servizio (JWT) alle credenziali server-to-server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Leggi i [tutorial sull’autenticazione di Experience Platform](/help/landing/api-authentication.md) aggiornati per ulteriori informazioni.

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Estensione | Estensione [!DNL Google Cloud Platform] per l’inoltro degli eventi | L’estensione [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) per l’inoltro degli eventi consente di inoltrare i dati degli eventi a Google per l’attivazione tramite [!DNL Google Pub/Sub]. |
| Estensione | Estensione [!DNL Cloud connector for Google Analytics 4 (ga4)] | L’estensione [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) per l‘’inoltro degli eventi consente di tenere traccia delle analisi tramite il nuovo standard [!DNL Google Analytics 4 (ga4)]. |
| Segreto | Segreto JWT OAuth 2 | Il [Segreto JWT OAuth 2](../../tags/ui/event-forwarding/secrets.md) consente di utilizzare i token di servizio Adobe e [!DNL Google] per supportare le interazioni server-server nell’inoltro degli eventi. |

{style="table-layout:auto"}

Per ulteriori informazioni sulla raccolta dei dati, consulta [panoramica sulla raccolta dati](../../tags/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!BADGE Beta]{type=Informative} [!DNL Amazon Ads] connessione](../../destinations/catalog/advertising/amazon-ads.md) | L’integrazione di [!DNL Amazon Ads] con Adobe Experience Platform ora supporta l’indirizzamento geografico ai vari marketplace di [!DNL Amazon Ads]. Per ulteriori informazioni, consulta [changelog destinazione](../../destinations/catalog/advertising/amazon-ads.md#changelog). |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Supporto di Workspace per le destinazioni di [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md). | Durante la configurazione di una nuova connessione di destinazione di Adobe Target, ora puoi selezionare l’area di lavoro di Adobe Target in cui desideri condividere i tipi di pubblico. Consulta la sezione [parametri di connessione](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) per ulteriori informazioni. Inoltre, consulta il tutorial sulla [configurazione delle aree di lavoro](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=it) in Adobe Target per ulteriori informazioni sulle aree di lavoro. |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Estensione (Prospect-Profile) | [[!UICONTROL Adobe di estensione Unified Profile Service Prospect-Profile Union]](https://github.com/adobe/xdm/pull/1735/files) | Sono stati aggiunti campi obbligatori per lo schema di unione Prospect-Profile. |
| Estensione | [[!UICONTROL Risorsa decisionale]](https://github.com/adobe/xdm/pull/1732/files) | Aggiungi un tipo di dati per rappresentare le risorse utilizzate nelle decisioni. [!UICONTROL Risorsa decisionale] fornisce un riferimento alle risorse utilizzate per eseguire il rendering di `decisionItems`. |
| Tipo di dati | [[!UICONTROL Commercio]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL Commerce] memorizza i record relativi all’attività di acquisto e vendita. |
| Gruppo di campi | [[!UICONTROL Arricchimento partner profilo (esempio)]](https://github.com/adobe/xdm/pull/1747/files) | È stato aggiunto uno schema di esempio per l’arricchimento dei partner di profilo. |
| Gruppo di campi | [[!UICONTROL Dettagli prospect partner (esempio)]](https://github.com/adobe/xdm/pull/1747/files) | È stato aggiunto uno schema di esempio per le estensioni del profilo prospect del fornitore di dati. |
| Tipo di dati | [[!UICONTROL Ambito Commerce]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL Ambito Commerce] identifica dove si è verificato un evento. Ad esempio, nella vista Store, nel negozio, nel sito Web e così via. |
| Tipo di dati | [[!UICONTROL Fatturazione]](https://github.com/adobe/xdm/pull/1734/files) | Le informazioni di fatturazione per uno o più pagamenti sono state aggiunte al [!UICONTROL Commerce] schema. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione aggiornamento |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Dettagli dell’interazione di Media Analytics]](https://github.com/adobe/xdm/pull/1736/files) | Modificato `bitrateAverageBucket` da 100 a &quot;800-899&quot; |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati Qoe]](https://github.com/adobe/xdm/pull/1736/files) | Modificato `bitrateAverageBucket` tipo di dati da stringa. |
| Gruppo di campi | [[!UICONTROL Dettagli sull’iscrizione al segmento]](https://github.com/adobe/xdm/pull/1735/files) | Aggiunto alla classe Prospect Profile. |
| Schema | [[!UICONTROL Schema di sistema per attributi calcolati]](https://github.com/adobe/xdm/pull/1735/files) | Mappa identità aggiunta al [!UICONTROL Schema di sistema per attributi calcolati]. |
| Tipo di dati | [[!UICONTROL Rete di distribuzione dei contenuti]](https://github.com/adobe/xdm/pull/1733/files) | Campo aggiunto a [!UICONTROL Informazioni sui dettagli della sessione] per descrivere la rete di distribuzione dei contenuti utilizzata. |
| Estensione | [[!UICONTROL Adobe di estensione dell’unione degli account del servizio profili unificato]](https://github.com/adobe/xdm/pull/1731/files) | Mappa identità aggiunta al [!UICONTROL Adobe di estensione dell’unione degli account del servizio profili unificato]. |
| Tipo di dati | [[!UICONTROL Ordine]](https://github.com/adobe/xdm/pull/1730/files) | `discountAmount` aggiunto a [!UICONTROL Ordine]. In questo modo viene espressa la differenza tra il prezzo ordinabile e il prezzo speciale. Viene applicato all’intero ordine anziché ai singoli prodotti. |
| Schema | [[!UICONTROL Richiesta operazione di igiene AEP]](https://github.com/adobe/xdm/pull/1728/files) | Il `targetServices` è stato aggiunto il campo per fornire i nomi dei servizi che elaborano le operazioni di igiene dei dati. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/pull/1727/files) | `currencyCode` è stato aggiunto alle informazioni sulla spedizione per uno o più prodotti. È un codice valuta alfabetico ISO 4217 utilizzato per la determinazione del prezzo del prodotto. |
| Tipo di dati | [[!UICONTROL Applicazione]](https://github.com/adobe/xdm/pull/1726/files) | Il `language` è stato aggiunto per fornire all’applicazione le preferenze linguistiche, geografiche o culturali dell’utente. |
| Estensione | [[!UICONTROL Campi entità AJO]](https://github.com/adobe/xdm/pull/1746/files) | [!UICONTROL Entità timestamp AJO] è stato aggiunto per indicare l’ora dell’ultima modifica apportata al messaggio. |
| Tipo di dati | (Multiplo) | [Sono stati rimossi diversi dettagli dei file multimediali](https://github.com/adobe/xdm/pull/1739/files) su diversi tipi di dati per coerenza. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md)

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati nel data lake di Adobe Experience Platform. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modelli in linea | Query Service ora supporta l’utilizzo di modelli che fanno riferimento ad altri modelli all’interno dell’SQL. Riduci il carico di lavoro ed evita errori sfruttando i modelli in linea nelle query. È possibile riutilizzare istruzioni o condizioni e fare riferimento a modelli nidificati per una maggiore flessibilità in SQL. Non esiste alcun limite alle dimensioni delle query che possono essere memorizzate come modelli o al numero di modelli a cui è possibile fare riferimento dalla query originale. Per ulteriori informazioni, leggi la [guida ai modelli in linea](../../query-service/essential-concepts/inline-templates.md). |
| Aggiornamenti pianificati dell’interfaccia utente per le query | Gestisci tutte le query pianificate da un’unica posizione nell’interfaccia utente con [[!UICONTROL Scheda Query pianificate]](../../query-service/ui/monitor-queries.md#inline-actions). L’interfaccia utente [!UICONTROL Query pianificate] è stata migliorata con l’aggiunta di azioni di query in linea e una nuova colonna relativa allo stato della query. Le aggiunte recenti includono la possibilità di abilitare, disabilitare ed eliminare una pianificazione, o di abbonarsi agli avvisi per le esecuzioni delle query imminenti direttamente dalla vista [!UICONTROL Query pianificate]. <p>![Azioni in linea evidenziate nella vista [!UICONTROL Query pianificate].](../../query-service/images/ui/monitor-queries/disable-inline.png "Azioni in linea evidenziate nella vista [!UICONTROL Query pianificate]."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}

Per ulteriori informazioni su Query Service, consulta [Panoramica di Query Service](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione dei flussi di dati di origine della classificazione Adobe Analytics | Ora puoi eliminare i flussi di dati di origine che utilizzano le classificazioni Adobe Analytics come origine. In **[!UICONTROL Origini]** > **[!UICONTROL Flussi di dati]**, seleziona il flusso di dati desiderato, quindi seleziona elimina. Per ulteriori informazioni, consulta la guida sulla [creazione di una connessione di origine per i dati delle classificazioni di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| Supporto del filtro per [!DNL Microsoft Dynamics] tramite API | Utilizza gli operatori logici e di confronto per filtrare i dati a livello di riga per l’origine [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md). Per ulteriori informazioni, consulta la guida su come [filtrare i dati per un’origine tramite API](../../sources/tutorials/api/filter.md). |
| [!BADGE Beta]{type=Informative}[!DNL RainFocus] | Ora puoi utilizzare l’integrazione delle origini [!DNL RainFocus] per portare i dati di gestione degli eventi e di analisi dall’account [!DNL RainFocus] su Experience Platform. Per ulteriori informazioni, leggi la [[!DNL RainFocus] panoramica dell’origine](../../sources/connectors/analytics/rainfocus.md). |
| Supporto per Adobe Commerce | Ora puoi utilizzare l’integrazione delle origini di Adobe Commerce per portare i dati dall’account Adobe Commerce su Experience Platform. Per ulteriori informazioni, leggi la [Panoramica sull’origine di Adobe Commerce](../../sources/connectors/adobe-applications/commerce.md). |
| Supporto per [!DNL Mixpanel] | Ora puoi utilizzare l’integrazione delle origini [!DNL Mixpanel] per importare i dati di analisi dal tuo account [!DNL Mixpanel] su Experience Platform tramite API o dall’interfaccia utente. Per ulteriori informazioni, leggi la [[!DNL Mixpanel] panoramica sull’origine](../../sources/connectors/analytics/mixpanel.md). |
| Supporto per [!DNL Zendesk] | Ora puoi utilizzare l’integrazione delle origini [!DNL Zendesk] per acquisire i dati di successo dei clienti dal tuo account [!DNL Zendesk] su Experience Platform tramite API o dall’interfaccia utente. Per ulteriori informazioni, leggi la [[!DNL Zendesk] panoramica sull’origine](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggi la [panoramica sulle origini](../../sources/home.md).
