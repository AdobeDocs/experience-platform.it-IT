---
title: Note sulla versione di Adobe Experience Platform - Aprile 2022
description: Le note sulla versione di aprile 2022 per Adobe Experience Platform.
source-git-commit: d09eb2e71a5ebce31aeaf8560c20f0c8595f5d19
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 aprile 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Flussi di dati](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Edizione B2B di Real-time Customer Data Platform](#B2B)
- [Origini](#sources)

## Flussi di dati {#dataflows}

In Platform, i dati vengono acquisiti da diverse sorgenti, analizzati all’interno del sistema e attivati in un’ampia gamma di destinazioni. Platform facilita il processo di tracciamento di questo flusso di dati potenzialmente non lineare grazie alla trasparenza dei flussi di dati.

Dataflows are a representation of jobs that move data across Platform. Questi flussi di dati sono configurati tra diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati dal servizio Identity e dal profilo cliente in tempo reale prima di essere infine attivati nelle destinazioni.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Dashboard dei segmenti | Ora puoi utilizzare il dashboard di monitoraggio per monitorare i flussi di dati per i segmenti. Per ulteriori informazioni, consulta la guida su [monitoraggio dei segmenti nell’interfaccia utente](../../dataflows/ui/monitor-segments.md) |

Per informazioni più generali sui flussi di dati, consulta [panoramica dei dataflows](../../dataflows/home.md). Per ulteriori informazioni sulla segmentazione, consulta la sezione [panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Support for Adobe Analytics source | L’origine Adobe Analytics ora supporta le funzioni di preparazione dei dati, che consentono di mappare i dati della suite di rapporti di Analytics su uno schema XDM di destinazione durante la creazione di un flusso di dati. See the tutorial on [creating an Analytics source connection](../../sources/tutorials/ui/create/adobe-applications/analytics.md) for more information. |
| Supporto per l&#39;importazione di regole di mappatura esistenti | Ora puoi importare le regole di mappatura da un flusso di dati esistente per accelerare le configurazioni del flusso di dati e limitare gli errori. See the tutorial on [importing existing mapping rules](../../data-prep/ui/mapping.md) for more information. |

Per ulteriori informazioni su [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Aggiunta o rimozione di singoli campi standard per uno schema | L’interfaccia utente dell’Editor di schema ora consente di aggiungere parti di gruppi di campi standard agli schemi, fornendo maggiore flessibilità per i campi che si sceglie di includere senza dover creare risorse personalizzate da zero.<br><br>È ora inoltre possibile definire campi personalizzati ad hoc direttamente all’interno della struttura dello schema e assegnarli a un gruppo di campi personalizzato nuovo o esistente senza dover prima creare o modificare il gruppo di campi.<br><br>Consulta la guida su [creazione e modifica di schemi nell’interfaccia utente](../../xdm/ui/resources/schemas.md) per ulteriori informazioni su questi nuovi flussi di lavoro. |

{style=&quot;table-layout:auto&quot;}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Richiesta di funzionamento dell&#39;igiene dei dati]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Acquisisce i dettagli di una richiesta di pulizia dei dati per eliminare o modificare i record in un set di dati o sandbox specifico. |
| Descrittore | [[!UICONTROL Descrittore di granularità della serie temporale]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica la granularità delle serie temporali e dei dati di riepilogo. Quando viene applicato a uno schema, la proprietà `timestamp` è la prima marca temporale in un periodo di questa granularità. |
| Classe | [[!UICONTROL Metriche di riepilogo XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fornisce metriche pre-riepilogate con dimensioni di raggruppamento, ad esempio i risultati di un SQL SELECT con un GROUP BY. |
| Gruppo di campi | [[!UICONTROL Mappa dei risultati della valutazione delle politiche di consenso]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Acquisisce il risultato della valutazione dei criteri di consenso per un singolo utente. |
| Field group | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captures site-search related information such as search query, filtering, and ordering. |
| Field group | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Acquisisce i dettagli di un evento in cui vengono uniti due o più lead. |
| Field group | [[!UICONTROL Invia e-mail]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Acquisisce i dettagli di un evento in cui viene inviato un messaggio e-mail a un destinatario. |
| Field group | [[!UICONTROL Unione di campi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Acquisisce i valori calcolati attraverso il processo di unione delle identità per un evento. |
| Gruppo di campi | [[!UICONTROL Dettagli Destinatario Secondario Per L&#39;Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Un gruppo di campi Adobe Journey Optimizer che acquisisce i dettagli di un destinatario secondario per un controllo di audit. |
| Gruppo di campi | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Gruppo di campi | [[!UICONTROL Dettagli persona account]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Data type | [[!UICONTROL Carrello]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Acquisisce informazioni su un carrello acquisti per e-commerce. |
| Tipo di dati | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Acquisisce le informazioni di spedizione per uno o più prodotti. |
| Data type | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captures information on site-search activity. |
| Extension (Workfront) | [[!UICONTROL Attributi delle attività operative]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Captures details related to an operational task. |
| Estensione (Workfront) | [[!UICONTROL Attributi del Portfolio di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Captures details related to a work portfolio. |
| Estensione (Workfront) | [[!UICONTROL Attributi del programma di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Acquisisce i dettagli relativi a un programma di lavoro. |
| Estensione (Workfront) | [[!UICONTROL Attributi del progetto di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Acquisisce i dettagli relativi a un progetto di lavoro. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione aggiornamento |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Destinazioni ]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nuovi valori enum per `destinationCategory`. |
| Descrittore | [[!UICONTROL Descrittore di nome descrittivo]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | È stato aggiunto il supporto per la rimozione dei valori suggeriti (`meta:enum`) non necessarie nei campi standard. |
| Gruppo di campi | [[!UICONTROL Processo di accesso utente]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` campo aggiunto. |
| Tipo di dati | [[!UICONTROL Commercio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Sono stati aggiunti diversi campi relativi al carrello. |
| Tipo di dati | [[!UICONTROL Voce dell’elenco dei prodotti]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nuovi campi aggiunti per le opzioni selezionate e l’importo dello sconto. |
| Estensione (Intelligent Services) | [[!UICONTROL Ottimizzazione dei tempi di invio di JourneyAI Intelligent Services]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Ottimizza il formato di archiviazione per i punteggi del tempo di invio. |
| Estensione (Workfront) | [[!UICONTROL Evento di modifica Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Diversi campi sono stati sostituiti da un `workfront:customData` campo per campi modulo personalizzati. |
| Estensione (Workfront) | [[!UICONTROL Attributi attività di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Sono stati aggiunti diversi campi. |
| Estensione (Workfront) | [[!UICONTROL Oggetto di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nuovi campi per il tipo di oggetto principale e i campi modulo personalizzati. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

### Edizione B2B di Real-time Customer Data Platform {#B2B}

Basato su Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. It brings together data from multiple sources and combines it into a single view of people and account profiles. This unified data allows marketers to precisely target specific audiences and engage those audiences across all available channels.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per `isDeleted` funzionalità | All [!DNL Marketo] datasets except `Activities` now support the `isDeleted` mapping. La nuova mappatura viene aggiunta automaticamente ai flussi di dati B2B esistenti. È possibile utilizzare `isDeleted` mappatura per filtrare i record eliminati in modo che i dati nella [!DNL Data Lake] è coerente con i dati di origine. See the [[!DNL Marketo] mapping fields guide](../../sources/connectors/adobe-applications/mapping/marketo.md) for more information on `isDeleted`. |

Per ulteriori informazioni su Real-time Customer Data Platform B2B Edition, consulta la sezione [Panoramica B2B](../../rtcdp/b2b-overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per [!DNL OneTrust Integration] | Ora puoi utilizzare la [!DNL OneTrust Integration] sorgente per acquisire i dati di consenso e preferenze dal tuo [!DNL OneTrust] a Platform. Consulta la documentazione su [creazione di un [!DNL OneTrust Integration] connessione sorgente](../../sources/connectors/consent-and-preferences/onetrust.md) per ulteriori informazioni. |
| Supporto per [!DNL Square] | Ora puoi utilizzare la [!DNL Square] origine per acquisire i dati di pagamento dal [!DNL Square] a Platform. |
| Supporto per l&#39;eliminazione dei flussi di dati Attributi del cliente | È ora possibile eliminare i flussi di dati creati con il connettore di origine Attributi del cliente. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
