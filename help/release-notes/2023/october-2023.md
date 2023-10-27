---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di ottobre 2023 per Adobe Experience Platform.
source-git-commit: fc0cb582d74f5ab52410991f65aa14ba05df3f97
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 34%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 ottobre 2023**

Aggiornamenti alle funzioni esistenti in Experience Platform:

- [Dashboard](#dashboards)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Metriche di utilizzo delle destinazioni | Sono state aggiunte nuove metriche di misurazione al dashboard Utilizzo licenze. Il **[!UICONTROL Dimensione Audience Activation]** e **[!UICONTROL Dimensione esportazione dati]** Le metriche consentono di tenere traccia della quantità di dati esportati al di fuori di Platform in relazione ai diritti di utilizzo della licenza. Consulta la [metriche disponibili](../../dashboards/guides/license-usage.md#available-metrics) la documentazione per le descrizioni di questi e di altre metriche di utilizzo della licenza. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Estensione | [!DNL Meta] Miglioramento API per le conversioni | Sono disponibili tre miglioramenti al [API di metaconversione](/help/tags/extensions/server/meta/overview.md) estensione: <ul><li>Integrazione con [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crea un’esperienza di accesso fluida consentendoti di condividere il pixelID e il token di accesso per l’integrazione API di conversione con Adobe.</li><li>Integrazione con [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): consente di inviare annunci pubblicitari a persone che hanno più probabilità di completare un’azione desiderata e di ricollegare l’azione agli annunci consegnati.</li><li>Integrazione con [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): consente di trasmettere la RampID di LiveRamp nel campo CIP, eliminando la necessità di condividere i dati PII direttamente con i partner o con Meta. </li></ul> |
| Estensione | [!DNL LinkedIn] API di conversione | Il [[!DNL LinkedIn] API di conversione](../../tags/extensions/server/linkedin/overview.md) L’estensione consente di valutare l’efficacia delle campagne di marketing LinkedIn inoltrando i dati dell’evento Experienci Platform a LinkedIn. |
| Segreto | [!DNL LinkedIn] Segreto OAuth 2 | Il [[!DNL LinkedIn] Segreto OAuth 2](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) consente di inviare interazioni server-server a [!DNL LinkedIn] nell’inoltro degli eventi. |

Per ulteriori informazioni sulla raccolta dati, consulta la [panoramica sulla raccolta dati](../../tags/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Nuova o aggiornata | Descrizione |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nuova | Utilizza la destinazione Moengagement per connettere e mappare i dati di Adobe (attributi utente, segmenti ed eventi) con MoEngage in tempo reale. I clienti possono quindi agire su questi dati, distribuendo esperienze personalizzate e mirate. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nuova | Utilizza l’aggregazione di più fonti di dati operativi in Adobe Experience Platform come input in Qualtrics Experience ID per comprendere meglio i tuoi clienti e consentire un’attività di sensibilizzazione mirata per colmare il divario quando si tratta di comprendere le intenzioni, le emozioni e i fattori che stimolano l’esperienza. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto delle funzioni di hashing nei campi calcolati | Oltre alle funzioni specifiche per [esportazione di array](../../destinations/ui/export-arrays-calculated-fields.md) o da un array, è ora possibile utilizzare [funzioni di hashing](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) per eseguire l&#39;hashing degli attributi nei file esportati. Le funzioni di hashing supportate sono: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (GA limitato) Attiva i tipi di pubblico dell’account su determinate destinazioni | I clienti B2B di Real-Time CDP ora possono attivare [pubblico dell’account](../../segmentation/ui/account-audiences.md) verso determinate destinazioni. Per ulteriori informazioni su questa funzione, leggere [tutorial attivare il pubblico dell’account](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

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
