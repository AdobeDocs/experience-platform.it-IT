---
title: Note sulla versione di Adobe Experience Platform - Aprile 2022
description: Le note sulla versione di aprile 2022 per Adobe Experience Platform.
source-git-commit: 4bbf7642a456f36ea0fe7fc1c8d68ad37351ff4c
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 3%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 aprile 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Experience Data Model (XDM)](#xdm)

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

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
| Gruppo di campi | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Acquisisce informazioni correlate alla ricerca del sito quali query di ricerca, filtri e ordine. |
| Gruppo di campi | [[!UICONTROL Unisci lead]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Acquisisce i dettagli di un evento in cui vengono uniti due o più lead. |
| Gruppo di campi | [[!UICONTROL Invia e-mail]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Acquisisce i dettagli di un evento in cui viene inviato un messaggio e-mail a un destinatario. |
| Gruppo di campi | [[!UICONTROL Unione di campi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Acquisisce i valori calcolati attraverso il processo di unione delle identità per un evento. |
| Gruppo di campi | [[!UICONTROL Dettagli Destinatario Secondario Per L&#39;Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Un gruppo di campi Adobe Journey Optimizer che acquisisce i dettagli di un destinatario secondario per un controllo di audit. |
| Gruppo di campi | [[!UICONTROL Dettagli sulle relazioni personali dell&#39;account aziendale XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Gruppo di campi | [[!UICONTROL Dettagli persona account]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Tipo di dati | [[!UICONTROL Carrello]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Acquisisce informazioni su un carrello acquisti per e-commerce. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Acquisisce le informazioni di spedizione per uno o più prodotti. |
| Tipo di dati | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Acquisisce informazioni sulle attività di ricerca nel sito. |
| Estensione (Workfront) | [[!UICONTROL Attributi delle attività operative]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Acquisisce i dettagli relativi a un&#39;attività operativa. |
| Estensione (Workfront) | [[!UICONTROL Attributi del Portfolio di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Acquisisce i dettagli relativi a un portafoglio di lavoro. |
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
