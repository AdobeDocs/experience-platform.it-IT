---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di giugno 2023 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a03d0eeab5ca42225705fdeab692020b1641395d
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 21 giugno 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Autenticazione per le API Experience Platform](#authentication-platform-apis)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Servizio query](#query-service)
- [Origini](#sources)

## Autenticazione per le API Experience Platform {#authentication-platform-apis}

Ad Experience Platform, per gli utenti API, ora è semplificato il metodo per ottenere i token di accesso necessari per l’autenticazione e per effettuare chiamate agli endpoint API. Il metodo JWT per ottenere i token di accesso è obsoleto e sostituito da un metodo di autenticazione server-to-server OAuth più semplice.<p>![È stato evidenziato il nuovo metodo di autenticazione OAuth per ottenere i token di accesso.](/help/landing/images/api-authentication/oauth-authentication-method.png "È stato evidenziato il nuovo metodo di autenticazione OAuth per ottenere i token di accesso."){width="100" zoomable="yes"}</p>

Anche se le integrazioni API esistenti che utilizzano il metodo di autenticazione JWT continueranno a funzionare fino al 1° gennaio 2025, Adobe consiglia vivamente di migrare le integrazioni esistenti al nuovo metodo server-to-server OAuth prima di tale data. Leggi la guida su [migrazione dalle credenziali dell’account di servizio (JWT) alle credenziali server-to-server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Leggi gli aggiornamenti [tutorial sull’autenticazione di Experience Platform](/help/landing/api-authentication.md) per ulteriori informazioni.

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Estensione  | [!DNL Google Cloud Platform] estensione di inoltro eventi | Il [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) l’estensione per l’inoltro degli eventi consente di inoltrare i dati degli eventi a Google per l’attivazione tramite [!DNL Google Pub/Sub]. |
| Estensione  | [!DNL Cloud connector for Google Analytics 4 (ga4)] Estensione | Il [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) l’estensione di inoltro degli eventi consente di tenere traccia di analytics tramite il nuovo [!DNL Google Analytics 4 (ga4)] standard. |
| Segreto | Segreto JWT OAuth 2 | Il [Segreto JWT OAuth 2](../../tags/ui/event-forwarding/secrets.md) consente di utilizzare Adobe e [!DNL Google] Token di servizio per supportare le interazioni server-server nell’inoltro degli eventi. |
| Tag e inoltro eventi | Attribuzione utente | L’attribuzione degli utenti fornisce dati chiave sulle attività in [Tag](../../tags/home.md) e [Inoltro eventi](../../tags/ui/event-forwarding/overview.md) UI.<br><br>I dati includono chi ha apportato modifiche e in che momento. Questi dati sono visibili nell’interfaccia utente di Tag ed Inoltro eventi nelle seguenti schermate:<br><ul><li> Panoramica delle proprietà</li><li> Estensioni installate</li><li>Confronto e revisione delle regole</li><li>Revisione del confronto degli elementi dati</li><li>Revisione del confronto delle estensioni</li><li>Modifiche alle risorse della libreria</li><li>Ultima build e pubblicazione della libreria</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni sulla raccolta dei dati, consulta [panoramica sulla raccolta dati](../../tags/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!BADGE Beta]{type=Informative} [!DNL Amazon Ads] connessione](../../destinations/catalog/advertising/amazon-ads.md) | Il [!DNL Amazon Ads] L&#39;integrazione con Adobe Experience Platform ora supporta il routing regionale ai vari [!DNL Amazon Ads] marketplace. Per ulteriori informazioni, consulta [changelog di destinazione](../../destinations/catalog/advertising/amazon-ads.md#changelog). |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Supporto di Workspace per [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) destinazioni. | Durante la configurazione di una nuova connessione di destinazione di Adobe Target, ora puoi selezionare l’area di lavoro di Adobe Target in cui desideri condividere i tipi di pubblico. Consulta la [parametri di connessione](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) per ulteriori informazioni. Inoltre, consulta l’esercitazione su [configurazione delle aree di lavoro](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) in Adobe Target per ulteriori informazioni sulle aree di lavoro. |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati nel data lake di Adobe Experience Platform. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire in Real-Time Customer Profile. &#x200B;
**Funzioni aggiornate**
&#x200B; | Funzione | Descrizione | | — | — | | &#x200B;Modelli in linea | Query Service ora supporta l’utilizzo di modelli che fanno riferimento ad altri modelli all’interno dell’SQL. Riduci il carico di lavoro ed evita errori sfruttando i modelli in linea nelle query. È possibile riutilizzare istruzioni o condizioni e fare riferimento a modelli nidificati per una maggiore flessibilità nell&#39;SQL. Non esiste alcun limite nelle dimensioni delle query che possono essere memorizzate come modelli o nel numero di modelli a cui è possibile fare riferimento dalla query originale. Per ulteriori informazioni, leggere [guida ai modelli in linea](../../query-service/essential-concepts/inline-templates.md). | | Aggiornamenti pianificati dell’interfaccia utente query | Gestisci tutte le query pianificate da un’unica posizione nell’interfaccia utente con [[!UICONTROL Scheda Query pianificate]](../../query-service/ui/monitor-queries.md#inline-actions). Il [!UICONTROL Query pianificate] L’interfaccia utente è stata migliorata con l’aggiunta di azioni di query in linea e la nuova colonna relativa allo stato della query. Le aggiunte recenti includono la possibilità di abilitare, disabilitare ed eliminare una pianificazione, o di abbonarsi agli avvisi per le esecuzioni delle query imminenti direttamente dal [!UICONTROL Query pianificate] visualizzazione. <p>![Azioni in linea evidenziate nel [!UICONTROL Query pianificate] visualizzazione.](../../query-service/images/ui/monitor-queries/disable-inline.png "Azioni in linea evidenziate nel [!UICONTROL Query pianificate] visualizzazione."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
&#x200B; Per ulteriori informazioni su Query Service, consulta [Panoramica di Query Service](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione dei flussi di dati di origine della classificazione Adobe Analytics | Ora puoi eliminare i flussi di dati di origine che utilizzano le classificazioni Adobe Analytics come origine. Sotto **[!UICONTROL Sorgenti]** > **[!UICONTROL Flussi dati]**, seleziona il flusso di dati desiderato, quindi seleziona elimina. Per ulteriori informazioni, consulta la guida su [creazione di una connessione di origine per i dati delle classificazioni di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| Supporto del filtro per [!DNL Microsoft Dynamics] utilizzo dell’API | Utilizzare gli operatori logici e di confronto per filtrare i dati a livello di riga per [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) sorgente. Per ulteriori informazioni, consulta la guida su [filtrare i dati per un’origine utilizzando l’API](../../sources/tutorials/api/filter.md). |
| [!BADGE Beta]{type=Informative}[!DNL RainFocus] | Ora puoi utilizzare la [!DNL RainFocus] integrazione delle origini per acquisire i dati di gestione degli eventi e analisi dalle [!DNL RainFocus] da Experience Platform. Per ulteriori informazioni, leggere [[!DNL RainFocus] panoramica dell’origine](../../sources/connectors/analytics/rainfocus.md). |
| Supporto per Adobe Commerce | Ora puoi utilizzare l’integrazione delle origini di Adobe Commerce per portare i dati dall’account Adobe Commerce all’Experience Platform. Per ulteriori informazioni, leggere [Panoramica sull’origine di Adobe Commerce](../../sources/connectors/adobe-applications/commerce.md). |
| Supporto per [!DNL Mixpanel] | Ora puoi utilizzare la [!DNL Mixpanel] integrazione delle origini per importare i dati di analytics dalle [!DNL Mixpanel] da Experience Platform tramite API o l’interfaccia utente. Per ulteriori informazioni, leggere [[!DNL Mixpanel] panoramica dell’origine](../../sources/connectors/analytics/mixpanel.md). |
| Supporto per [!DNL Zendesk] | Ora puoi utilizzare la [!DNL Zendesk] integrazione di sorgenti per acquisire i dati di successo dei clienti dalle [!DNL Zendesk] da Experience Platform tramite API o l’interfaccia utente. Per ulteriori informazioni, leggere [[!DNL Zendesk] panoramica dell’origine](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).
