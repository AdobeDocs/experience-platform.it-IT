---
title: Note sulla versione di Adobe Experience Platform, giugno 2024
description: Note sulla versione di Adobe Experience Platform di giugno 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e1b56c6150274748c35fedfc1e1b6bbbf66d1bfb
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 20%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giugno 2024**

>[!TIP]
>
>[Assistente AI nell’Experience Platform](https://platform.adobe.com) è ora disponibile. Utilizza l’Assistente AI per accelerare i flussi di lavoro nelle applicazioni Adobe. [Ulteriori informazioni](#ai-assistant) sulle nuove funzionalità.

Nuove funzioni di Adobe Experience Platform:

- [Assistente IA](#ai-assistant)
- [Autenticazione per le API di Experience Platform](#authentication-platform-apis)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Privacy Service](#privacy)
- [Servizio di segmentazione](#segmentation)
- [Usare i playbook sui casi d’uso](#use-case-playbooks)

## Assistente IA {#ai-assistant}

L’Assistente AI in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente AI per comprendere meglio la conoscenza del prodotto, risolvere i problemi o eseguire ricerche attraverso le informazioni e trovare informazioni operative. L’Assistente AI supporta Experienci Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Nuova funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Assistente AI nell’Experience Platform | Ora puoi utilizzare l’Assistente AI in Experienci Platform. L’Assistente AI supporta Experienci Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics. <br> ![Assistente AI in Experience Platform.](../2024/assets/june/ai-assistant-full.png "Assistente AI in Experience Platform."){width="100" zoomable="yes"} <br> Per ulteriori informazioni su questa funzione, leggere [Guida all’interfaccia utente di Assistente IA](../../ai-assistant/ui-guide.md). |
| Supporto per le domande relative alla conoscenza del prodotto | [Conoscenza del prodotto](../../ai-assistant/home.md#product-knowledge) sono concetti e argomenti basati sulla documentazione di Experience League e possono essere utilizzati per l’apprendimento mirato, l’individuazione aperta e la risoluzione dei problemi. Puoi porre domande sulla conoscenza del prodotto di AI Assistant come: <ul><li>Cosa sono i tipi di pubblico simili?</li><li>Come viene calcolata la ricchezza del profilo?</li><li> Posso eliminare uno schema abilitato per il profilo dopo l’acquisizione dei dati?</li></ul> |
| [!BADGE Beta]Supporto {type=Informative} per domande di approfondimenti operativi | [Informazioni operative](../../ai-assistant/home.md#operational-insights) sono le risposte che l’Assistente AI genera sugli oggetti di metadati, inclusi i conteggi, le ricerche e l’impatto sulla derivazione. Gli approfondimenti operativi non esaminano alcun dato all’interno della sandbox. Puoi porre all’Assistente AI domande di approfondimenti operativi come: <ul><li>Quali destinazioni sono in uno stato attivo?</li><li>Quanti set di dati ho?</li><li>Elencare i tipi di pubblico utilizzati nei percorsi live.</li></ul> Le informazioni operative sono supportate nei seguenti domini: attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, percorsi, schemi e origini. |
| Accedi all’Assistente di AI | Per accedere all’Assistente all’intelligenza artificiale, ad Experience Platform Real-Time CDP e Journey Optimizer, devi essere aggiunto a un ruolo che includa **Abilita Assistente IA** e **Visualizza informazioni operative** autorizzazioni. Per ulteriori informazioni, leggere [guida all’accesso alle funzioni](../../ai-assistant/access.md). Utilizza l’Admin Console per [accesso nel Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

Per ulteriori informazioni sull&#39;Assistente di intelligenza artificiale, leggere [Panoramica dell’Assistente AI](../../ai-assistant/home.md).

## Autenticazione per le API di Experience Platform {#authentication-platform-apis}

Il metodo JWT per ottenere i token di accesso è ora obsoleto per le nuove integrazioni e sostituito da un metodo di autenticazione server-to-server OAuth più semplice.<p>![Quello evidenziato è il nuovo metodo di autenticazione OAuth per ottenere i token di accesso.](/help/landing/images/api-authentication/oauth-authentication-method.png "Quello evidenziato è il nuovo metodo di autenticazione OAuth per ottenere i token di accesso."){width="100" zoomable="yes"}</p>

Anche se le integrazioni API esistenti che utilizzano il metodo di autenticazione JWT continueranno a funzionare fino al 1° gennaio 2025, Adobe consiglia vivamente di migrare le integrazioni esistenti al nuovo metodo server-to-server OAuth prima di tale data. Leggi la guida sulla [migrazione dalle credenziali dell’account di servizio (JWT) alle credenziali server-to-server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

## Preparazione dati (#data-prep)

Utilizza la preparazione dati per mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiunte all&#39;elenco delle parole chiave riservate | Le parole seguenti sono state aggiunte all’elenco delle parole chiave riservate della preparazione dati:<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul>. Per ulteriori informazioni, leggere la [guida alle funzioni di preparazione dei dati](../../data-prep/functions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulla preparazione dati, consulta [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Miglioramento dell’API di esportazione ad hoc per esportare pubblici esterni | Ora puoi utilizzare l’API di esportazione ad hoc per esportare i tipi di pubblico esterni (caricamento personalizzato). [Ulteriori informazioni](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta) Funzioni aggiuntive supportate nella fase beta del supporto dell&#39;array di esportazione | In precedenza, quando si attivavano i tipi di pubblico su destinazioni basate su file e si selezionava Usa campo calcolato, era limitato all’utilizzo di un sottoinsieme dei tipi di pubblico disponibili tramite la preparazione dati. Tale limite è stato ora rimosso e i clienti hanno accesso a tutte le funzioni disponibili tramite la preparazione dati quando esportano tipi di pubblico in destinazioni basate su file. [Ulteriori informazioni](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions). |
| Mostra solo i campi con dati nel passaggio di mappatura | Quando mappi gli attributi del profilo alle destinazioni, ora puoi alternare tra tutti gli attributi del profilo o solo quelli che contengono dati. Per impostazione predefinita, vengono visualizzati solo i campi con i dati. Consulta le guide all’attivazione per [batch](../../destinations/ui/activate-batch-profile-destinations.md#mapping) e [streaming](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) destinazioni per ulteriori dettagli. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Diverse normative legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi di dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto Privacy Service per Adobe Journey Optimizer | Le funzionalità di Privacy Service sono ora compatibili con i protocolli Adobe Journey Optimizer per l’elaborazione delle richieste di eliminazione. Consulta la [Documentazione sulle richieste di privacy di Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) per ulteriori informazioni, o la documentazione di Experience Platform per un elenco di [Applicazioni di Experience Cloud integrate con Privacy Service](../../privacy-service/experience-cloud-apps.md). |

Consulta la [Panoramica di Privacy Service](../../privacy-service/home.md) per ulteriori informazioni sul servizio.

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dei vincoli di tempo | Il comportamento per &quot;Questo mese&quot; e &quot;Quest’anno&quot; è stato aggiornato e ora rappresentano rispettivamente &quot;il mese corrente&quot; e &quot;l’anno corrente&quot;. Per ulteriori informazioni su questa modifica, leggere [Guida al Generatore di segmenti](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Usare i playbook sui casi d’uso {#use-case-playbooks}

[!DNL Use Case Playbooks] sono disponibili senza costi aggiuntivi per tutti i clienti Adobe Experience Platform. Per accedere a una raccolta completa di playbook di casi d’uso nell’interfaccia utente di Experienci Platform, ora puoi selezionare **[!UICONTROL Playbook]** dal menu di navigazione a sinistra.

[!DNL Use Case Playbooks] sono progettati per aiutare a superare le sfide quando si inizia con Real-time Customer Data Platform o Adobe Journey Optimizer. Offrono indicazioni e generano varie risorse che puoi testare e importare negli ambienti di produzione quando sei pronto, anche se non sei sicuro su dove iniziare o su come produrre le risorse corrette per i casi d’uso previsti.

Per iniziare, leggi [Panoramica sui playbook di casi d’uso](/help/use-case-playbooks/playbooks/overview.md), che fornisce una panoramica delle funzionalità dei playbook, del loro scopo e una dimostrazione end-to-end, tra cui come creare istanze e importare risorse generate in altri ambienti sandbox.

Per scoprire come accedere e impostare una sandbox ispiratrice per sperimentare ed esplorare vari playbook di casi d’uso, consulta [Scopri il playbook corretto](/help/use-case-playbooks/playbooks/discover.md) documento.

Per ulteriori informazioni su [!DNL Use Case Playbooks], leggi le seguenti pagine della documentazione:

- Ottieni un elenco di tutti [playbook disponibili](/help/use-case-playbooks/playbooks/playbooks-list.md), raggruppati per prodotto (Real-Time CDP o Journey Optimizer).
- Scopri cosa [autorizzazioni](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) sono necessari per utilizzare i playbook e le risorse che creano.
- Comprendere la [funzionalità di riconoscimento dei dati](/help/use-case-playbooks/playbooks/data-awareness.md) che consente di duplicare le risorse generate in altri ambienti sandbox.
