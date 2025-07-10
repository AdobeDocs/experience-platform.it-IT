---
title: Note sulla versione di Adobe Experience Platform di giugno 2025
description: Note sulla versione di Adobe Experience Platform di giugno 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c78dc0e83976499403e066b314a0889df803c976
workflow-type: ht
source-wordcount: '1665'
ht-degree: 100%

---


# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: 18 giugno 2025**

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

Experience Platform sfrutta i profili di prodotto di [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a diverse funzionalità di Experience Platform, tra cui la modellazione dati, la gestione profilo e l’amministrazione della sandbox.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Autorizzazione per esportare i dati della dashboard | Le opzioni **[!UICONTROL Scarica CSV]** e **[!UICONTROL Invia come messaggio e-mail]** nelle dashboard ora richiedono l’autorizzazione **[!UICONTROL Esporta dati dashboard]**. Questa autorizzazione garantisce che solo gli utenti autorizzati possano esportare dati di approfondimenti tabulati, supportando regole di governance e criteri di controllo degli accessi ai dati più rigidi. Per ulteriori informazioni, consulta la sezione sulle [autorizzazioni della guida al controllo degli accessi](../../access-control/home.md#permissions). |

Per ulteriori informazioni, consulta la [panoramica sul controllo degli accessi](../../access-control/home.md).

## Gestione avanzata del ciclo di vita dei dati {#advanced-data-lifecycle-management}

Experience Platform offre una suite di funzionalità di igiene dei dati che ti consentono di gestire i dati archiviati tramite l’eliminazione programmatica di record e set di dati del consumatore. Utilizzando l’area di lavoro del ciclo di vita dei dati nell’interfaccia utente o tramite chiamate all’API di igiene dei dati, puoi gestire in modo efficace gli archivi di dati. Usa queste funzionaità per garantire che le informazioni vengano utilizzate come previsto, che vengano aggiornate quando è necessario correggere dati scorretti e che vengano eliminate quando i criteri organizzativi lo ritengono necessario.

**Nuova documentazione**

| Nuova documentazione | Descrizione |
| --- | --- |
| Elimina record in disponibilità generale | Ora puoi eliminare singoli record in base ai campi di identità utilizzando l’interfaccia utente o l’API. Questa funzione permette di ridurre l’archiviazione, applicare la governance e migliorare l’igiene dei dati consentendo le eliminazioni da un singolo set di dati o tra tutti i set di dati. Si applicano requisiti di limiti di volume e di diritto. Per ulteriori informazioni, consulta la [guida per l’eliminazione dei record](../../hygiene/ui/record-delete.md). |

Per ulteriori informazioni, consulta la [panoramica sulla gestione avanzata del ciclo di vita dei dati](../../hygiene/home.md).

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Anteprima del set di dati migliorata: navigazione più rapida e approfondimenti più chiari | Visualizza rapidamente in anteprima i dati del set di dati, le query SQL sottostanti ed esplora un massimo di 100 righe con un filtro migliore e una visibilità più chiara della struttura, il tutto all’interno dell’esperienza familiare di anteprima del set di dati. Per ulteriori informazioni, consulta la [guida utente per i set di dati](../../catalog/datasets/user-guide.md#preview). |

{style="table-layout:auto"}

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Opzione di esportazione Invia come e-mail | Ora puoi esportare fino a 10.000 record dalle dashboard in Modalità query pro selezionando **[!UICONTROL Invia come e-mail]** dal menu **[!UICONTROL Visualizza altro]**. Questa opzione invia in modo sicuro un collegamento per il download all’indirizzo e-mail associato ad Adobe per esportazioni più grandi. Per ulteriori informazioni, consulta la [guida visualizza altro](../../dashboards/sql-insights-query-pro-mode/view-more.md#export). |

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Governance dei dati {#data-governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Configurazione elenco Consentiti IP e avvisi CMK di Azure | Ora puoi inserire nell’elenco Consentiti l’indirizzo IP statico di Adobe in Azure Key Vault per garantire l’accesso continuo quando sono abilitate le restrizioni di rete. Questo consente di evitare interruzioni dei servizi Platform dovute a restrizioni all’accesso limitato alle chiavi. |
| Avvisi e risoluzioni di configurazione CMK | Experience Platform ora attiva gli avvisi quando i servizi Adobe perdono l’accesso ad Azure Key Vault (ad esempio, a causa di voci rimosse dall’elenco Consentiti IP o di chiavi disabilitate). Una nuova guida ti aiuta a comprendere ogni avviso e a intraprendere azioni correttive. |

Per ulteriori informazioni, consulta la [panoramica sulla governance dei dati](../../data-governance/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| --- | --- |
| Connessione [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md) | Utilizza la destinazione [!DNL Algolia] per distribuire una personalizzazione coerente tra i siti dalla pagina Home alla ricerca. Crea tipi di pubblico avanzati da più origini di dati e condividili tra vari canali per migliorare le strategie di targeting e la personalizzazione delle campagne. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) disponibilità generale | La destinazione Google Customer Match + DV360 è ora disponibile per tutti gli utenti di Experience Platform. La documentazione ora include istruzioni dettagliate per il [collegamento account](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) tra gli account pubblicitari [!DNL Adobe] e [!DNL Google]. |
| [Monitoraggio a livello di pubblico](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) per le destinazioni di streaming | Il monitoraggio a livello di pubblico è ora disponibile per le seguenti destinazioni: <ul><li>[[!DNL (API) Oracle Eloqua] connessione](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Supporto di identificatori aggiuntivi per destinazioni [Facebook](../../destinations/catalog/social/facebook.md#supported-identities) | La destinazione [!DNL Facebook] ora supporta la mappatura di nuovi campi relativi all’indirizzo per migliorare il targeting e la corrispondenza con i profili nelle proprietà di Facebook. Per ulteriori informazioni sui nuovi campi relativi all’indirizzo, consulta la sezione sulle [identità supportate](../../destinations/catalog/social/facebook.md#supported-identities). <br> ![Immagine dell’interfaccia utente di Platform che mostra i campi aggiuntivi per Facebook.](../2025/assets/june/facebook-destination-fields.png "Immagine dell’interfaccia utente di Platform che mostra i campi aggiuntivi per Facebook."){width="200" align="center" zoomable="yes"} |
| Aggiornamento destinazione [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | A partire dal 19 giugno 2025 nel catalogo delle destinazioni, puoi visualizzare due schede **[!DNL Braze]** affiancate. Questo è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore della destinazione [!DNL Braze] esistente è stato rinominato in **[!UICONTROL Braze (obsoleto)]** ed è ora disponibile una nuova scheda denominata **[!UICONTROL Braze]**. <br> Utilizza la connessione **[!UICONTROL Braze]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi nella destinazione **[!UICONTROL Braze (obsoleto)]**, questi verranno aggiornati automaticamente e non è quindi richiesta alcuna azione da parte tua. <br> Se si creano flussi di dati tramite [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai seguenti valori: <ul><li>Flow spec ID: `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>Connection spec ID: `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Composizione di pubblico federato {#fac}

La composizione di pubblico federato consente alle aziende di comporre i dati per un migliore utilizzo in vari casi d’uso. Con questo nuovo approccio, in qualità di utente di Adobe Real-Time Customer Data Platform e/o di Adobe Journey Optimizer, puoi federare i set di dati direttamente dal data warehouse esistente per creare e arricchire i tipi di pubblico e gli attributi di Adobe Experience Platform in un unico sistema.

| Nuova funzione | Descrizione |
| ----------- | ----------- |
| Disponibilità generale per la clientela Healthcare Shield di Adobe | La funzione Composizione di pubblico federato sarà disponibile per la clientela Healthcare Shield di Adobe per i casi d’uso di creazione di pubblico, arricchimento e arricchimento del profilo entro la fine di giugno. Per ulteriori informazioni sulle misure di privacy e sicurezza della funzione Composizione di pubblico federato, consulta [privacy e sicurezza nella panoramica sulla Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/start/privacy-security). Per ulteriori informazioni sulla conformità HIPAA per i prodotti Experience Platform in generale, consulta la [panoramica sui prodotti e servizi HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Per ulteriori informazioni, consulta la [documentazione sulla composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Nuove normative legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire le richieste di dati dalla clientela. Con [!DNL Privacy Service] puoi inviare richieste di accesso e cancellare dati della clientela personali o privati dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | ---|
| Supporto per leggi sulla privacy in Tennessee e Minnesota | Privacy Service ora supporta il Tennessee Information Protection Act (`tipa_tn_usa`) e il Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Puoi elaborare le richieste di accesso ed eliminazione in conformità a queste nuove normative a livello di stato. Per ulteriori dettagli, consulta la [panoramica sulle normative](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/regulations/overview). |

Per ulteriori informazioni sul servizio, consulta la [panoramica di Privacy Service](../../privacy-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere a sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Migrazione degli aggiornamenti di configurazione degli oggetti | Dopo la replica iniziale, è ora possibile eseguire la migrazione degli aggiornamenti di configurazione degli oggetti iterativi tra sandbox. Questo miglioramento supporta flussi di lavoro di sviluppo in cui le configurazioni devono essere aggiornate e propagate tra gli ambienti senza ricreare l’intera configurazione della sandbox. Per ulteriori informazioni, consulta la guida al [trasferimento degli aggiornamenti di configurazione tra sandbox](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento della disponibilità di approfondimenti per similarità | Gli approfondimenti e i tipi di pubblico per similarità vengono disabilitati automaticamente per gli ambienti che mostrano un basso utilizzo. Per basso utilizzo si intende che non vengono visualizzati approfondimenti per similarità negli ultimi tre mesi, oppure che non viene creato un nuovo pubblico per similarità negli ultimi sei mesi. Ulteriori dettagli su questa modifica sono disponibili nella [guida sui tipi di pubblico per similarità](../../segmentation/types/lookalike-audiences.md). |

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto interfaccia utente [!BADGE Beta]{type=Informative} per [!DNL Azure Databricks] | Ora puoi connettere il tuo account [!DNL Azure Databricks] a Experience Platform utilizzando l’area di lavoro delle origini nell’interfaccia utente. Per ulteriori informazioni, consulta la guida sulla [connessione [!DNL Databricks]  a Experience Platform nell’interfaccia utente](../../sources/connectors/databases/databricks.md). |
| Supporto per nuovo tipo di autenticazione per [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] supporterà ora anche l’autenticazione con l’entità principale del servizio, oltre all’autenticazione con stringa di connessione esistente. Per ulteriori informazioni, consulta la [[!DNL Azure Synapse Analytics] panoramica sull’autenticazione](../../sources/connectors/databases/synapse-analytics.md). |
| Obsolescenza dell’autenticazione di base per [!DNL Salesforce] | L’autenticazione di base per [Salesforce CRM](../../sources/connectors/crm/salesforce.md) e [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) diventerà obsoleta entro gennaio 2026. La clientela deve effettuare la migrazione all’autenticazione OAuth 2.0 per mantenere la connettività. Questa modifica interessa entrambi i connettori di origine e garantisce una maggiore sicurezza e conformità agli standard di autenticazione di Salesforce. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
