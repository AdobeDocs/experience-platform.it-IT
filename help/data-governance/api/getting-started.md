---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori API di DULE Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Guida per gli sviluppatori API di DULE Policy Service

L’etichettatura e l’applicazione dell’uso dei dati (DULE) è il meccanismo fondamentale di governance dei dati della piattaforma Adobe Experience. Il servizio DULE Policy Service fornisce un&#39;API RESTful che consente di creare e gestire i criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere eseguite rispetto ai dati etichettati con determinate etichette di utilizzo dei dati.

Questo documento fornisce istruzioni per l&#39;esecuzione delle operazioni chiave disponibili nell&#39;API del servizio criteri. Se non l&#39;avete ancora fatto, potete iniziare rivedendo la panoramica [sulla governance dei](../home.md) dati per acquisire dimestichezza con il framework DULE. Per istruzioni dettagliate sulla creazione e l&#39;applicazione di criteri DULE, vedete l&#39;esercitazione [sulla politica](../policies/create.md)DULE.

Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all&#39;API del servizio criteri.

## Guida introduttiva a DULE Policy Service

Prima di iniziare a lavorare con il servizio Criteri, i dati su Experience Platform devono disporre di etichette DULE appropriate. Istruzioni dettagliate per l&#39;applicazione delle etichette di utilizzo dei dati ai set di dati e ai campi sono disponibili nella guida [utente delle etichette](../labels/user-guide.md)DULE.

## Prerequisiti

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Governance](../home.md)dei dati: Il framework tramite il quale Experience Platform applica la conformità all’utilizzo dei dati.
   * [Etichette](../labels/overview.md)DULE: Le etichette di utilizzo dei dati vengono applicate ai campi di dati XDM (Experience Data Model), specificando le restrizioni per l&#39;accesso ai dati.
* [Sistema](../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
* [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform, comprese quelle appartenenti a Data Governance, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Risorse Core e personalizzate

All&#39;interno dell&#39;API del servizio criteri, tutti i criteri e le azioni di marketing sono denominati o `core` `custom` risorse.

Le `core` risorse sono quelle definite e gestite da Adobe, mentre `custom` le risorse vengono create e gestite da singoli clienti e sono pertanto univoche e visibili esclusivamente all&#39;organizzazione IMS che le ha create. Di conseguenza, le operazioni di elenco e ricerca (`GET`) sono le uniche operazioni consentite sulle `core` risorse, mentre le operazioni di elenco, ricerca e aggiornamento (`POST`, `PUT`, `PATCH`e `DELETE`) sono disponibili per `custom` le risorse.

## Stato dei criteri

I criteri di utilizzo dei dati possono avere uno dei tre stati possibili: `DRAFT`, `ENABLED`o `DISABLED`.

Per impostazione predefinita, solo le politiche &quot;ENABLED&quot; partecipano alla valutazione delle politiche.

I criteri &quot;DRAFT&quot; possono essere considerati anche nella valutazione dei criteri, ma solo impostando il parametro della query `?includeDraft=true`. Ulteriori informazioni sulla valutazione delle politiche sono reperibili nel documento relativo all&#39;applicazione delle [politiche](../enforcement/overview.md) alla fine del presente documento.

## Nomi delle azioni di marketing {#marketing-actions}

I nomi delle azioni di marketing sono identificatori univoci per le azioni di marketing. Ogni azione `core` di marketing ha un nome univoco che si applica a tutte le organizzazioni IMS. Questi nomi sono definiti e gestiti da Adobe. Nel frattempo, tutte le azioni di marketing (`custom` risorse) definite dal cliente sono univoche all&#39;interno della vostra organizzazione e non sono visibili o condivise con altre organizzazioni IMS.

I passaggi per l&#39;utilizzo delle azioni di marketing nell&#39;API di Policy Service sono descritti nella sezione Azioni [di](#marketing-actions) marketing più avanti in questo documento.

## Passaggi successivi

Ora che disponete delle conoscenze e delle credenziali preliminari, potete continuare a leggere le chiamate API di esempio fornite in questa guida per gli sviluppatori:

* [Azioni di marketing](marketing-actions.md)
* [Criteri](policies.md)