---
title: Panoramica di Adobe Experience Platform Assurance
description: Adobe Experience Platform Assurance consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze all’interno delle tue applicazioni mobili.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '824'
ht-degree: 100%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance è un prodotto di [Adobe Experience Cloud](https://www.adobe.com/it/experience-cloud.html) che consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze nelle tue applicazioni mobili.

>[!IMPORTANT]
>
> Il Project Griffon è ora noto come **Assurance**.
>
> Il Project Griffon è ora disponibile per **tutta** la clientela di Adobe Experience Cloud come Assurance. Per ulteriori informazioni su questa transizione, consulta la [guida all’accesso utente](./user-access.md).

>[!INFO]
>
>Sono disponibili le API pubbliche di Assurance.
>
>Le [API di Assurance](https://developer.adobe.com/adobe-assurance-public-apis/) sono una raccolta di API che consente agli utenti di testare ed eseguire il debug delle proprie app web e mobili, se dotate di Adobe Assurance con Mobile SDK.

## Disponibilità generale

A partire dal 15 ottobre 2022, Assurance è generalmente disponibile per tutti su Adobe Experience Cloud.

### Che cosa è cambiato?

Dal 15 ottobre l’accesso ad Assurance sarà gestito tramite Admin Console. Consulta la [guida all’accesso utente](./user-access.md) per avere un accesso illimitato.

Non sono previste altre modifiche o interruzioni per le integrazioni, le sessioni e gli eventi Assurance esistenti. Puoi accedere ad Assurance tramite [https://griffon.adobe.com](https://griffon.adobe.com) **oppure** utilizzare (e salvare) la pagina [https://experience.adobe.com/it/assurance](https://experience.adobe.com/it/assurance).

## Cosa può fare Assurance per te?

### Configurazione rapida

Inizia subito con poche righe di codice. Per le app mobili, Assurance utilizza Adobe Experience Platform Mobile SDK per consentire di controllare, simulare e convalidare gli eventi dell’app, la localizzazione del segnale, i parametri di configurazione, i registri SDK, le informazioni sul dispositivo e molto altro ancora.

### Connessione senza problemi

Con Assurance, è possibile connettere l’app a Platform in modo semplice e affidabile. Non è necessario utilizzare proxy di rete, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) e altri tipi di meccanismi: per connettere l’app ad Assurance è sufficiente scansionare un codice QR o premere un pulsante.

![](./images/index/no-hassle-connection.png)

### Controllo, simulazione e convalida in tempo reale

Dopo aver effettuato la connessione ad Assurance, puoi controllare gli eventi e le attività dell’app trasmessi in diretta streaming, applicare filtri ed eseguire ricerche per eliminare il rumore. Gli eventi contengono dettagli su come convalidare, eseguire il debug e risolvere i problemi relativi all’implementazione dell’app mobile. Assurance consente inoltre di fare screenshot, simulare la localizzazione del segnale e altro ancora in tempo reale.

![](./images/index/real-time-insepction.png)

### Integrazione con Adobe Experience Cloud

I dati e le esperienze lato client vengono contestualizzati in base al modo in cui gli utenti configurano le regole di reporting, le attività e le campagne sulle interfacce utente mirate per i marketer. Per aiutarti ad avere una visione d’insieme, stiamo integrando le soluzioni di Adobe Experience Cloud come Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service e altro ancora.

![](./images/index/integration.png)

## Funzioni

### Eventi, registri e altro ancora di Adobe Experience Platform Mobile SDK

Assurance consente di controllare gli eventi SDK non elaborati generati da Adobe Experience Platform Mobile SDK. Tutti gli eventi raccolti dall’SDK sono disponibili per il controllo. Gli eventi SDK vengono caricati in una vista a elenco, ordinati in ordine cronologico. Ogni evento dispone di una vista dettagliata che fornisce ulteriori dettagli. Sono inoltre disponibili viste aggiuntive per sfogliare la configurazione dell’SDK, gli elementi dati, gli stati condivisi e le versioni delle estensioni SDK.

### Adobe Analytics

La vista Adobe Analytics > Eventi di Analytics è una vista mirata che mostra gli eventi relativi alla tua implementazione di Adobe Analytics per dispositivi mobili. La vista a elenco mostra gli eventi del ciclo di vita o dell’azione/stato, lo “stato” post-elaborazione, insieme ai dettagli dell’evento richiesti in una vista con un formato speciale. Lo stato post-elaborazione mostra il modo in cui l’evento è stato elaborato da Adobe Analytics dopo l’applicazione delle regole di elaborazione all’evento.

### Adobe Analytics per contenuti in streaming

La vista Adobe Analytics > Eventi di Media Analytics mostra gli eventi per l’implementazione di analisi audio e video. La vista dei dettagli degli eventi mostra i metadati standard e personalizzati tracciati per ogni sessione di riproduzione. Inoltre, puoi visualizzare lo stato post-elaborazione e i dati di analisi dei contenuti multimediali nella fase di post-elaborazione, ad esempio il tempo trascorso sui contenuti multimediali o la durata totale del buffer.

### Places (Servizi di localizzazione)

La vista Servizi di localizzazione è una vista su dispositivo che mostra gli eventi di entrata e uscita della posizione dell’utente per una facile convalida. Questa pratica vista fornisce una comoda interfaccia per visualizzare punti dati specifici della posizione per il controllo sul client per il debug nel contesto.

## Assurance è sicuro?

In Assurance sono state adottate le seguenti misure di sicurezza:

* Sia Assurance che l’interfaccia utente web di Assurance per la connessione dispongono di un handshake protetto basato su PIN. L’utente deve creare esplicitamente un handshake che impedisce a un utente finale di creare connessioni ad Assurance “involontarie”.
* Sono supportate solo le connessioni tra Assurance e l’interfaccia web di Assurance che appartengono allo stesso ID organizzazione di Adobe Experience Cloud.
* Gli eventi di Adobe Experience Platform Mobile SDK vengono trasmessi tramite HTTPS.
* Assurance and Adobe Experience Platform Mobile SDK utilizzano il protocollo TLS 1.2
* Le sessioni di Assurance vengono eliminate dopo 30 giorni.
* I dati della sessione di Assurance vengono crittografati a riposo, seguendo le best practice relative all’archiviazione.

## Introduzione

Per impostare Assurance, devi prima installare l’estensione Assurance nell’applicazione. Per scoprire come eseguire questa operazione, consulta il tutorial sull’[implementazione dell’estensione Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Dopo aver aggiunto Assurance all’applicazione, puoi creare una sessione di Assurance che può essere connessa al dispositivo. Per informazioni su come utilizzare Assurance, consulta la [guida all’utilizzo di Assurance](./tutorials/using-assurance.md).
