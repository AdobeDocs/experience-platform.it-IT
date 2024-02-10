---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2023
description: Note sulla versione di Adobe Experience Platform di febbraio 2023.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 5bf54374773fd95ae1c40dd00b5dbe633031b70e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 97%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 22 febbraio 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio query](#query-service)
- [Edizione B2B di Real-Time Customer Data Platform](#b2b)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

### Assurance {#assurance}

Adobe Assurance consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze all’interno delle tue applicazioni mobili.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| API pubbliche | Le API di Adobe Assurance sono ora disponibili. Le API di Assurance sono una raccolta di API che consente agli utenti di testare ed eseguire il debug delle proprie app web e per dispositivi mobili, se dotate dell’estensione Adobe Assurance con Mobile SDK. Per ulteriori informazioni sulle API di Assurance, consulta la sezione [Panoramica sulle API di Assurance](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Per ulteriori informazioni su Assurance, consulta la [documentazione di Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate** {#destinations-new-updated-features}

| Funzione | Descrizione |
| ----------- | ----------- |
| [Miglioramento dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) per le integrazioni con [destinazioni basate su file (batch)](/help/destinations/destination-types.md#file-based) | <p> Quando i profili non sono più qualificati per un criterio di consenso, Experience Platform ora comunica in modo proattivo la relativa uscita dal criterio alle destinazioni basate su file. Questo segue la [versione di febbraio 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) della stessa funzionalità per le destinazioni di streaming. </p> <p> <b>Nota</b>: questa funzionalità è disponibile solo per i clienti di **[!UICONTROL Privacy and Security Shield]** e quelli di **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Documentazione nuova o aggiornata** {#destinations-new-updated-documentation}

| Documentazione | Descrizione |
| ----------- | ----------- |
| Documentazione sul funzionamento delle destinazioni | <p>Abbiamo pubblicato tre nuovi articoli esplicativi sul funzionamento delle destinazioni, basati sulle domande comuni degli utenti:</p> <p><ul><li>[Impostazioni di esportazione comuni e configurabili nelle destinazioni](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamento di esportazione del profilo per diversi tipi di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestione dell’identità nel flusso di lavoro di attivazione delle destinazioni](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Deprecazione del campo tramite l’interfaccia utente | Ora puoi [rendere obsoleti i campi dagli schemi dopo l’acquisizione dei dati](../../xdm/tutorials/field-deprecation-ui.md). La funzione obsoleta dei campi XDM consente di rimuovere i campi dalla vista dell’interfaccia utente conservandoli per l’utilizzo. Se necessario, puoi visualizzare nuovamente i campi obsoleti; eventuali segmenti, query o soluzioni a valle che fanno riferimento a tali campi verranno eseguiti come di consueto. |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Profilo individuale potenziale cliente XDM]](https://github.com/adobe/xdm/pull/1669/files) | La classe del profilo individuale potenziale cliente XDM include gli ID forniti dai partner. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [!UICONTROL Vincoli di quota limite] | Il gruppo di campi [!UICONTROL Vincoli di quota limite] è stato [aggiornato per supportare eventi ripetuti e personalizzati](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo di dati | [!UICONTROL Riferimento web] | Le proprietà del riferimento web sono state [aggiornate per includere `xdm:linkName` e `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Rispettivamente, questi sono il nome e l’area dell’elemento HTML selezionato nella pagina precedente. |
| Gruppo di campi | [!UICONTROL Adobe CJM ExperienceEvent: dettagli sull’interazione del messaggio] | [Il campo [!UICONTROL tracciamento URL] è stato aggiunto](https://github.com/adobe/xdm/pull/1665/files) ad [!UICONTROL Adobe CJM ExperienceEvent]. Questo tracciamento fornisce l’URL selezionato dall’utente. |
| Gruppo di campi | [!UICONTROL Adobe CJM ExperienceEvent: dettagli sull’interazione del messaggio] | [La proprietà `meta:enum` vuota è stata rimossa](https://github.com/adobe/xdm/pull/1668/files) dal campo [!UICONTROL Tipo di tracciamento] dell’URL. |
| Tipo di dati | [!UICONTROL Informazioni su file multimediali] | [Il pattern regex dalla proprietà `videoSegment` nel tipo di dati [!UICONTROL Informazioni su file multimediali] è stato rimosso](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform.[!DNL Data Lake] Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Abilitare i set di dati per il profilo con SQL | [Utilizza LABEL nelle query CTAS per rendere un set di dati “abilitato per il profilo”](../../query-service/sql/syntax.md#create-table-as-select), oppure utilizza ALTER per aggiornare i set di dati esistenti da abilitare per il profilo. È possibile utilizzare questo costrutto SQL esteso per fornire supporto senza soluzione di continuità per i set di dati derivati per i casi di utilizzo aziendali di Real-Time Customer Profile. Consulta la [Flusso SQL semplice per il documento dei set di dati derivati](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md) per ulteriori dettagli. |
| Monitorare le query pianificate | Utilizza la [Scheda query pianificate](../../query-service/ui/monitor-queries.md) per trovare informazioni importanti sulle esecuzioni delle query e abbonarti agli avvisi. Monitora le query per i dettagli della pianificazione, lo stato e i messaggi/codici di errore in caso di esito negativo. |
| Attiva/disattiva la funzione di completamento automatico | Elimina alcuni comandi relativi ai metadati e migliora i tempi di elaborazione tramite l’[attivazione/disattivazione della funzione di completamento automatico dell’Editor di query](../../query-service/ui/user-guide.md#auto-complete). Questa funzione suggerisce automaticamente le potenziali parole chiave SQL e i dettagli della tabella per la query durante la scrittura. |
| Esempi di set di dati | Specifica una frequenza di campionamento nella query e [utilizza gli esempi di set di dati per creare un campione casuale uniforme](../../query-service/key-concepts/dataset-samples.md) oppure creare campioni condizionali in base a criteri specifici. |

{style="table-layout:auto"}

Per ulteriori informazioni sul Servizio query, consulta la [Panoramica sul servizio query](../../query-service/home.md).


## Edizione B2B di Real-Time Customer Data Platform {#b2b}

L’Edizione B2B di Real-Time CDP, basata su Real-Time Customer Data Platform (Real-Time CDP), è creata appositamente per i marketer che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Abilitare il servizio account correlato | La nuova funzione di attivazione/disattivazione consente di abilitare il servizio account correlato sul tuo account. Per ulteriori informazioni, consulta la guida sull’[abilitazione del servizio account correlato](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Per ulteriori informazioni sull’Edizione B2B di Real-Time CDP, consulta la [Panoramica sull’edizione B2B di Real-Time CDP](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Specificare l’accesso a livello di abbonamento con [!DNL Google PubSub] | È ora possibile definire l’accesso a un abbonamento di argomento specifico quando si utilizza [!DNL Google PubSub] fornendo l’ID dell’abbonamento al momento dell’autenticazione. Per ulteriori informazioni, consulta il [!DNL Google PubSub]tutorial sull’autenticazione [utilizzando l’API del servizio Flow](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) oppure l’[Interfaccia utente di Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Acquisire dati di attività personalizzati da [!DNL Marketo] | Ora puoi importare dati di attività personalizzati dalla tua istanza di [!DNL Marketo] a Experience Platform. Per acquisire dati personalizzati sulle attività, devi impostare gruppi di campi attività personalizzati nello schema Attività B2B e creare un flusso di dati utilizzando il set di dati attività. Una volta completato il flusso di dati, il set di dati acquisito conterrà sia le attività standard che quelle personalizzate dell’istanza [!DNL Marketo]. Puoi quindi utilizzare il [Servizio query](../../query-service/home.md) per accedere ai record di attività personalizzati su Platform. Per ulteriori informazioni, consulta la guida sulla [creazione di un flusso di dati per dati di attività personalizzati](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Escludere account non rivendicati da [!DNL Marketo] | Ora è possibile configurare se desideri escludere o includere account non rivendicati dall’acquisizione durante la creazione di un flusso di dati per i dati aziendali. Per ulteriori informazioni, consulta la guida sulla [creazione di una connessione di origine e di un flusso di dati per  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).
