---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di febbraio 2023 per Adobe Experience Platform.
source-git-commit: ccd3df0bc045f98306901b2d734cf17262275f18
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 7%

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

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobi o non Adobi.

### Assurance {#assurance}

Adobe Assurance consente di verificare, verificare, simulare e convalidare la modalità di raccolta dei dati o di gestione delle esperienze nell’app mobile.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| API pubbliche | Le API Adobe Assurance sono ora disponibili. Le API Assurance sono una raccolta di API che consentono agli utenti di testare ed eseguire il debug delle proprie app web e mobili, quando dotate dell’estensione Adobe Assurance con Mobile SDK. Per ulteriori informazioni sulle API Assurance, consulta la sezione [Panoramica dell’API Assurance](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su Assurance, leggere [Documentazione di Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate** {#destinations-new-updated-features}

| Funzione | Descrizione |
| ----------- | ----------- |
| [Miglioramento dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) per le integrazioni con [destinazioni basate su file (batch)](/help/destinations/destination-types.md#file-based) | <p> Quando i profili non sono più qualificati per un criterio di consenso, Experience Platform ora comunica in modo proattivo la propria uscita dal criterio alle destinazioni basate su file. Questo segue il [versione di febbraio 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) della stessa funzionalità per le destinazioni di streaming. </p> <p> <b>Nota</b>: questa funzionalità è disponibile solo per i clienti di **[!UICONTROL Privacy e sicurezza]** e quelli di **[!UICONTROL Healthcare Shield]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Documentazione nuova o aggiornata** {#destinations-new-updated-documentation}

| Documentazione | Descrizione |
| ----------- | ----------- |
| Funzionamento delle destinazioni | <p>Abbiamo pubblicato tre nuovi articoli esplicativi sul funzionamento delle destinazioni, basati sulle domande comuni degli utenti:</p> <p><ul><li>[Impostazioni di esportazione comuni e configurabili nelle destinazioni](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamento di esportazione del profilo per diversi tipi di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestione dell’identità nel flusso di lavoro di attivazione delle destinazioni](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Deprecazione del campo tramite l’interfaccia utente | Ora puoi [deprecare i campi dagli schemi dopo l’acquisizione dei dati](../../xdm/tutorials/field-deprecation-ui.md). La deprecazione dei campi XDM consente di rimuovere i campi dalla vista dell’interfaccia utente conservandoli per l’utilizzo. Se necessario, puoi visualizzare nuovamente i campi obsoleti; eventuali segmenti, query o soluzioni a valle che fanno riferimento a tali campi verranno eseguiti come di consueto. |

{style=&quot;table-layout:auto&quot;}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Profilo potenziale individuale XDM]](https://github.com/adobe/xdm/pull/1669/files) | La classe XDM Individual Prospect Profile include gli ID forniti dai partner. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [!UICONTROL Vincoli di quota limite] | Il [!UICONTROL Vincoli di quota limite] gruppo di campi è stato [aggiornato per supportare eventi ripetuti e personalizzati](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo di dati | [!UICONTROL Referente web] | Le proprietà del referente web sono state [aggiornato per includere `xdm:linkName` e `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Rispettivamente, questi sono il nome e l’area dell’elemento HTML selezionato nella pagina precedente. |
| Gruppo di campi | [!UICONTROL Adobe di ExperienceEvent CJM: dettagli sull’interazione del messaggio] | [Il [!UICONTROL URL tracker] il campo è stato aggiunto](https://github.com/adobe/xdm/pull/1665/files) al [!UICONTROL Adobe di ExperienceEvent CJM]. Questo tracker fornisce l’URL selezionato dall’utente. |
| Gruppo di campi | [!UICONTROL Adobe di ExperienceEvent CJM: dettagli sull’interazione del messaggio] | [Il vuoto `meta:enum` la proprietà è stata rimossa](https://github.com/adobe/xdm/pull/1668/files) dall’URL [!UICONTROL Tipo di tracciamento] campo. |
| Tipo di dati | [!UICONTROL Informazioni multimediali] | [Il pattern regex dalla `videoSegment` proprietà in [!UICONTROL Informazioni multimediali] tipo di dati rimosso](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire in Real-Time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Abilitare i set di dati per il profilo con SQL | [Utilizzare le etichette nelle query CTAS per rendere un set di dati &quot;abilitato per il profilo&quot;](../../query-service/sql/syntax.md#create-table-as-select), oppure utilizza ALTER per aggiornare i set di dati esistenti da abilitare per il profilo. È possibile utilizzare questo costrutto SQL esteso per fornire supporto senza soluzione di continuità per gli attributi derivati per i casi di utilizzo aziendali di Real-Time Customer Profile. Consulta la [Flusso SQL senza interruzioni per il documento attributi derivati](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) per ulteriori dettagli. |
| Monitorare le query pianificate | Utilizza il [Scheda Query pianificate](../../query-service/ui/monitor-queries.md) per trovare informazioni importanti sull’esecuzione della query e abbonarti agli avvisi. Monitora le query per i dettagli della pianificazione, lo stato e i messaggi/codici di errore in caso di esito negativo. |
| Attiva/disattiva la funzione di completamento automatico | Eliminazione di alcuni comandi relativi ai metadati e miglioramento dei tempi di elaborazione [attivazione/disattivazione della funzione di completamento automatico di Query Editor](../../query-service/ui/user-guide.md#auto-complete). Questa funzione suggerisce automaticamente le parole chiave SQL potenziali e i dettagli della tabella per la query durante la scrittura. |
| Esempi di set di dati | Specificare una frequenza di campionamento nella query e [utilizzare gli esempi di set di dati per creare un campione casuale uniforme](../../query-service/essential-concepts/dataset-samples.md)o creare campioni condizionali in base a criteri specifici. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su Query Services, consulta [Panoramica di Query Service](../../query-service/home.md).

## Edizione B2B di Real-Time Customer Data Platform {#b2b}

Basata su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettata appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli addetti al marketing di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Abilita servizio account correlati | La nuova funzione di attivazione/disattivazione consente di abilitare il servizio account correlato sul tuo account. Per ulteriori informazioni, consulta la guida su [abilitazione del servizio account correlato](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulla versione B2B di Real-Time CDP, leggere [Panoramica dell’edizione B2B di Real-Time CDP](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Designare l’accesso a livello di abbonamento con [!DNL Google PubSub] | È ora possibile definire l’accesso a una sottoscrizione di argomento specifica quando si utilizza [!DNL Google PubSub] fornendo l’ID dell’abbonamento al momento dell’autenticazione. Per ulteriori informazioni, leggere [!DNL Google PubSub] tutorial sull’autenticazione [utilizzo dell’API del servizio Flusso](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) o [Interfaccia utente di Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Acquisire dati di attività personalizzati da [!DNL Marketo] | Ora puoi importare dati di attività personalizzati dal tuo [!DNL Marketo] da Experience Platform. Per acquisire dati personalizzati sulle attività, devi impostare gruppi di campi attività personalizzati nello schema Attività B2B e creare un flusso di dati utilizzando il set di dati attività. Una volta completato il flusso di dati, il set di dati acquisito conterrà sia le attività standard che quelle personalizzate del [!DNL Marketo] dell&#39;istanza. A questo punto puoi utilizzare [Servizio query](../../query-service/home.md) per accedere ai record di attività personalizzati su Platform. Per ulteriori informazioni, consulta la guida su [creazione di un flusso di dati per dati di attività personalizzati](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Escludi account non rivendicati da [!DNL Marketo] | Ora puoi configurare se escludere o includere account non rivendicati dall’acquisizione durante la creazione di un flusso di dati per i dati aziendali. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente e di un flusso di dati per [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).
