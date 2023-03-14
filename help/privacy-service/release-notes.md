---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Note sulla versione di Privacy Service
description: Note aggiornate sulla versione di Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzioni di Adobe Experience Platform [!DNL Privacy Service], nonché miglioramenti e correzioni di bug significativi.

>[!NOTE]
>
>Note aggiornate sulla versione per altri [!DNL Experience Platform] servizi disponibili [qui](../release-notes/latest/latest.md).

## 9 settembre 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Sostegno alla LGPD (Brasile) | I lavori sulla privacy possono ora essere creati con il [!DNL Lei Geral de Proteção de Dados] (LGPD). Questi lavori vengono tracciati in base al codice del regolamento `lgpd_bra`. |

## 8 aprile 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | [!DNL Privacy] Ora è possibile creare e tenere traccia delle richieste ai sensi della legge sulla protezione dei dati personali (PDPA) in Thailandia. Quando effettui richieste di accesso a dati personali nell’API, il `regulation` l’array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di spazio dei nomi nell’interfaccia utente | Ora puoi specificare diversi tipi di spazio dei nomi nel Generatore di richieste in [!DNL Privacy Service] UI. Consulta la [guida utente](ui/user-guide.md) per ulteriori informazioni. |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| [!DNL Privacy Service] rebranding | Il servizio precedentemente denominato &quot;GDPR Service&quot; è stato rinominato in [!DNL Privacy Service] in quanto il servizio è cresciuto fino a supportare altre normative oltre al RGPD. |
| Nuovi endpoint API | Percorso di base per [!DNL Privacy Service] L’API è stata aggiornata da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuovo obbligatorio `regulation` proprietà | Quando si creano nuovi processi in [!DNL Privacy Service] API, a `regulation` La proprietà deve essere fornita nel payload della richiesta per indicare in quale regolamento tracciare il processo. I valori accettati sono `gdpr` e `ccpa`. Vedi il documento su [processi di privacy](api/privacy-jobs.md) nel [!DNL Privacy Service] Guida API di per ulteriori informazioni. |
| Supporto per l’autenticazione di Adobe Primetime | [!DNL Privacy Service] ora accetta le richieste di accesso/eliminazione dall’autenticazione di Adobe Primetime, utilizzando `primetimeAuthentication` come valore del prodotto. Consulta la [Documentazione sull’autenticazione di Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) per ulteriori informazioni. |

### Miglioramenti

* [!DNL Privacy Service] Miglioramenti all’interfaccia utente:
   * Pagine di tracciamento del lavoro separate per le normative RGPD e CCPA.
   * Nuovo *Tipo di regolamento* menu a discesa per passare dai dati di tracciamento per RGPD e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Dashboard delle metriche delle richieste | La nuova dashboard delle metriche in [!DNL Privacy Service] L’interfaccia utente fornisce visibilità sulle richieste RGPD inviate, errate e completate. |
| Request Builder | Per assistere le organizzazioni con utenti tecnici e non tecnici che inviano richieste RGPD, è stata aggiunta una funzionalità &quot;Crea richiesta&quot; all’interfaccia utente di. La funzionalità di invio file JSON è ancora disponibile nel [!DNL Privacy Service] Interfaccia utente per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche eventi processo RGPD | Le notifiche degli eventi relativi agli stati dei processi RGPD sono un elemento fondamentale per molti flussi di lavoro. Mentre le notifiche venivano servite in precedenza utilizzando singoli avvisi e-mail, le notifiche degli eventi RGPD sono messaggi che sfruttano gli eventi di Adobe I/O, che vengono inviati a un webhook configurato per facilitare l’automazione delle richieste di lavoro. [!DNL Privacy Service] Gli utenti dell’interfaccia utente possono iscriversi agli eventi RGPD di Adobe I/O per ricevere aggiornamenti al completamento di un prodotto o del processo RGPD. |

## 18 aprile 2019

### Miglioramenti

* Intervallo predefinito per la tabella di stato in [!DNL Privacy Service] Interfaccia utente modificata in un intervallo di 7 giorni.
* Migliore gestione interna delle eccezioni.
* Sono state migliorate le prestazioni introducendo il caching per le chiamate interne comuni con basse percentuali di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per `GET /` endpoint nella [!DNL Privacy Service] API.

## 11 aprile 2019

### Miglioramenti

* Interfaccia utente aggiornata per supportare nuove funzionalità per i clienti beta
* Nuove API per le metriche per supportare le funzioni dell’interfaccia utente 2.0 in versione beta

## 9 aprile 2019

### Miglioramenti

* Tutte le chiamate API di ricerca (GET) sono state aggiornate all’intervallo di lookback predefinito di 30 giorni
* L’utilizzo API è limitato a un intervallo di lookback massimo di 45 giorni

## 14 febbraio 2019

### Miglioramenti

* Imponi `include` in ogni invio POST.
* Imponi `include` durante il caricamento di JSON.

### Correzioni di bug

* È stato risolto un problema che impediva ai clienti di caricare il [!DNL Privacy Service] UI.
