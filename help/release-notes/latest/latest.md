---
title: Note sulla versione di Adobe Experience Platform di giugno 2025
description: Note sulla versione di Adobe Experience Platform di giugno 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b39de456b40acda77c67d25ebeba2c8a41c5d3f6
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 46%

---


# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: giovedì 18 giugno 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Controllo degli accessi](#access-control)
- [Gestione avanzata del ciclo di vita dei dati](#advanced-data-lifecycle-management)
- [Servizio catalogo](#catalog-service)
- [Dashboard](#dashboards)
- [Governance dei dati](#data-governance)
- [Destinazioni](#destinations)
- [Composizione di pubblico federato](#fac)
- [Privacy Service](#privacy-service)
- [Sandbox](#sandboxes)
- [Segmentazione](#segmentation-service)
- [Origini](#sources)

## Controllo degli accessi {#access-control}

Experience Platform sfrutta i profili di prodotto [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a diverse funzionalità di Experience Platform, tra cui la modellazione di dati, la gestione dei profili e l’amministrazione della sandbox.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Esporta autorizzazione per i dati del dashboard | Le opzioni **[!UICONTROL Scarica CSV]** e **[!UICONTROL Invia come messaggio e-mail]** nei dashboard ora richiedono l&#39;autorizzazione **[!UICONTROL Esporta dati dashboard]**. Questa autorizzazione garantisce che solo gli utenti autorizzati possano esportare dati insight tabulati, supportando regole di governance e criteri di controllo dell’accesso ai dati più rigidi. Per ulteriori informazioni, leggere la sezione sulle [autorizzazioni della guida al controllo degli accessi](../../access-control/home.md#permissions). |

Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi](../../access-control/home.md).

## Gestione avanzata del ciclo di vita dei dati {#advanced-data-lifecycle-management}

Experience Platform offre una suite di funzionalità di igiene dei dati che ti consentono di gestire i dati archiviati tramite l’eliminazione programmatica di record e set di dati del consumatore. Utilizzando l’area di lavoro del ciclo di vita dei dati nell’interfaccia utente o tramite chiamate all’API di igiene dei dati, puoi gestire in modo efficace gli archivi di dati. Usa queste funzionaità per garantire che le informazioni vengano utilizzate come previsto, che vengano aggiornate quando è necessario correggere dati scorretti e che vengano eliminate quando i criteri organizzativi lo ritengono necessario.

**Nuova documentazione**

| Nuova documentazione | Descrizione |
| --- | --- |
| Record Elimina disponibilità generale | Ora puoi eliminare singoli record in base ai campi di identità utilizzando l’interfaccia utente o l’API. Questa funzione consente di ridurre lo storage, applicare la governance e migliorare l’igiene dei dati consentendo le eliminazioni da un singolo set di dati o tra tutti i set di dati. Si applicano limiti di volume e requisiti di adesione. Per ulteriori informazioni, leggere la [guida eliminazione record](../../hygiene/ui/record-delete.md). |

Per ulteriori informazioni, leggi la [panoramica sulla gestione avanzata del ciclo di vita dei dati](../../hygiene/home.md).

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Anteprima del set di dati migliorata: navigazione più rapida e informazioni più chiare | Anteprima rapida dei dati del set di dati, visualizzazione delle query SQL sottostanti ed esplorazione di un massimo di 100 righe con un filtro migliore e una visibilità più chiara della struttura, il tutto all’interno della familiare esperienza di anteprima del set di dati. Per ulteriori informazioni, leggere la [guida utente per i set di dati](../../catalog/datasets/user-guide.md#preview). |

{style="table-layout:auto"}

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Opzione Invia come esportazione e-mail | Ora puoi esportare fino a 10.000 record dai dashboard in modalità Query Pro selezionando **[!UICONTROL Invia come e-mail]** dal menu **[!UICONTROL Visualizza altro]**. Questa opzione invia in modo sicuro un collegamento per il download all’e-mail associata ad Adobe per esportazioni più grandi. Per ulteriori informazioni, leggere la [guida ulteriori](../../dashboards/sql-insights-query-pro-mode/view-more.md#export). |

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Governance dei dati {#data-governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Inserire nell&#39;elenco Consentiti Configurazione di avvisi CMK di Azure e IP | Ora puoi inserire nell&#39;elenco Consentiti l’indirizzo IP statico di Adobe nell’Insieme di credenziali delle chiavi di Azure per garantire l’accesso continuo quando sono abilitate le restrizioni di rete. Questo aiuta a evitare interruzioni dei servizi Platform dovute a restrizioni nell’accesso alle chiavi. |
| Avvisi e risoluzioni di configurazione CMK | Experience Platform ora attiva gli avvisi quando i servizi Adobe perdono l’accesso all’insieme di credenziali delle chiavi di Azure (ad esempio, a causa di voci di elenco Consentiti IP rimosse o di chiavi disabilitate). Una nuova guida ti aiuta a comprendere ogni avviso e ad intraprendere azioni correttive. |

Per ulteriori informazioni, consulta la [panoramica sulla governance dei dati](../../data-governance/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| --- | --- |
| Connessione [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md) | Utilizza la destinazione [!DNL Algolia] per distribuire una personalizzazione coerente tra i siti dalla home page alla ricerca. Crea tipi di pubblico avanzati da più origini di dati e condividili tra vari canali per migliorare le strategie di targeting e la personalizzazione delle campagne. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Monitoraggio a livello di pubblico](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) per le destinazioni di streaming | Il monitoraggio a livello di pubblico è ora disponibile per le seguenti destinazioni: <ul><li>Connessione [[!DNL (API) Oracle Eloqua] ](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Supporto di identificatori aggiuntivi per [Facebook](../../destinations/catalog/social/facebook.md#supported-identities) destinazioni | La destinazione [!DNL Facebook] ora supporta la mappatura di nuovi campi relativi all&#39;indirizzo per migliorare il targeting e la corrispondenza con i profili nelle proprietà di Facebook. Per informazioni dettagliate sui nuovi campi relativi all&#39;indirizzo, consulta la sezione [identità supportate](../../destinations/catalog/social/facebook.md#supported-identities). <br> ![Immagine dell&#39;interfaccia utente di Platform che mostra i campi aggiuntivi per Facebook.](../2025/assets/june/facebook-destination-fields.png "Immagine dell&#39;interfaccia utente di Platform che mostra i campi aggiuntivi per Facebook."){width="200" align="center" zoomable="yes"} |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) aggiornamento destinazione | A partire dal 19 giugno 2025, è possibile visualizzare due schede **[!DNL Braze]** affiancate nel catalogo delle destinazioni. Ciò è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore di destinazione [!DNL Braze] esistente è stato rinominato in **[!UICONTROL (Obsoleto) Braze]** ed è ora disponibile una nuova scheda con il nome **[!UICONTROL Braze]**. <br> Utilizza la connessione **[!UICONTROL Braze]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi per la destinazione **[!UICONTROL (obsoleto) Braze]**, verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente. <br> Se si creano flussi di dati tramite [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai seguenti valori: <ul><li>Flow spec ID: `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>Connection spec ID: `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

<!-- | [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) general availability | The Google Customer Match + DV360 destination is now available for all Experience Platform users. The documentation now includes detailed guidance for [account linking](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) between [!DNL Adobe] and [!DNL Google] advertising accounts. | -->

Per ulteriori informazioni, consulta la [Panoramica sulle destinazioni](../../destinations/home.md).

## Composizione di pubblico federato {#fac}

La composizione di pubblico federato consente alle aziende di comporre i dati per un migliore utilizzo in vari casi d’uso. Con questo nuovo approccio, in qualità di utente di Adobe Real-Time Customer Data Platform e/o di Adobe Journey Optimizer, puoi federare i set di dati direttamente dal data warehouse esistente per creare e arricchire i tipi di pubblico e gli attributi di Adobe Experience Platform in un unico sistema.

| Nuova funzionalità | Descrizione |
| ----------- | ----------- |
| Disponibilità generale per i clienti Adobe Healthcare Shield | Federated Audience Composition sarà disponibile per i clienti di Adobe Healthcare Shield per i casi di utilizzo di creazione di pubblico, arricchimento e arricchimento del profilo entro la fine di giugno. Per ulteriori informazioni sulle misure di privacy e sicurezza di Federated Audience Composition, leggi [privacy e sicurezza in Panoramica di Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Per ulteriori informazioni sulla conformità HIPAA per i prodotti Experience Platform in generale, leggere la [Panoramica su prodotti e servizi HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Per ulteriori informazioni, consulta la [documentazione sulla composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Nuove normative legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire le richieste di dati dalla clientela. Con [!DNL Privacy Service] puoi inviare richieste di accesso e cancellare dati della clientela personali o privati dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | ---|
| Supporto per le leggi sulla privacy in Tennessee e Minnesota | Privacy Service ora supporta il Tennessee Information Protection Act (`tipa_tn_usa`) e il Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Puoi elaborare le richieste di accesso ed eliminazione in conformità a queste nuove normative a livello di stato. Per ulteriori dettagli, consulta la [Panoramica sulle normative](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview). |

Per ulteriori informazioni sul servizio, consulta la [panoramica di Privacy Service](../../privacy-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Migrazione degli aggiornamenti della configurazione degli oggetti | Dopo la replica iniziale, è ora possibile eseguire la migrazione degli aggiornamenti della configurazione di oggetti iterativi tra sandbox. Questo miglioramento supporta i flussi di lavoro di sviluppo in cui le configurazioni devono essere aggiornate e propagate tra gli ambienti senza ricreare l’intera configurazione sandbox. Per ulteriori informazioni, consulta la guida al [trasferimento degli aggiornamenti della configurazione tra sandbox](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento della disponibilità di approfondimenti simili | Gli approfondimenti simili e i tipi di pubblico simili vengono disabilitati automaticamente per gli ambienti che mostrano un utilizzo ridotto. Per basso utilizzo si intende che non vengono visualizzate informazioni simili negli ultimi tre mesi o che non viene creato un nuovo pubblico simile negli ultimi sei mesi. Ulteriori informazioni su questa modifica sono disponibili nella [guida dei tipi di pubblico simili](../../segmentation/types/lookalike-audiences.md). |

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Supporto interfaccia utente di Beta]{type=Informative} per [!DNL Azure Databricks] | È ora possibile collegare l&#39;account [!DNL Azure Databricks] ad Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente. Per ulteriori informazioni, leggi la guida su [connessione [!DNL Databricks] ad Experience Platform nell&#39;interfaccia utente](../../sources/connectors/databases/databricks.md). |
| Supporto per il nuovo tipo di autenticazione per [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] supporterà ora anche l&#39;autenticazione dell&#39;entità servizio, oltre all&#39;autenticazione della stringa di connessione esistente. Per ulteriori informazioni, leggere la [[!DNL Azure Synapse Analytics] panoramica sull&#39;autenticazione](../../sources/connectors/databases/synapse-analytics.md) |
| [!DNL Salesforce] Autenticazione di base obsoleta | L&#39;autenticazione di base per [Salesforce CRM](../../sources/connectors/crm/salesforce.md) e [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) diventerà obsoleta entro gennaio 2026. I clienti devono effettuare la migrazione all’autenticazione OAuth 2.0 per mantenere la connettività. Questa modifica interessa entrambi i connettori di origine e garantisce una maggiore sicurezza e conformità agli standard di autenticazione di Salesforce. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [Panoramica sulle origini](../../sources/home.md).
