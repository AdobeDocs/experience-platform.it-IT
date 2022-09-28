---
title: Note sulla versione di Adobe Experience Platform - Settembre 2022
description: Note sulla versione di settembre 2022 per Adobe Experience Platform.
source-git-commit: 3d7a04c0ec6cf6a9bed90c9c22db2e8b56bfa01f
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 28 settembre 2022**

Nuove funzioni in Adobe Experience Platform:

- [Igiene dei dati](#data-hygiene)
- [[!UICONTROL Console sulla privacy]](#privacy-console)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Registri di controllo](#audit-logs)
- [Raccolta dati](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Servizio Identity](#identity-service)
- [Origini](#sources)

## Igiene dei dati {#data-hygiene}

Adobe Experience Platform fornisce un solido set di strumenti per gestire operazioni complesse e di grandi dimensioni sui dati al fine di orchestrare le esperienze dei consumatori. Man mano che i dati vengono acquisiti nel sistema nel tempo, diventa sempre più importante gestire gli archivi di dati in modo che i dati vengano utilizzati come previsto, vengono aggiornati quando è necessario correggere i dati errati e vengono eliminati quando i criteri organizzativi lo ritengono necessario.

Le funzionalità di igiene dei dati di Adobe Experience Platform consentono di pulire i dati pianificando la scadenza automatica dei set di dati e l’eliminazione programmatica dei dati dei consumatori in base all’identità.

>[!NOTE]
>
>Le funzionalità di eliminazione dei consumatori sono disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield o Privacy Shield.

Per informazioni sull’igiene dei dati, consulta la seguente documentazione:

- [Panoramica sull&#39;igiene dei dati](../../hygiene/home.md): Scopri le nozioni di base sulle funzionalità di igiene dei dati di Platform.
- [[!UICONTROL Igiene dei dati] Guida all’interfaccia utente](../../hygiene/ui/overview.md): Scopri come pianificare le scadenze dei set di dati e le richieste di cancellazione del consumatore all’interno dell’interfaccia utente di Platform.
- [Guida all’API per l’igiene dei dati](../../hygiene/api/overview.md): Anche tutte le attività di igiene dei dati che puoi eseguire nell’interfaccia utente possono essere eseguite a livello di programmazione

## [!UICONTROL Console sulla privacy] {#privacy-console}

La [!UICONTROL Console sulla privacy] nell’interfaccia utente di Experience Platform è disponibile una vista dashboard delle informazioni chiave provenienti da funzioni relative alla privacy come [richieste di persone interessate da Privacy Service], [ordini di lavoro per l&#39;igiene dei dati]e [registri di controllo]. La console fornisce anche diverse guide di casi d’uso all’interno del prodotto per guidarti attraverso i flussi di lavoro comuni sulla privacy.

Consulta la sezione [Panoramica della console Privacy](../../landing/governance-privacy-security/privacy-console.md) per ulteriori informazioni sulla funzione.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

I servizi AI/ML consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare modelli specifici per le esigenze aziendali utilizzando configurazioni a livello di business senza la necessità di disporre di competenze scientifiche in materia di dati.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
| --- | --- |
| Salva istanza bozza | Questa nuova funzione consente agli analisti di marketing di salvare la configurazione del modello come istanza bozza durante le configurazioni e di continuare a modificare la bozza fino al completamento prima della formazione e del punteggio. Gli scenari in cui questa funzione è utile includono, ma non sono limitati a, quando gli utenti hanno più campi da definire nel flusso di lavoro di configurazione che non sono in grado di completare in una sola volta o quando una o più statistiche del set di dati (come la completezza della colonna) richiedono del tempo per essere elaborate prima che diventino disponibili. Leggi la sezione [Guida utente di Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) per saperne di più. |
| Politiche di governance | Dopo che gli utenti si inviano per creare un&#39;istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di imposizione dei criteri verifica se sono presenti violazioni dei criteri relativi all&#39;utilizzo dei dati e visualizza i dettagli in un pover. Garantisce che le operazioni di dati e le azioni di marketing siano conformi ai criteri di utilizzo dei dati configurati su Adobe Experience Platform. |

Per ulteriori informazioni sulle Attribution AI, consulta [Panoramica di Attribution AI](../../intelligent-services/attribution-ai/overview.md). Per informazioni sui criteri di governance dei dati, consulta la sezione [panoramica dei criteri](../../data-governance/policies/overview.md).

### Customer AI

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala.

| Funzione | Descrizione |
| --- | --- |
| Salva istanza bozza | Questa nuova funzione consente agli analisti di marketing di salvare la configurazione del modello come istanza bozza durante le configurazioni e di continuare a modificare la bozza fino al completamento prima della formazione e del punteggio. Gli scenari in cui questa funzione è utile includono, ma non sono limitati a, quando gli utenti hanno più campi da definire nel flusso di lavoro di configurazione che non sono in grado di completare in una sola volta o quando una o più statistiche del set di dati (come la completezza della colonna) richiedono del tempo per essere elaborate prima che diventino disponibili. Leggi la sezione [Guida utente di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md) per saperne di più. |
| Politiche di governance | Dopo che gli utenti si inviano per creare un&#39;istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di imposizione dei criteri verifica se sono presenti violazioni dei criteri relativi all&#39;utilizzo dei dati e visualizza i dettagli in un pover. Garantisce che le operazioni di dati e le azioni di marketing siano conformi ai criteri di utilizzo dei dati configurati su Adobe Experience Platform. |

Per ulteriori informazioni su Customer AI, consulta la sezione [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md). Per informazioni sui criteri di governance dei dati, consulta la sezione [panoramica dei criteri](../../data-governance/policies/overview.md).

## Registri di audit {#audit-logs}

L’Experience Platform ti consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di controllo forniscono informazioni su chi ha fatto cosa e quando.

**Funzioni aggiornate**

| Funzione | Nome | Descrizione |
| --- | --- | --- |
| Risorse aggiunte | <ul><li>Attribution AI</li><li>Istanza di Customer AI</li><li>Datastream</li></ul> | Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività. Se la funzione è abilitata, non è necessario abilitare manualmente la raccolta dei registri. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui diversi tipi di evento specifici per le risorse tracciati dai registri di controllo in Platform, consulta la sezione [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## Raccolta dati

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Integrazione della navigazione a sinistra nell’interfaccia utente di Platform | Tutte le funzionalità precedentemente esclusive dell’interfaccia utente di raccolta dati (compresi tag, inoltro eventi e datastreams) sono ora disponibili anche nella navigazione a sinistra in Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si lavora con le funzionalità di raccolta dati in Platform. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’interfaccia utente di enum e valori consigliati | Oltre agli enum che abilitano la convalida dei dati, ora puoi [aggiungere o rimuovere valori consigliati](../../xdm/ui/fields/enum.md) per i campi stringa standard o personalizzati in modo che gli utenti di Platform dispongano di un elenco di valori descrittivi da selezionare durante la creazione dei segmenti. |

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Proprietà di un elemento specifico interagito con il quale è stato attivato l&#39;evento di proposizione. |
| Gruppo di campi | [[!UICONTROL Dettagli dell’interazione con MediaAnalytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Tiene traccia delle interazioni multimediali nel tempo. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dati multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Tiene traccia delle informazioni sui dettagli multimediali. |
| Gruppo di campi | [[!UICONTROL Adobe CJM ExperienceEvent - Superfici]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Descrive le superfici per gli eventi di esperienza in Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Serie temporali]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Sono stati aggiunti valori per `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valori rimossi per `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Gruppo di campi | (Multipli) | [Sono state aggiornate diverse descrizioni dei campi](https://github.com/adobe/xdm/pull/1628/files) tra i componenti di Journey Orchestration. |
| Gruppo di campi | (Multipli) | [Sono stati aggiornati i titoli per diversi componenti di Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) per coerenza. |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Sono stati aggiornati i namespace di diversi campi in `xdm`. |
| Gruppo di campi | [[!UICONTROL Campi comuni evento evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | È stato aggiunto un nuovo campo , `isReadSegmentTriggerStartEvent`. |
| Gruppo di campi | [[!UICONTROL Tempo previsto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Modificato il `xdm:uvIndex` è stato aggiunto il campo a un tipo di numero intero e il `xdm` spazio dei nomi in diversi campi in cui era mancante. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dati multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` e `xdm:implementationDetails` sono stati rimossi dal gruppo di campi. |
| Tipo di dati | (Multipli) | [Sono stati aggiornati diversi nomi di proprietà multimediali](https://github.com/adobe/xdm/pull/1626/files) tra diversi tipi di dati per coerenza. |
| Tipo di dati | [[!UICONTROL Dettagli di implementazione]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Aggiunti nomi noti per lo scaricamento. |
| Tipo di dati | [[!UICONTROL Dettagli del punto di interesse]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Il tipo di dati può ora accettare un elenco di coppie chiave-valore di metadati associate al punto di interesse. |
| Tipo di dati | [[!UICONTROL Azione proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| Tipo di dati | [[!UICONTROL Tipo evento proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| (Multipli) | (Multipli) | Le proprietà sperimentali sono state [stabilizzato su tutti i componenti B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Multipli) | (Multipli) | Le entità Adobe Journey Optimizer sono state [stabilizzato](https://github.com/adobe/xdm/pull/1625/files). |
| (Multipli) | (Multipli) | I namespace di alcuni campi in diversi componenti sperimentali sono stati [aggiornato per coerenza](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio Identity {#identity-service}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni cliente sembri avere più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity consente di acquisire una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire in tempo reale esperienze digitali personali di impatto.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione dei set di dati | Il servizio Identity supporta ora l’eliminazione dei set di dati durante la richiesta tramite [API del servizio catalogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), l’interfaccia utente o l’igiene dei dati. Leggi la guida su [eliminazione di set di dati nell’interfaccia utente](../../catalog/datasets/user-guide.md#delete-a-dataset) per ulteriori informazioni. |

Per ulteriori informazioni sul servizio Identity, consulta la sezione [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Audience Manager dell’impatto sulla popolazione del segmento sul profilo cliente in tempo reale | L’acquisizione di popolazioni di segmenti di Audience Manager di grandi dimensioni ha un impatto diretto sul conteggio totale dei profili quando invii per la prima volta un segmento di Audience Manager a Platform utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente portare a un conteggio di profili superiore all’adesione all’utilizzo della licenza. Per ulteriori informazioni, consulta la sezione [Panoramica di Audience Manager Source](../../sources/connectors/adobe-applications/audience-manager.md). Per informazioni sull&#39;utilizzo della licenza, consulta la documentazione su [utilizzo del dashboard di utilizzo della licenza](../../dashboards/guides/license-usage.md). |

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).