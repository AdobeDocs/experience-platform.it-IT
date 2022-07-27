---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 93ac391370ddd1fe596b8515bd520fb870a10a3c
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 luglio 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Raccolta dati](#collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)

<!-- - [Real-time Customer Data Platform B2B Edition](#b2b) -->
- [Profilo cliente in tempo reale](#profile)
- [Fonti](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più [!DNL dashboards] attraverso cui puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

### Dashboard dei profili account

Il dashboard Profili account visualizza un&#39;istantanea di informazioni unificate sull&#39;account provenienti da più origini nei diversi canali di marketing e nei diversi sistemi utilizzati dalla tua organizzazione per archiviare le informazioni sull&#39;account cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Account totali per widget di settore | Questo widget visualizza il numero totale di account in una singola metrica e utilizza un grafico ad anello per illustrare le dimensioni proporzionali dei conteggi per i settori che compongono il numero complessivo. |
| Widget aggiunti per profili account | Questo widget utilizza un grafico a barre con codici a colori per illustrare il conteggio dei profili aggiunti a un account in un determinato periodo di tempo e la proporzione di settori diversi che costituiscono tali profili aggiunti. |

{style=&quot;table-layout:auto&quot;}

Consulta la sezione [Panoramica su Real-time CDP, B2B Edition](../../rtcdp/b2b-overview.md) per ulteriori informazioni sulle funzioni B2B disponibili, oppure [esercitazione end-to-end](../../rtcdp/b2b-tutorial.md) Per ulteriori informazioni sulla modalità di creazione dei profili account nell’ambito del flusso di lavoro B2B.

Per ulteriori informazioni sui widget disponibili per visualizzare le metriche relative al profilo del tuo account, consulta la sezione [documentazione dei widget dei profili account](../../dashboards/guides/account-profiles.md#standard-widgets).

### Dashboard di profili

Nel dashboard Profili viene visualizzata un’istantanea dei dati dell’attributo (record) dell’organizzazione all’interno dell’archivio profili in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget Pubblico mappato | Questo widget visualizza il numero totale di tipi di pubblico mappati che possono essere attivati nella destinazione selezionata dal menu a discesa Dashboard Profili . |

Per ulteriori informazioni sul dashboard Profili, consulta la sezione [Panoramica delle dashboard dei profili](../../dashboards/guides/profiles.md).

### Dashboard delle destinazioni

Nel dashboard Destinazioni viene visualizzata un&#39;istantanea delle destinazioni abilitate dall&#39;organizzazione in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget Pubblico | Questo widget fornisce il numero totale di segmenti pronti per essere attivati, in base al criterio di unione scelto applicato ai dati del profilo. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sul dashboard Destinazioni, consulta la sezione [panoramica del dashboard Destinazioni](../../dashboards/guides/destinations.md).

## Raccolta dati {#collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Gestione delle autorizzazioni tramite Adobe Admin Console | L’accesso alle funzionalità di raccolta dati ora è gestito tramite Adobe Admin Console nella scheda per la raccolta dati di Adobe Experience Platform. Consulta la guida su [autorizzazioni per la raccolta dati](../../collection/permissions.md) per ulteriori informazioni.<br><br>Le autorizzazioni per i datastreams vengono ora gestite anche tramite Admin Console sotto la scheda per Adobe Experience Platform, migliorando la sicurezza rispetto al metodo precedente di impostare manualmente queste autorizzazioni per ogni utente. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti apportati a [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations è ora più intelligente e veloce. I nuovi controlli di convalida riducono in modo significativo gli errori di mappatura più comuni, riducendo ulteriormente il time-to-value. |
| Supporto gerarchico per i set di dati in streaming | È ora possibile utilizzare le funzioni `upsert_array_append` e `upsert_array_replace` per aggiornare array e oggetti durante lo streaming degli aggiornamenti a Profilo. Consulta la sezione [[!DNL Data Prep] guida alle funzioni di mappatura](../../data-prep/functions.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| [Esporta file ora (Beta)](../../destinations/ui/export-file-now.md) | Esporta un file completo senza interrompere la pianificazione dell’esportazione corrente di un segmento pianificato in precedenza. Questa esportazione si verifica oltre alle esportazioni pianificate in precedenza e non modifica la frequenza di esportazione del segmento. <br> L’esportazione del file viene attivata immediatamente e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform. <br> <br>Contatta il tuo rappresentante di Adobe per accedere a questa funzionalità. |

{style=&quot;table-layout:auto&quot;}

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [(Beta) [!DNL Trade Desk] - Connessione CRM](../../destinations/catalog/advertising/tradedesk-emails.md) | Utilizzo [!DNL The Trade Desk] Destinazione CRM per attivare profili al tuo [!DNL Trade Desk] account per il targeting e la soppressione del pubblico in base ai dati CRM. <br><br>Questa destinazione è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche. |
| [(Beta) [!DNL Snap Inc.]](../../destinations/catalog/advertising/snap-inc.md) | Questa destinazione consente agli esperti di marketing di importare i segmenti di utenti creati in Experience Platform in Snapchat Ads e di utilizzarli per il targeting dei loro annunci. <br><br>Questa destinazione è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche. |

{style=&quot;table-layout:auto&quot;}

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Modello dati del settore sanitario | È stato introdotto un modello standard di dati sanitari per supportare cinque casi d&#39;uso comuni del settore, relativi all&#39;aumento dell&#39;acquisizione digitale, al miglioramento dell&#39;iscrizione al programma e alla promozione delle informazioni sui farmaci. Vedi la panoramica sul [modello di dati sanitari](../../xdm/schema/industries/healthcare.md) per ulteriori informazioni su questi casi d’uso e sui componenti XDM standard che li supportano.<br><br>È stato aggiunto un nuovo filtro di settore al [!UICONTROL Schemi] Interfaccia utente per l’esplorazione dei componenti relativi all’assistenza sanitaria durante la creazione di schemi personalizzati. |

{style=&quot;table-layout:auto&quot;}

**Nuovi componenti XDM**

>[!WARNING]
>
>I nuovi componenti XDM elencati nella tabella seguente sono sperimentali e attualmente in fase di test. Questi componenti devono essere aggiornati con le modifiche di interruzione (se necessarie) prima che siano stabilizzati. Pianifica di conseguenza i tuoi sforzi di sviluppo.

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Tempo]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | Classe basata su record utilizzata per l&#39;acquisizione dei dati meteo. |
| Gruppo di campi | [[!UICONTROL Tempo attuale]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] e [!UICONTROL Tempo] classi, utilizzate per acquisire le condizioni meteorologiche correnti per un codice postale. |
| Gruppo di campi | [[!UICONTROL Tempo previsto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] e [!UICONTROL Tempo] classi, utilizzate per acquisire le condizioni meteorologiche previste per un codice postale. |
| Gruppo di campi | [[!UICONTROL Trigger dei prodotti]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] e [!UICONTROL Tempo] , utilizzato per acquisire trigger specifici del prodotto che sfruttano le condizioni meteorologiche note per determinare il comportamento del consumatore. |
| Gruppo di campi | [[!UICONTROL Trigger relativi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] e [!UICONTROL Tempo] classi, utilizzate per acquisire trigger relativi che sfruttano le condizioni meteorologiche note per determinare il comportamento dei consumatori. |
| Gruppo di campi | [[!UICONTROL Trigger severi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] e [!UICONTROL Tempo] classi, utilizzate per l&#39;acquisizione di trigger che sfruttano gravi condizioni meteorologiche note per determinare il comportamento dei consumatori. |
| Gruppo di campi | [[!UICONTROL Trigger del tempo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/weather-triggers.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] e [!UICONTROL Tempo] classi, utilizzate per acquisire trigger generali che sfruttano le condizioni meteorologiche note per determinare il comportamento dei consumatori. |
| Gruppo di campi | [[!UICONTROL Dettagli interazione MediaCollection]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-collection.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] classe che acquisisce i dettagli relativi a un&#39;interazione multimediale. |
| Gruppo di campi | [[!UICONTROL Dettagli interazione MediaReporting]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-reporting.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] che acquisisce i dettagli relativi a un&#39;interazione con il reporting multimediale. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli pubblicitari]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Acquisisce i dettagli di una risorsa pubblicitaria. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli del contenitore pubblicitario]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json) | Acquisisce i dettagli su un pod pubblicitario, che è una sequenza di più annunci riprodotti all’interno di una singola interruzione pubblicitaria. |
| Tipo di dati | [[!UICONTROL Informazioni dettagliate del capitolo]](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json) | Acquisisce i dettagli di un capitolo o segmento in un contenuto video. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli degli errori]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Acquisisce i dettagli relativi a un errore di riproduzione video. |
| Tipo di dati | [[!UICONTROL Informazioni sull&#39;evento del lettore]](https://github.com/adobe/xdm/blob/master/components/datatypes/playereventdetails.schema.json) | Acquisisce i dettagli relativi all’evento su un lettore video, inclusa la posizione del playhead e l’ID della sessione. |
| Tipo di dati | [[!UICONTROL Informazioni sullo stato del lettore]](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json) | Acquisisce i dettagli relativi allo stato di un lettore video. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati QE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Acquisisce i dettagli di qualità dell’esperienza (QoE) su un evento di riproduzione video. |
| Tipo di dati | [[!UICONTROL Informazioni sulla sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Acquisisce i dettagli della sessione su un evento di riproduzione video. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

<!-- ## Real-time Customer Data Platform B2B Edition {#b2b}

Built on Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition is purpose-built for marketers operating in a business-to-business service model. It brings together data from multiple sources and combines it into a single view of people and account profiles. This unified data allows marketers to precisely target specific audiences and engage those audiences across all available channels.

| Feature | Description |
| Lead to account matching | Lead to account matching allows you to use Real-time CDP B2B edition to match known person profiles to account profiles so that these profiles can be segmented and targeted with B2B context data like account, opportunity (and add something else like don't use etc. to the description). For more information, see the document on [lead to account matching](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md). For a guide on how to monitor profile enrichment, see the document on [monitoring profile enrichment in the UI](../../dataflows/ui/b2b/monitor-profile-enrichment.md). For instructions on how to use related accounts in segment definitions, see the guide on [Segmentation use cases for Real-time Customer Data Platform B2B Edition](../../rtcdp/segmentation/b2b.md#related-accounts)."|

{style="table-layout:auto"}

To learn more about Real-time CDP B2B Edition, see the [Real-time CDP B2B overview](../../rtcdp/overview.md). -->

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Pulizia degli attributi edge del profilo orfano (versione limitata) | Se l’organizzazione dispone dell’accesso a questa funzione, ora il servizio di profilo rimuove quotidianamente gli attributi edge residui dell’area di attività dell’utente per fornire una rappresentazione più accurata dei profili nel sistema. Questa pulizia si verifica dopo l’eliminazione di tutti i frammenti di profilo per un determinato profilo e dovrebbe influenzare i profili che vengono uniti dai set di dati in cui `com_adobe_aep_profile_region_dataset` è contrassegnato come true. Questo può mostrare un calo nella metrica &quot;Pubblico di riferimento&quot; nel dashboard dell’utilizzo della licenza e può mostrare un calo nella metrica &quot;Conteggio profili&quot; nel dashboard del profilo, poiché queste metriche includevano frammenti di attributi di margine residuo prima di questa versione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sul Profilo del cliente in tempo reale, compresi tutorial e best practice per l’utilizzo dei dati del profilo, consulta la sezione [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale [!DNL Azure Data Explorer] source | Utilizza l’origine di Data Explorer di Azure per estrarre i dati dal tuo [!DNL Azure] Experience Platform. Consulta la sezione [[!DNL Azure Data Explorer] panoramica di origine](../../sources/connectors/databases/data-explorer.md) per ulteriori informazioni. |
| Disponibilità generale [!DNL Generic OData] source | Utilizza la [!DNL Generic OData] origine per portare ad Experience Platform le risorse dei sistemi che supportano il protocollo open data. Consulta la sezione [[!DNL Generic OData] panoramica di origine](../../sources/connectors/protocols/odata.md) per ulteriori informazioni. |
| Supporto per il rilevamento automatico delle proprietà del file sorgente per [!DNL Data Landing Zone] nell’interfaccia utente di Experience Platform | La [!DNL Data Landing Zone] ora supporta il rilevamento automatico delle proprietà del file quando si utilizza l’interfaccia utente di Experience Platform. Consulta la documentazione su [creazione di un [!DNL Data Landing Zone] connessione sorgente](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
