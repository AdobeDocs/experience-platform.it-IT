---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di ottobre 2023 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4ab89ef7cabc9d808fd9dab24b6dbe3fe23e53f3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 35%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 ottobre 2023**

Aggiornamenti alle funzioni esistenti in Experience Platform:

- [Raccolta dati](#data-collection)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Estensione | [!DNL Meta] Miglioramento API per le conversioni | Sono disponibili tre miglioramenti al [API di metaconversione](/help/tags/extensions/server/meta/overview.md) estensione: <ul><li>Integrazione con [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crea un’esperienza di accesso fluida consentendoti di condividere il pixelID e il token di accesso per l’integrazione API di conversione con Adobe.</li><li>Integrazione con [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): consente di inviare annunci pubblicitari a persone che hanno più probabilità di completare un’azione desiderata e di ricollegare l’azione agli annunci consegnati.</li><li>Integrazione con [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): consente di trasmettere la RampID di LiveRamp nel campo CIP, eliminando la necessità di condividere i dati PII direttamente con i partner o con Meta. </li></ul> |

Per ulteriori informazioni sulla raccolta dati, consulta la [panoramica sulla raccolta dati](../../tags/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experienci Platform fornisce sandbox che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Nuova funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Strumenti sandbox | La funzione di strumenti sandbox consente di migliorare la precisione della configurazione tra le sandbox ed esportare e importare facilmente le configurazioni sandbox tra di esse. È possibile utilizzare la funzione degli strumenti sandbox per selezionare oggetti diversi ed esportarli in un pacchetto. Per ulteriori informazioni, vedere [guida dell’interfaccia utente per gli strumenti della sandbox](../../sandboxes/ui/sandbox-tooling.md). |

Per ulteriori informazioni sulle sandbox, consulta [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Nuova funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Pubblico dell’account (GA limitato) | In Real-time Customer Data Platform B2B Edition, è ora possibile utilizzare la segmentazione dell’account per portare la piena facilità e sofisticatezza dell’esperienza di segmentazione di marketing da tipi di pubblico basati sulle persone a tipi di pubblico basati sull’account. Per ulteriori informazioni su questa funzione, leggere [panoramica sui tipi di pubblico dell’account](../../segmentation/ui/account-audiences.md). |

Per ulteriori informazioni sul servizio di segmentazione, consulta [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Autenticazione aggiornata per Data Landing Zone | Visualizzando le credenziali, ora puoi vedere la data di scadenza designata per la Data Landing Zone. Per continuare a utilizzare il token nell’applicazione, è necessario aggiornarlo prima della data di scadenza. Se non aggiorni manualmente il token prima della data di scadenza dichiarata, al successivo recupero delle credenziali verrà automaticamente aggiornato e verrà fornito un nuovo token. Per ulteriori informazioni, consulta la documentazione su [utilizzo della Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere la [panoramica sulle origini](../../sources/home.md).
