---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di settembre 2023 per Adobe Experience Platform.
source-git-commit: 1bfd5e05642e0ac8f80af5502878eaee0b33c704
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 26%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 28 settembre 2023**

Nuove funzioni di Adobe Experience Platform:

- [Attributi calcolati](#computed-attributes)

Aggiornamenti alle funzioni esistenti in Experience Platform:

- [Avvisi](#alerts)
- [Raccolta dati](#data-collection)
- [Identity Service](#identity-service)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Attributi calcolati {#computed-attributes}

Gli attributi calcolati consentono di riepilogare facilmente i dati dell’evento negli attributi del profilo tramite un’interfaccia utente intuitiva per migliorare la segmentazione, la personalizzazione e l’attivazione basate sul comportamento. Con questa funzione, puoi creare attributi calcolati in modo autonomo, gestirli e utilizzarli in segmentazione, destinazioni Real-Time CDP o Adobe Journey Optimizer. Inoltre, gli attributi calcolati semplificano la segmentazione e i flussi di lavoro di percorso per aiutarti a fornire esperienze rilevanti in modo semplice. Per ulteriori informazioni sugli attributi calcolati, consulta [panoramica degli attributi calcolati](../../profile/computed-attributes/overview.md).

## Avvisi {#alerts}

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. È possibile abbonarsi a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Scheda Cronologia avvisi | Avvisi [!UICONTROL Cronologia] La scheda ora includerà tutti gli eventi tra cui ritardi, avvii, successo e errori. Leggi le [documentazione dell’interfaccia utente avvisi](../../observability/alerts/ui.md) per ulteriori informazioni sulla scheda cronologia. |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, consulta la sezione [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Stream di dati | Supporto per la ricerca del dispositivo | Durante la configurazione di un flusso di dati, ora puoi selezionare il livello di informazioni di ricerca del dispositivo da raccogliere. Le informazioni sulla ricerca del dispositivo includono dati sul dispositivo, sull’hardware, sul sistema operativo e sul browser utilizzati per interagire con la pagina. <br>  Non è possibile raccogliere le informazioni di ricerca del dispositivo insieme all’agente utente e agli hint client. La scelta di raccogliere informazioni sul dispositivo disabiliterà la raccolta di hint dell’agente utente e del client e viceversa. Tutte le informazioni di ricerca del dispositivo sono memorizzate in `xdm:device` gruppo di campi. Per ulteriori informazioni, consulta la documentazione su [configurazione degli stream di dati](../../datastreams/configure.md#geolocation-device-lookup). |
| Estensioni | [!DNL TikTok] estensione API per eventi web | Il [[!DNL TikTok] API per eventi web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL TikTok] sotto forma di eventi lato server che utilizzano [!DNL TikTok] API per eventi web. |

{style="table-layout:auto"}

Per ulteriori informazioni sulla raccolta dei dati, consulta [panoramica sulla raccolta dati](../../tags/home.md).

## Identity Service {#identity-service}

Adobe Experience Platform Identity Service offre una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti dell’interfaccia utente di Identity Service | Utilizza lo strumento di creazione dello spazio dei nomi personalizzato migliorato nell’interfaccia utente di Experienci Platform per gestire meglio gli spazi dei nomi personalizzati e i corrispondenti tipi di identità. L’interfaccia utente avanzata del servizio Identity offre: <ul><li>Esperienza contestuale: suggerimenti visivi, chiarezza e contesto per definire lo spazio dei nomi e i tipi di identità.</li><li>Precisione: è stata migliorata la gestione degli errori, senza più nomi di identità duplicati.</li><li>Discoverability: accesso alla documentazione da una finestra di dialogo interna al prodotto.</li></ul> Per ulteriori informazioni, consulta la guida su [creazione di spazi dei nomi personalizzati](../../identity-service/namespaces.md#create-namespaces). |
| Modifiche ai limiti del grafo delle identità | Il limite del grafico delle identità è cambiato da 150 a 50. Quando una nuova identità viene acquisita in un grafico completo, l’identità meno recente in base alla marca temporale e al tipo di identità dell’acquisizione viene eliminata. Ai tipi di identità dei cookie viene assegnata una priorità per l’eliminazione. Contatta il team dell’account Adobe per richiedere una modifica nel tipo di identità se la sandbox di produzione contiene: <ul><li>uno spazio dei nomi personalizzato in cui gli identificatori della persona (come gli ID del sistema di gestione delle relazioni con i clienti) sono configurati come tipo di identità cookie/dispositivo.</li><li>uno spazio dei nomi personalizzato in cui gli identificatori cookie/dispositivo sono configurati come tipo di identità tra dispositivi.</li></ul> Queste richieste verranno elaborate manualmente da Adobe Engineering. Per ulteriori informazioni, leggere [guardrail per i dati del servizio Identity](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sul servizio Identity, consulta [Panoramica del servizio Identity](../../identity-service/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Colonne personalizzabili | Ora puoi personalizzare il layout di Audience Portal con colonne ridimensionabili. Per ulteriori informazioni su questa funzione, leggere [guida all’interfaccia utente di segmentazione](../../segmentation/ui/overview.md#customize). |
| Aggiorna raggruppamento frequenza | Ora puoi visualizzare un raggruppamento delle frequenze di aggiornamento dei tipi di pubblico nell’organizzazione. Per ulteriori informazioni su questa funzione, leggere [guida all’interfaccia utente di segmentazione](../../segmentation/ui/overview.md#browse). |

Per ulteriori informazioni sulle origini, leggere la [panoramica sulle origini](../../sources/home.md).

Per ulteriori informazioni sul servizio di segmentazione, consulta [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovi parametri per `offset` impaginazione in origini self-service (SDK batch) | Ora puoi specificare un `endConditionName` e `endConditionValue` per l’origine quando si utilizza `offset` impaginazione. Questi parametri ti consentono di indicare la condizione che terminerà il ciclo di paginazione nella successiva richiesta HTTP. Per ulteriori informazioni, leggere [guida all’impaginazione per le origini self-service (SDK batch)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere la [panoramica sulle origini](../../sources/home.md).