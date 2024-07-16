---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Note sulla versione di Privacy Service
description: Note aggiornate sulla versione di Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzionalità di Adobe Experience Platform [!DNL Privacy Service], nonché sui miglioramenti e sulle correzioni di bug significativi.

>[!NOTE]
>
>Le ultime note sulla versione per gli altri servizi [!DNL Experience Platform] sono disponibili [qui](../release-notes/latest/latest.md).

## 9 settembre 2020

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Sostegno alla LGPD (Brasile) | I lavori sulla privacy possono ora essere creati in base al regolamento [!DNL Lei Geral de Proteção de Dados] (LGPD) del Brasile. Questi processi vengono tracciati con il codice di regolamento `lgpd_bra`. |

## 8 aprile 2020

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | È ora possibile creare e tenere traccia di [!DNL Privacy] richieste ai sensi del Personal Data Protection Act (PDPA) in Thailandia. Quando si eseguono richieste di accesso a dati personali nell&#39;API, l&#39;array `regulation` accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di spazio dei nomi nell’interfaccia utente | È ora possibile specificare diversi tipi di spazio dei nomi nel Generatore di richieste nell&#39;interfaccia utente [!DNL Privacy Service]. Per ulteriori informazioni, consulta la [guida utente](ui/user-guide.md). |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| [!DNL Privacy Service] rebranding | Il servizio precedentemente denominato &quot;GDPR Service&quot; è stato rinominato [!DNL Privacy Service] in quanto è cresciuto fino a supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39;API [!DNL Privacy Service] è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova proprietà `regulation` richiesta | Quando si creano nuovi processi nell&#39;API [!DNL Privacy Service], è necessario fornire una proprietà `regulation` nel payload della richiesta per indicare in quale regolamento tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. Per ulteriori informazioni, consulta il documento sui [processi per la privacy](api/privacy-jobs.md) nella guida dell&#39;API [!DNL Privacy Service]. |
| Supporto per l’autenticazione di Adobe Primetime | [!DNL Privacy Service] ora accetta le richieste di accesso/eliminazione dall&#39;autenticazione di Adobe Primetime, utilizzando `primetimeAuthentication` come valore di prodotto. Per ulteriori informazioni, vedere la [documentazione relativa all&#39;autenticazione Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Miglioramenti

* Miglioramenti all&#39;interfaccia utente di [!DNL Privacy Service]:
   * Pagine di tracciamento del lavoro separate per le normative RGPD e CCPA.
   * Nuovo elenco a discesa *Tipo di regolamento* per passare dai dati di tracciamento per RGPD a quelli per CCPA.

## 25 luglio 2019

### Nuove funzioni

| Funzione | Descrizione |
| --- | --- |
| Dashboard delle metriche delle richieste | La nuova dashboard delle metriche nell&#39;interfaccia utente di [!DNL Privacy Service] fornisce visibilità sulle richieste RGPD inviate, errate e completate. |
| Request Builder | Per assistere le organizzazioni con utenti tecnici e non tecnici che inviano richieste RGPD, è stata aggiunta una funzionalità &quot;Crea richiesta&quot; all’interfaccia utente di. La funzionalità di invio file JSON è ancora disponibile nell&#39;interfaccia utente [!DNL Privacy Service] per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche eventi processo RGPD | Le notifiche degli eventi relativi agli stati dei processi RGPD sono un elemento fondamentale per molti flussi di lavoro. Mentre le notifiche venivano servite in precedenza utilizzando singoli avvisi e-mail, le notifiche degli eventi RGPD sono messaggi che sfruttano gli eventi di Adobe I/O, che vengono inviati a un webhook configurato per facilitare l’automazione delle richieste di lavoro. Gli utenti dell&#39;interfaccia utente [!DNL Privacy Service] possono iscriversi agli eventi RGPD di Adobe I/O per ricevere aggiornamenti quando un prodotto o il processo RGPD è stato completato. |

## 18 aprile 2019

### Miglioramenti

* Intervallo predefinito per la tabella di stato nell&#39;interfaccia utente [!DNL Privacy Service] modificato in un intervallo di 7 giorni.
* Migliore gestione interna delle eccezioni.
* Sono state migliorate le prestazioni introducendo il caching per le chiamate interne comuni con basse percentuali di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per l&#39;endpoint `GET /` nell&#39;API [!DNL Privacy Service].

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

* Imponi il campo `include` in ogni invio POST.
* Applica il campo `include` durante il caricamento di JSON.

### Correzioni di bug

* È stato risolto un problema che impediva ai clienti di caricare l&#39;interfaccia utente [!DNL Privacy Service].
