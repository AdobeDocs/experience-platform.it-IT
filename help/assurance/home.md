---
title: Panoramica di Adobe Experience Platform Assurance
description: Adobe Experience Platform Assurance consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze all’interno delle tue applicazioni mobili.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance è un prodotto di [Adobe Experience Cloud](https://www.adobe.com/it/experience-cloud.html) per aiutarti a ispezionare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze nella tua app mobile.

>[!IMPORTANT]
>
> Il progetto Griffon è ora noto come **Assurance**!
>
> Il progetto Griffon è ora generalmente disponibile per **tutto** Clienti Adobe Experience Cloud come Assurance. Per ulteriori informazioni su questa transizione, leggi la sezione [guida all’accesso utente](./user-access.md).

>[!INFO]
>
>Le API pubbliche di Assurance sono disponibili.
>
>[API di Assurance](https://developer.adobe.com/adobe-assurance-public-apis/) sono una raccolta di API che consentono agli utenti di testare ed eseguire il debug delle proprie app web e mobili, se dotate dell’SDK Adobe Assurance Mobile.

## Disponibilità generale

A partire dal 15 ottobre 2022, Assurance è generalmente disponibile per tutti i Adobe Experience Cloud.

### Cosa sta cambiando?

Il 15 ottobre - l&#39;accesso ad Assurance sarà gestito tramite Admin Console. Leggi le [guida all’accesso utente](./user-access.md) per garantire un accesso ininterrotto.

Non sono previste altre modifiche o interruzioni per integrazioni, sessioni ed eventi Assurance esistenti. È possibile continuare ad accedere ad Assurance tramite [https://griffon.adobe.com](https://griffon.adobe.com) **o** è possibile utilizzare (e un segnalibro) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Cosa può fare Assurance per te?

### Configurazione rapida

Inizia in fretta con poche righe di codice. Per le app per dispositivi mobili, Assurance collabora con l’SDK di Adobe Experience Platform Mobile per aiutarti a verificare, simulare e convalidare eventi dell’app, segnali di posizione, parametri di configurazione, registri SDK, informazioni sul dispositivo e altro ancora.

### Connessione senza problemi

Con Assurance, collegare l’app a Platform è semplice e affidabile. Non è necessario utilizzare proxy di rete, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)), e altri tipi di ginnastica in rete: collegare l&#39;app ad Assurance è facile come scansionare un codice QR o toccare un pulsante.

![](./images/index/no-hassle-connection.png)

### Ispezione, simulazione e convalida in tempo reale

Dopo aver effettuato la connessione ad Assurance, puoi esaminare gli eventi dell’app in diretta streaming e le attività, filtrare e cercare per eliminare il rumore. Gli eventi contengono dettagli su come convalidare, eseguire il debug e risolvere i problemi relativi all’implementazione dell’app mobile. Assurance consente inoltre di visualizzare schermate, simulare segnali di posizione e altro ancora in tempo reale.

![](./images/index/real-time-insepction.png)

### Integrazione con Adobe Experience Cloud

I dati e le esperienze lato client vengono contestualizzati in base al modo in cui gli utenti configurano regole di reporting, attività e campagne sulle interfacce utente mirate agli addetti al marketing. Per aiutarti a collegare i punti tra i due, stiamo integrando con soluzioni Adobe Experience Cloud come Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service e altro ancora.

![](./images/index/integration.png)

## Funzioni

### Eventi, registri e altro ancora dell’SDK di Adobe Experience Platform Mobile

Assurance consente di esaminare gli eventi SDK non elaborati generati dall’SDK di Adobe Experience Platform Mobile. Tutti gli eventi raccolti dall’SDK sono disponibili per l’ispezione. Gli eventi SDK vengono caricati in una vista a elenco, ordinati in base all’ora. Ogni evento ha una vista dettagliata che fornisce ulteriori dettagli. Sono inoltre disponibili viste aggiuntive per sfogliare la configurazione dell’SDK, gli elementi dati, gli stati condivisi e le versioni delle estensioni SDK.

### Adobe Analytics

La vista Adobe Analytics > Eventi di Analytics è una vista mirata che mostra gli eventi relativi alla tua implementazione Adobe Analytics per dispositivi mobili. La vista a elenco mostra gli eventi del ciclo di vita o dell’azione/stato, &quot;stato&quot; post-elaborato, insieme ai dettagli dell’evento richiesti in una vista con un formato speciale. Lo stato Post-elaborazione mostra il modo in cui l’evento è stato elaborato da Adobe Analytics dopo l’applicazione delle regole di elaborazione all’evento.

### Adobe Analytics per contenuti in streaming

La vista Adobe Analytics > Eventi di Media Analytics mostra gli eventi per l’implementazione di analisi audio e video. La vista dei dettagli degli eventi mostra i metadati standard e personalizzati tracciati per ogni sessione di riproduzione. Inoltre, puoi visualizzare lo stato post-elaborazione e i dati di analisi dei contenuti multimediali post-elaborazione, ad esempio il tempo trascorso sui contenuti multimediali o la durata totale del buffer.

### Luoghi (Location Services)

La vista Servizi posizione è una vista su dispositivo che mostra gli eventi di entrata e uscita della posizione dell’utente per una facile convalida. Questa pratica vista fornisce una comoda interfaccia per visualizzare punti dati specifici della posizione per l&#39;ispezione sul client per il debug nel contesto.

## Assurance è sicuro?

Assurance dispone delle seguenti misure di sicurezza:

* Sia Assurance che l&#39;interfaccia utente Web Assurance dispongono di un handshake protetto basato su PIN per una connessione. L’utente deve creare esplicitamente un handshake che impedisce a un utente finale di creare connessioni Assurance &quot;accidentali&quot;.
* Sono supportate solo le connessioni tra Assurance e l’interfaccia web di Assurance che appartengono allo stesso ID organizzazione Adobe Experience Cloud.
* Gli eventi SDK di Adobe Experience Platform Mobile vengono trasportati tramite HTTPS.
* Gli SDK per dispositivi mobili Assurance e Adobe Experience Platform utilizzano TLS 1.2
* Le sessioni Assurance vengono eliminate dopo 30 giorni.
* I dati della sessione Assurance vengono crittografati a riposo, seguendo le best practice di archiviazione.

## Introduzione

Per impostare Assurance, devi prima installare l&#39;estensione Assurance nell&#39;applicazione. Per scoprire come eseguire questa operazione, leggi l’esercitazione su [implementazione dell’estensione Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Dopo aver aggiunto Assurance all’app, puoi creare una sessione Assurance che può essere connessa al dispositivo. Per informazioni su come utilizzare Assurance, leggi [guida all’utilizzo di Assurance](./tutorials/using-assurance.md).
