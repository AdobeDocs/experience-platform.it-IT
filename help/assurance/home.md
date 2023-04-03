---
title: Panoramica di Adobe Experience Platform Assurance
description: Adobe Experience Platform Assurance ti consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze all’interno delle tue applicazioni mobili.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance è un prodotto di [Adobe Experience Cloud](https://www.adobe.com/it/experience-cloud.html) per aiutarti a controllare, verificare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze nella tua app mobile.

>[!IMPORTANT]
>
> Il Griffon del progetto è ora noto come **Affidabilità**!
>
> Il Griffon del progetto è ora disponibile al pubblico per **tutto** Clienti Adobe Experience Cloud come garanzia. Per ulteriori informazioni su questa transizione, consulta la sezione [guida all’accesso utente](./user-access.md).

>[!INFO]
>
>Sono disponibili le API pubbliche di assicurazione.
>
>[API di garanzia](https://developer.adobe.com/adobe-assurance-public-apis/) sono una raccolta di API che consentono agli utenti di testare ed eseguire il debug delle app web e mobili, se equipaggiate con Adobe Assurance Mobile SDK.

## Disponibilità generale

A partire dal 15 ottobre 2022, Assurance è generalmente disponibile per tutti i Adobe Experience Cloud.

### Cosa sta cambiando?

Il 15 ottobre - l&#39;accesso a Assurance sarà gestito tramite Admin Console. Per piacere, leggi le [guida all’accesso utente](./user-access.md) per continuare ad avere accesso ininterrotto.

Non sono previste altre modifiche o interruzioni per le integrazioni, le sessioni e gli eventi di Assurance esistenti. L&#39;accesso alla garanzia può essere continuato tramite [https://griffon.adobe.com](https://griffon.adobe.com) **o** è possibile utilizzare (e segnalibro) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Cosa può fare Assurance per te?

### Configurazione rapida

Inizia subito con poche righe di codice. Per le app mobili, Assurance funziona con l’SDK di Adobe Experience Platform Mobile per aiutarti a ispezionare, simulare e convalidare gli eventi delle app, i segnali di posizione, i parametri di configurazione, i registri SDK, le informazioni sul dispositivo e altro ancora.

### Connessione senza problemi

Con Assurance, la connessione dell’app a Platform è semplice e affidabile. Non è necessario utilizzare proxy di rete, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) e altre ginnastiche di rete - collegare la tua app a Assurance è facile quanto scannerizzare un codice QR o toccare un pulsante.

![](./images/index/no-hassle-connection.png)

### Ispezione, simulazione e convalida in tempo reale

Dopo aver effettuato la connessione a Assurance, puoi controllare gli eventi e le attività delle app in streaming live e filtrare e cercare per eliminare il rumore. Gli eventi contengono dettagli sulla convalida, il debug e la risoluzione dei problemi relativi all’implementazione dell’app mobile. L&#39;affidabilità consente inoltre di visualizzare le immagini, simulare i segnali di posizione e altro in tempo reale.

![](./images/index/real-time-insepction.png)

### Integrazione con Adobe Experience Cloud

I dati e le esperienze lato client sono contestuali in base alle modalità con cui gli utenti impostano regole di reporting, attività e campagne sulle interfacce utente incentrate sull’addetto al marketing. Per aiutarti a collegare i punti tra i due, stiamo integrando con soluzioni Adobe Experience Cloud come Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service e altro ancora.

![](./images/index/integration.png)

## Funzioni

### Eventi, registri e altro ancora dell’SDK di Adobe Experience Platform Mobile

Questa funzione consente di controllare gli eventi SDK non elaborati generati dall’SDK di Adobe Experience Platform Mobile. Tutti gli eventi raccolti dall’SDK sono disponibili per l’ispezione. Gli eventi SDK vengono caricati in una vista a elenco, ordinati per ora. Ogni evento ha una visualizzazione dettagliata che fornisce ulteriori dettagli. Sono inoltre disponibili visualizzazioni aggiuntive per sfogliare la configurazione SDK, gli elementi dati, gli stati condivisi e le versioni di estensione SDK.

### Adobe Analytics

La visualizzazione Adobe Analytics > Eventi di Analytics è una visualizzazione mirata che mostra gli eventi relativi all’implementazione mobile di Adobe Analytics. La vista a elenco mostra gli eventi del ciclo di vita o dell&#39;azione/stato, &quot;stato&quot; post-elaborazione, insieme ai dettagli dell&#39;evento richiesti in una visualizzazione formattata appositamente. Lo stato post-elaborazione mostra come l’evento è stato elaborato da Adobe Analytics dopo l’applicazione delle regole di elaborazione sull’evento.

### Adobe Analytics per contenuti in streaming

La vista Eventi di Adobe Analytics > Media Analytics mostra gli eventi per l’implementazione di analisi audio e video. La visualizzazione dettagliata degli eventi mostra i metadati standard e personalizzati tracciati per ogni sessione di riproduzione. Inoltre, puoi visualizzare lo stato post-elaborato e i dati di analisi dei contenuti multimediali post-elaborati, ad esempio il tempo trascorso per i file multimediali o la durata totale del buffer.

### Luoghi (servizi ubicazione)

La visualizzazione Servizi posizione è una visualizzazione sul dispositivo che mostra gli eventi di ingresso e uscita della posizione dell’utente per facilitarne la convalida. Questa pratica visualizzazione fornisce un’interfaccia utile per visualizzare punti dati specifici della posizione da controllare sul client per il debug nel contesto.

## La garanzia è sicura?

Assicurazione ha in atto le seguenti misure di sicurezza:

* Sia l&#39;interfaccia utente Web di Assurance che quella di Assurance dispongono di un handshake sicuro basato su PIN per una connessione. L&#39;utente deve creare esplicitamente un handshake, che impedisce la creazione di connessioni &quot;accidentali&quot; di Assurance da parte di un utente finale.
* Sono supportate solo le connessioni tra l’interfaccia web Assurance e l’interfaccia utente Web Assurance appartenente allo stesso ID organizzazione Adobe Experience Cloud.
* Gli eventi SDK di Adobe Experience Platform Mobile vengono trasportati tramite HTTPS.
* Gli SDK per dispositivi mobili Assurance e Adobe Experience Platform utilizzano TLS 1.2
* Le sessioni di affidabilità vengono eliminate dopo 30 giorni.
* I dati della sessione di garanzia vengono crittografati durante il riposo, seguendo le best practice relative all’archiviazione.

## Introduzione

Per configurare Assurance, devi prima installare l&#39;estensione Assurance nell&#39;applicazione. Per informazioni su come eseguire questa operazione, leggi l’esercitazione su [implementazione dell’estensione Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Dopo aver aggiunto Assurance all&#39;app, puoi creare una sessione di verifica che può essere connessa al tuo dispositivo. Per informazioni su come utilizzare Assurance, leggere il [guida all’utilizzo di Assurance](./tutorials/using-assurance.md).
