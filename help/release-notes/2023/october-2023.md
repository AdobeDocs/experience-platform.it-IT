---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2023
description: Note sulla versione di Adobe Experience Platform di ottobre 2023.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: d6e306294d0a119108e2de7ba03ebed4f633fba1
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 39%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 ottobre 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

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
| Metriche di utilizzo delle destinazioni | Sono state aggiunte nuove metriche di misurazione al dashboard Utilizzo licenze. Le metriche **[!UICONTROL Dimensione Audience Activation]** e **[!UICONTROL Dimensione esportazione dati]** consentono di tenere traccia della quantità di dati esportati fuori da Platform in relazione ai diritti di utilizzo della licenza. Per le descrizioni di queste e di altre metriche di utilizzo della licenza, consulta la documentazione delle [metriche disponibili](../../dashboards/guides/license-usage.md#available-metrics). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Estensioni | Miglioramento API conversioni [!DNL Meta] | Sono disponibili tre miglioramenti all&#39;estensione [Meta Conversions API](/help/tags/extensions/server/meta/overview.md): <ul><li>Integrazione con [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crea un&#39;esperienza di accesso fluida consentendo di condividere il pixelID e il token di accesso per l&#39;integrazione dell&#39;API di conversione con Adobe.</li><li>Integrazione con [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): consente di inviare annunci pubblicitari a persone che hanno più probabilità di completare un&#39;azione desiderata e collegarla nuovamente agli annunci consegnati.</li><li>Integrazione con [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): consente di trasmettere il RampID di LiveRamp nel campo CIP, eliminando la necessità di condividere i dati PII direttamente con i partner o con Meta. </li></ul> |
| Estensioni | API per conversioni [!DNL LinkedIn] | L&#39;estensione [[!DNL LinkedIn] Conversions API](../../tags/extensions/server/linkedin/overview.md) consente di valutare l&#39;efficacia delle campagne di marketing LinkedIn inoltrando i dati dell&#39;evento Experience Platform a LinkedIn. |
| Segreto | [!DNL LinkedIn] segreto OAuth 2 | Il segreto [[!DNL LinkedIn] OAuth 2](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) ti consente di inviare interazioni server-server a [!DNL LinkedIn] nell&#39;inoltro degli eventi. |
| Inoltro eventi | Aggiornamento dei tag e inoltro degli eventi | Per mantenere le prestazioni di [Tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it) e [Inoltro eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) in Platform, verranno mantenute solo le build di sviluppo e staging più recenti, sia riuscite che non riuscite. Tutte le build non più in uso verranno rimosse. Inoltre, è stata implementata una limitazione della velocità e della limitazione di limitazione per garantire che alcuni utilizzi API pesanti non danneggino le prestazioni API di altri. |
| Estensioni | Elementi, regole ed estensioni | [Gli elementi, le regole e le estensioni](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) sono ora ordinati nell&#39;output della libreria per garantire una maggiore coerenza tra più build e distribuzioni della stessa libreria. |

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
| (Beta) Supporto delle funzioni di hashing nei campi calcolati | Oltre alle funzioni specifiche per [esportare array](../../destinations/ui/export-arrays-calculated-fields.md) o elementi da un array, è ora possibile utilizzare ulteriori [funzioni di hashing](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) per eseguire l&#39;hashing degli attributi nei file esportati. Le funzioni di hashing supportate sono: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (GA limitato) Attiva i tipi di pubblico dell’account su determinate destinazioni | I clienti B2B di Real-Time CDP ora possono attivare [tipi di pubblico dell&#39;account](../../segmentation/ui/account-audiences.md) in determinate destinazioni. Per ulteriori informazioni su questa funzione, leggere l&#39;esercitazione [attivare il pubblico dell&#39;account](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza di Platform in ambienti virtuali separati, utili per le attività di sviluppo e evoluzione delle applicazioni di esperienza digitale.

**Nuova funzione**

| Funzione | Descrizione |
| --- | --- |
| Strumenti sandbox | La funzione di strumenti sandbox consente di migliorare la precisione della configurazione tra le sandbox ed esportare e importare facilmente le configurazioni sandbox tra di esse. È possibile utilizzare la funzione degli strumenti sandbox per selezionare oggetti diversi ed esportarli in un pacchetto. Per ulteriori informazioni, consulta la [guida dell&#39;interfaccia utente per gli strumenti della sandbox](../../sandboxes/ui/sandbox-tooling.md). |

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Nuova funzione**

| Funzione | Descrizione |
| ------- | ----------- |
| Pubblico dell’account (GA limitato) | In Real-time Customer Data Platform B2B edition, ora puoi utilizzare la segmentazione dell’account per rendere l’esperienza di segmentazione di marketing completamente semplice e sofisticata, dal pubblico basato sulle persone a quello basato sull’account. Per ulteriori informazioni su questa funzione, leggere la [panoramica sui tipi di pubblico dell&#39;account](../../segmentation/ui/account-audiences.md). |

Per ulteriori informazioni sul servizio di segmentazione, leggere la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Autenticazione aggiornata per Data Landing Zone | Visualizzando le credenziali, ora puoi vedere la data di scadenza designata per la Data Landing Zone. Per continuare a utilizzare il token nell’applicazione, è necessario aggiornarlo prima della data di scadenza. Se non aggiorni manualmente il token prima della data di scadenza dichiarata, al successivo recupero delle credenziali verrà automaticamente aggiornato e verrà fornito un nuovo token. Per ulteriori informazioni, consulta la documentazione su [utilizzo della Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere la [panoramica delle origini](../../sources/home.md).
