---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2023
description: Le note sulla versione di febbraio 2023 per Adobe Experience Platform.
source-git-commit: 66ca8d3972045cffe4a1614f638546f4e7838680
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 22 febbraio 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio query](#query-service)
- [Edizione B2B di Real-Time Customer Data Platform](#b2b)
- [Origini](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate** {#destinations-new-updated-features}

| Funzione | Descrizione |
| ----------- | ----------- |
| [Miglioramento dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) per integrazioni con [destinazioni basate su file (batch)](/help/destinations/destination-types.md#file-based) | <p> Quando i profili non sono più qualificati per i criteri di consenso, ora Experience Platform comunica in modo proattivo la loro uscita dai criteri alle destinazioni basate su file. Questo segue [versione di febbraio 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) della stessa funzionalità per le destinazioni di streaming. </p> <p> <b>Nota</b>: Questa funzionalità è disponibile solo per i clienti di **[!UICONTROL Privacy e sicurezza]** e quelli di **[!UICONTROL Scudo sanitario]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Documentazione nuova o aggiornata** {#destinations-new-updated-documentation}

| Documentazione | Descrizione |
| ----------- | ----------- |
| Come funzionano le destinazioni | <p>Abbiamo pubblicato tre nuovi articoli esplorativi sul funzionamento delle destinazioni, sulla base delle domande comuni degli utenti:</p> <p><ul><li>[Impostazioni di esportazione comuni e configurabili nelle destinazioni](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamento dell’esportazione del profilo per diversi tipi di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestione delle identità nel flusso di lavoro di attivazione delle destinazioni](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Funzioni aggiornate**
&#x200B; | Funzione | Descrizione | | — | — | | Deprecazione del campo tramite l’interfaccia utente | È ora possibile [dopo l’acquisizione dei dati, i campi degli schemi diventano obsoleti](../../xdm/tutorials/field-deprecation-ui.md). La funzione di deprecazione del campo XDM consente di rimuovere i campi dalla visualizzazione dell’interfaccia utente conservandoli per l’utilizzo. Se necessario, puoi visualizzare nuovamente i campi obsoleti e tutti i segmenti, le query o le soluzioni downstream che fanno riferimento ai campi verranno eseguiti come di consueto. |



**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Profilo di prospettiva individuale XDM]](https://github.com/adobe/xdm/pull/1669/files) | La classe Profilo di prospettiva individuale XDM include gli ID forniti dal partner. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [!UICONTROL Vincoli di limitazione della frequenza] | La [!UICONTROL Vincoli di limitazione della frequenza] gruppo di campi [aggiornato per supportare eventi ripetuti e personalizzati](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo di dati | [!UICONTROL Referrer Web] | Le proprietà del referente web sono state [aggiornato per includere `xdm:linkName` e `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Rispettivamente, si tratta del nome e della regione dell’elemento HTML selezionato nella pagina precedente. |
| Gruppo di campi | [!UICONTROL Adobe CJM ExperienceEvent - Dettagli interazione messaggio] | [La [!UICONTROL URL di tracciamento] campo aggiunto](https://github.com/adobe/xdm/pull/1665/files) al [!UICONTROL Adobe CJM ExperienceEvent]. Questo tracker fornisce l’URL selezionato dall’utente. |
| Gruppo di campi | [!UICONTROL Adobe CJM ExperienceEvent - Dettagli sull’interazione del messaggio] | [Il vuoto `meta:enum` proprietà rimossa](https://github.com/adobe/xdm/pull/1668/files) dall’URL [!UICONTROL Tipo di tracciamento] campo . |
| Tipo di dati | [!UICONTROL Informazioni multimediali] | [Il modello regex dal `videoSegment` proprietà in [!UICONTROL Informazioni multimediali] Il tipo di dati è stato rimosso](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md)&#x200B;

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati da data lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento nel Profilo cliente in tempo reale.

**Funzioni aggiornate**
&#x200B; | Funzione | Descrizione | | — | — | | Abilitare i set di dati per il profilo con SQL | Utilizza LE ETICHETTE nelle query CTAS per rendere un set di dati &quot;abilitato al profilo&quot; o utilizza ALTER per aggiornare i set di dati esistenti da abilitare per il profilo. | | Monitorare query pianificate | Utilizza la scheda Query pianificate per trovare informazioni importanti sulle esecuzioni della query e per abbonarti agli avvisi. Monitora le query per i dettagli della pianificazione, lo stato e i messaggi/codici di errore in caso di errore.  | | Attiva/disattiva la funzione di completamento automatico | Elimina alcuni comandi di metadati e migliora i tempi di elaborazione attivando la funzione di completamento automatico dell’editor delle query. Questa funzione suggerisce automaticamente potenziali parole chiave SQL e dettagli della tabella per la query durante la scrittura. | | Esempi di set di dati | Specifica una frequenza di campionamento nella query e utilizza i campioni di set di dati per creare un campione casuale uniforme o creare campioni condizionali basati su criteri specifici. |

&#x200B; Per ulteriori informazioni su Query Services, consulta [Panoramica del servizio query](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Edizione B2B di Real-Time Customer Data Platform {#b2b}

Basato su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Riunisce i dati provenienti da più sorgenti e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli esperti di marketing di eseguire il targeting preciso di tipi di pubblico specifici e coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Abilita il servizio account correlato | La nuova funzione di attivazione/disattivazione consente di abilitare il relativo servizio di account sul tuo account. Per ulteriori informazioni, consulta la guida su [abilitazione del servizio di account correlato](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su Real-Time CDP B2B Edition, consulta la sezione [Panoramica di Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Designare l’accesso a livello di abbonamento con [!DNL Google PubSub] | È ora possibile definire l’accesso a una sottoscrizione di un argomento specifica quando si utilizza il [!DNL Google PubSub] , fornendo l’ID della sottoscrizione al momento dell’autenticazione. Per ulteriori informazioni, consulta la sezione [!DNL Google PubSub] esercitazione sull&#39;autenticazione [utilizzo dell’API del servizio di flusso](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) o [Interfaccia utente della piattaforma](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Acquisisci dati di attività personalizzati da [!DNL Marketo] | Ora puoi importare dati di attività personalizzati dal tuo [!DNL Marketo] Experience Platform. Per acquisire dati di attività personalizzati, devi impostare gruppi di campi di attività personalizzati nello schema Attività B2B e creare un flusso di dati utilizzando il set di dati delle attività. Una volta completato il flusso di dati, il set di dati acquisito conterrà le attività standard e personalizzate dal tuo [!DNL Marketo] istanza. È quindi possibile utilizzare [Servizio query](../../query-service/home.md) per accedere ai record di attività personalizzati in Platform. Per ulteriori informazioni, consulta la guida su [creazione di un flusso di dati per i dati di attività personalizzati](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Escludere i conti non reclamati da [!DNL Marketo] | È ora possibile configurare se si desidera escludere o includere account non reclamati dall’acquisizione durante la creazione di un flusso di dati per i dati delle aziende. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente e di un flusso di dati per [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
