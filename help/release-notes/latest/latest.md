---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '1794'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 22 giugno 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio query](#query-service)
- [Connessioni Real-time Customer Data Platform](#data-collection)
- [Origini](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per scatenare insights dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni Adobe. Uno dei modi in cui Data Science Workspace ottiene questo risultato è attraverso l&#39;uso di JupyterLab. JupyterLab è un&#39;interfaccia utente basata sul Web per <a href="https://jupyter.org/" target="_blank">Jupyter del progetto</a> ed è strettamente integrato in Adobe Experience Platform. Offre agli scienziati dei dati un ambiente di sviluppo interattivo per lavorare con notebook, codice e dati Jupyter.

| Funzione | Descrizione |
| --- | --- |
| JupyterLab Launcher | JupyterLab Launcher ora include avviatori per i notebook Spark 3.2. Gli avviatori per notebook Spark 2.4 vengono ora sostituiti dai notebook Spark 3.2 e faranno parte di questa versione. |
| Spark 3.2 | Le nuove ricette Scala (Spark) e PySpark ora utilizzano Spark 3.2 |
| Kernel | I notebook Scala (Spark) vengono ora creati tramite il kernel Scala. I notebook PySpark sono ora creati tramite il Kernel Python. Il kernel Spark e PySpark sono obsoleti e sono impostati per essere rimossi in una versione successiva. |
| Ricette | Le nuove ricette PySpark e Spark ora seguono il flusso di lavoro Docker simile alle ricette Python e R. |

{style=&quot;table-layout:auto&quot;}

Per informazioni più generali su Data Science Workspace, consulta la sezione [documentazione panoramica](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto Destination SDK per [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) destinazioni basate su file e [nomi di file configurabili](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | È ora possibile utilizzare la Destination SDK per creare le destinazioni di Google Cloud Storage e definire nomi di file personalizzati per i file esportati tramite macro di nomi di file. <br><br> Il supporto per la destinazione basata su file in Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche. |
| La colonna Segmento nel flusso di dati viene eseguita su destinazioni batch | Per il flusso di dati che viene eseguito su destinazioni batch, l’interfaccia utente visualizza ora il nome del segmento associato a ogni esecuzione del flusso di dati. Ulteriori informazioni [il flusso di dati viene eseguito su destinazioni batch](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | La [!DNL Google Ad Manager 360] la connessione abilita il caricamento batch per [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], tramite [!DNL Google Cloud Storage] <br><br>Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso al [!DNL Google Ad Manager 360] contatta il tuo rappresentante di Adobe e fornisci [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Attiva profili per sondaggi Medallia mirati e raccolta di feedback per comprendere meglio le esigenze e le aspettative dei clienti. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) la destinazione ti consente di condividere segmenti di prime parti autenticati con inserzionisti approvati e gli utenti per l’attivazione della campagna con DSP. |

{style=&quot;table-layout:auto&quot;}

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Medicina]](https://github.com/adobe/xdm/blob/master/components/classes/medication.schema.json) | Una classe di settore sanitario che cattura i dettagli su una sostanza usata per il trattamento medico, in particolare un farmaco o. |
| Classe | [[!UICONTROL Pianificare]](https://github.com/adobe/xdm/blob/master/components/classes/plan.schema.json) | Classe di settore sanitario che acquisisce i dettagli su un piano medico, ad esempio un piano sanitario o un piano assicurativo. |
| Classe | [[!UICONTROL Provider]](https://github.com/adobe/xdm/blob/master/components/classes/provider.schema.json) | Una classe di settore sanitario che cattura i dettagli di un fornitore di assistenza sanitaria. |
| Classe | [[!UICONTROL Pagatore]](https://github.com/adobe/xdm/blob/master/components/classes/payer.schema.json) | Una classe di settore sanitario che cattura i dettagli di una compagnia assicurativa. |
| Classe | [[!UICONTROL Pianificazione eventi live]](https://github.com/adobe/xdm/blob/master/components/classes/live-event-schedule.json) | Una classe di settore dello sport e dell&#39;intrattenimento che acquisisce i dettagli di un programma di eventi live, come un programma di concerti itineranti o un programma della squadra sportiva. |
| Classe | [[!UICONTROL Posizione ]](https://github.com/adobe/xdm/blob/master/components/classes/location.json) | Una classe di settore dello sport e dell&#39;intrattenimento che cattura la posizione di un evento live, come una sala concerti o un&#39;arena sportiva. |
| Gruppo di campi | [[!UICONTROL Medicina sanitaria]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json) | Un gruppo di campi per [!UICONTROL Medicina] classe che acquisisce i dettagli sul farmaco come nome del marchio, numero di lotto e quantità. |
| Gruppo di campi | [[!UICONTROL Dettagli sul piano sanitario]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/plan/healthcare-plan-details.schema.json) | Un gruppo di campi per [!UICONTROL Pianificare] classe che acquisisce dettagli quali rete, tipo e stato attivo. |
| Gruppo di campi | [[!UICONTROL Fornitore sanitario]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Un gruppo di campi per [!UICONTROL Provider] classe che acquisisce i dettagli di un singolo professionista sanitario o di un&#39;organizzazione di una struttura sanitaria autorizzata a fornire servizi di diagnosi e trattamento sanitari. |
| Gruppo di campi | [[!UICONTROL Dettagli dei membri del settore sanitario]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Un gruppo di campi per [!UICONTROL Profilo individuale XDM] classe che acquisisce i dettagli di una persona che ha o riceverà un servizio o un&#39;assistenza, ad esempio informazioni di contatto, medico primario e informazioni di piano. |
| Gruppo di campi | [[!UICONTROL Dettagli Sitetool]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] classe che acquisisce le informazioni raccolte da sitetools come chatbot, survey e così via. |
| Gruppo di campi | [[!UICONTROL Acquisto ticket evento live]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-live-event-ticket-purchase.json) | Un gruppo di campi per [!UICONTROL ExperienceEvent XDM] classe che acquisisce la cronologia degli acquisti per i biglietti per un evento live, ad esempio un concerto o una partita sportiva. |
| Gruppo di campi | [[!UICONTROL Programma eventi sportivi e di intrattenimento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/live-event-schedule/sports-entertainment-event-schedule.schema.json) | Un gruppo di campi per [!UICONTROL Pianificazione eventi live] classe che acquisisce ulteriori dettagli sulla pianificazione, come il nome dell&#39;attrazione, gli orari di apertura della porta e altro ancora. |
| Gruppo di campi | [[!UICONTROL Evento di intrattenimento sportivo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/location/sports-entertainment-event-venue.schema.json) | Un gruppo di campi per [!UICONTROL Posizione] classe che acquisisce ulteriori dettagli sulla sede dell&#39;evento, come la capacità di seduta e le aree di mercato designate (DMA). |
| Schema globale | (Diversi) | Sono disponibili nuovi schemi globali per le metriche delle destinazioni per RTCDP Insights. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1560) per ulteriori dettagli. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione aggiornamento |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Schema della serie temporale]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | È stato aggiunto un tipo di evento di aggiornamento degli stati multimediali. |
| Gruppo di campi | [[!UICONTROL Riserva]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json) | È stata aggiunta la proprietà relativa al pagamento di un alloggio. |
| Tipo di dati | [[!UICONTROL Informazioni multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Sono stati aggiunti i campi stati-start e stati-end . |
| Estensione  | [[!UICONTROL Evento di modifica Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Sono stati aggiunti due campi utilizzati per memorizzare gli attributi per identificare l’utente e l’ora di un evento di creazione. |
| Estensione  | [[!UICONTROL Adobe CJM ExperienceEvent - Dettagli interazione messaggio]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/message-interaction.schema.json) | Sono state aggiunte informazioni su abbonamento, consenso, e-mail personalizzata e dati aggiuntivi nell’oggetto della pagina di destinazione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Etichettatura dello schema ad hoc | Gestisci l’accesso ai dati sensibili applicando etichette ai campi di dati di schemi ad hoc generati automaticamente tramite query CTAS del servizio query. Puoi limitare l’utilizzo di determinati campi, o set di dati, di schemi ad hoc per controllare l’accesso sia a dati personali sensibili che a informazioni personali identificabili. Utilizzando la funzionalità di controllo degli accessi basata sugli attributi, puoi assegnare etichette ai campi dello schema ad hoc tramite l’interfaccia utente di Platform. |
| `FLATTEN` impostazione | Quando ci si connette a un database tramite strumenti BI di terze parti, il `FLATTEN` l’impostazione appiattisce le strutture di dati nidificate in colonne separate in cui il nome dell’attributo diventa il nome della colonna contenente i valori della riga. Questo migliora l’usabilità degli schemi ad hoc e riduce il carico di lavoro necessario per recuperare, analizzare, trasformare e creare rapporti sui dati in strumenti BI che non supportano strutture di dati nidificate. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui servizi di query, consulta la [Panoramica del servizio query](../../query-service/home.md).

## Connessioni Real-time Customer Data Platform {#data-collection}

Real-time Customer Data Platform Connections fornisce una suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network in modo da poter essere arricchiti, trasformati e distribuiti su destinazioni di Adobe o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| [Configurazione del tipo di accesso per i datastreams](../../edge/datastreams/overview.md#create) | Quando crei un nuovo datastream, ora puoi selezionare il tipo di richieste che desideri che la rete Edge accetti: <ul><li>**[!UICONTROL Autenticazione mista]**: Quando questa opzione è selezionata, la rete Edge accetta richieste autenticate e non autenticate. Seleziona questa opzione quando intendi usare l’SDK per web o [SDK per dispositivi mobili](https://aep-sdks.gitbook.io/docs/), insieme al [API server](../../server-api/overview.md). </li><li>**[!UICONTROL Solo autenticazione]**: Quando questa opzione è selezionata, la rete Edge accetta solo richieste autenticate. Selezionare questa opzione quando si intende utilizzare solo l&#39;API server e si desidera impedire l&#39;elaborazione di richieste non autenticate da parte del [!DNL Edge Network]. </li></ul> |
| [Proposte di rendering](../../edge/personalization/rendering-personalization-content.md#applypropositions) nelle applicazioni a pagina singola senza incrementare le metriche. | La nuova aggiunta `applyPropositions` consente di eseguire il rendering o l&#39;esecuzione di un array di proposizioni da [!DNL Target] nelle applicazioni a pagina singola, senza incrementare il [!DNL Analytics] e [!DNL Target] metriche. Questo aumenta l’accuratezza dei rapporti. |
| [Condivisione di ID da mobile a web e tra domini diversi](../../edge/identity/id-sharing.md) | L’SDK per web di Adobe Experience Platform ora supporta le funzionalità di condivisione degli ID visitatore che consentono di fornire esperienze personalizzate più accuratamente, tra app mobili e contenuti web per dispositivi mobili, e tra domini diversi. |

Per ulteriori informazioni, consulta la sezione [Panoramica delle connessioni Real-Time CDP](../../rtcdp-connections/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| Versione beta di [!DNL Mixpanel] source | Ora puoi utilizzare la [!DNL Mixpanel] sorgente per acquisire i dati di analisi dal [!DNL Mixpanel] conto all&#39;Experience Platform. Consulta la sezione [[!DNL Mixpanel] documentazione di origine](../../sources/connectors/analytics/mixpanel.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
