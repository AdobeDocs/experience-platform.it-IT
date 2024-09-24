---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Note sulla versione di Privacy Service
description: Note aggiornate sulla versione di Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzioni di Adobe Experience Platform [!DNL Privacy Service], nonché sui miglioramenti e sulle correzioni di bug significativi.

>[!NOTE]
>
>Le note aggiornate sulle versioni di altri servizi [!DNL Experience Platform] sono disponibili [qui](../release-notes/latest/latest.md).

## 9 settembre 2020

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Supporto per LGPD (Brasile) | I processi relativi alla privacy possono ora essere creati in base al regolamento [!DNL Lei Geral de Proteção de Dados] (LGPD) del Brasile. Questi processi vengono tracciati con il codice di regolamento `lgpd_bra`. |

## 8 aprile 2020

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | È ora possibile creare e tenere traccia di richieste [!DNL Privacy] ai sensi della Legge sulla protezione dei dati personali (Personal Data Protection Act, PDPA) in Thailandia. Quando si eseguono richieste di accesso a dati personali nell’API, l’array `regulation` accetta il valore “pdpa_tha”. |
| Tipi di spazio dei nomi nell’interfaccia utente | È ora possibile specificare diversi tipi di spazio dei nomi nel Generatore di richieste nell’interfaccia utente di [!DNL Privacy Service]. Per ulteriori informazioni, consulta la [guida utente](ui/user-guide.md). |
| Obsolescenza dell’endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Rebranding di [!DNL Privacy Service] | Il servizio precedentemente denominato “GDPR Service” è stato rinominato [!DNL Privacy Service] in quanto è stato esteso per supportare anche altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l’API di [!DNL Privacy Service] è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova proprietà `regulation` obbligatoria | Quando si creano nuovi processi nell’API di [!DNL Privacy Service], è necessario fornire una proprietà `regulation` nel payload della richiesta per indicare in quale regolamento tenere traccia del processo. I valori consentiti sono `gdpr` e `ccpa`. Per ulteriori informazioni, consulta il documento sui [processi per la privacy](api/privacy-jobs.md) nella guida dell’API di [!DNL Privacy Service]. |
| Supporto per l’autenticazione di Adobe Primetime | [!DNL Privacy Service] ora accetta le richieste di accesso/eliminazione dall’autenticazione di Adobe Primetime, utilizzando `primetimeAuthentication` come valore di prodotto. Per ulteriori informazioni, consulta la [documentazione sull’autenticazione di Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Miglioramenti

* Miglioramenti dell’interfaccia utente di [!DNL Privacy Service]:
   * Pagine di tracciamento dei processi separate per le normative GDPR e CCPA.
   * Nuovo elenco a discesa *Tipo di regolamento* per passare dai dati di tracciamento per GDPR a quelli per CCPA.

## 25 luglio 2019

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Dashboard delle metriche delle richieste | La nuova dashboard delle metriche nell’interfaccia utente di [!DNL Privacy Service] fornisce visibilità sulle richieste correlate al GDPR inviate, errate e completate. |
| Generatore di richieste | Per assistere le organizzazioni con utenti tecnici e non tecnici che inviano richieste correlate al GDPR, è stata aggiunta una funzionalità “Crea richiesta” all’interfaccia utente. La funzionalità di invio file JSON è ancora disponibile nell’interfaccia utente di [!DNL Privacy Service] per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche eventi processo GDPR | Le notifiche degli eventi relativi agli stati dei processi GPDR sono un elemento fondamentale per molti flussi di lavoro. Mentre le notifiche in precedenza venivano inviate utilizzando singoli avvisi e-mail, le notifiche degli eventi GDPR sono messaggi che sfruttano gli eventi di Adobe I/O, che vengono inviati a un webhook configurato per facilitare l’automazione delle richieste dei processo. Gli utenti dell’interfaccia utente [!DNL Privacy Service] possono iscriversi agli eventi GDPR di Adobe I/O per ricevere aggiornamenti quando un prodotto o il processo GDPR è stato completato. |

## 18 aprile 2019

### Miglioramenti

* Intervallo predefinito per la tabella di stato nell’interfaccia utente di [!DNL Privacy Service] modificato in un intervallo di 7 giorni.
* Migliore gestione interna delle eccezioni.
* Sono state migliorate le prestazioni introducendo la memorizzazione in cache per le chiamate interne comuni con basse percentuali di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni sulla registrazione mancanti per le query filtrate per l’endpoint `GET /` nell’API di [!DNL Privacy Service].

## 11 aprile 2019

### Miglioramenti

* Interfaccia utente aggiornata per supportare nuove funzionalità per la clientela Beta
* Nuove API per le metriche per supportare le funzioni dell’interfaccia utente 2.0 in versione Beta

## 9 aprile 2019

### Miglioramenti

* Tutte le chiamate API di ricerca (GET) sono state aggiornate all’intervallo di lookback predefinito di 30 giorni
* L’utilizzo di API è limitato a un intervallo di lookback massimo di 45 giorni

## 14 febbraio 2019

### Miglioramenti

* Applicare il campo `include` in ogni invio POST.
* Applicare il campo `include` durante il caricamento di JSON.

### Correzioni di bug

* È stato risolto un problema che impediva alla clientela di caricare l’interfaccia utente di [!DNL Privacy Service].
