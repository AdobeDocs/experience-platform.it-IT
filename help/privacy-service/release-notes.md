---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Note sulla versione di Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 4cfa64e3371496e2408fe8fee64d49883334917c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---


# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzioni per  Adobe Experience Platform [!DNL Privacy Service], nonché miglioramenti e correzioni di bug significativi.

>[!NOTE]
>
>Le ultime note sulla versione di altri [!DNL Experience Platform] servizi sono disponibili [qui](../release-notes/latest/latest.md).

## 8 aprile 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | [!DNL Privacy] Le richieste possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando si effettuano richieste di privacy nell&#39;API, l&#39; `regulation` array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia | È ora possibile specificare diversi tipi di spazio nomi nel Generatore di richieste nell&#39; [!DNL Privacy Service] interfaccia utente. Per ulteriori informazioni, consultate la guida [](ui/user-guide.md) utente. |
| Obsoleto endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| [!DNL Privacy Service] rebranding | L&#39;ex &quot;GDPR Service&quot; è stato rinominato [!DNL Privacy Service] in quanto il servizio è cresciuto per supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39; [!DNL Privacy Service] API è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova `regulation` proprietà obbligatoria | Durante la creazione di nuovi processi nell&#39; [!DNL Privacy Service] API, nel payload della richiesta deve essere specificata una `regulation` proprietà per indicare quale regola tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. Per ulteriori informazioni, consulta il documento sui processi di [privacy](api/privacy-jobs.md) nella guida per [!DNL Privacy Service] gli sviluppatori. |
| Supporto per l&#39;autenticazione Adobe Primetime | [!DNL Privacy Service] accetta ora le richieste di accesso/eliminazione dall&#39;autenticazione Adobe Primetime, utilizzando `primetimeAuthentication` come valore di prodotto. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Miglioramenti

* [!DNL Privacy Service] Miglioramenti dell’interfaccia utente:
   * Pagine separate per il monitoraggio dei processi per le normative GDPR e CCPA.
   * Nuovo menu a discesa Tipo __ regolamento per passare dai dati di monitoraggio per GDPR e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Pannello Metriche richieste | Il nuovo dashboard delle metriche nell’ [!DNL Privacy Service] interfaccia utente fornisce visibilità sulle richieste GDPR inviate, errate e completate. |
| Request Builder | Per le organizzazioni di assistenza con utenti tecnici e non tecnici che inviano richieste GDPR, all’interfaccia utente è stata aggiunta la funzionalità &quot;Crea richiesta&quot;. La funzionalità di invio dei file JSON è ancora disponibile nell’ [!DNL Privacy Service] interfaccia utente per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche evento processo GDPR | Le notifiche degli eventi relative agli stati dei processi GDPR sono un elemento critico per molti flussi di lavoro. Sebbene in precedenza le notifiche venivano servite tramite notifiche e-mail singole, le notifiche evento GDPR sono messaggi che sfruttano gli eventi di I/O di Adobe, che vengono inviati a un webhook configurato per facilitare l’automazione della richiesta di un processo. [!DNL Privacy Service] Gli utenti dell&#39;interfaccia utente possono iscriversi agli eventi Adobe I/O GDPR per ricevere aggiornamenti al termine di un processo relativo a un prodotto o al GDPR. |

## 18 aprile 2019

### Miglioramenti

* Intervallo predefinito per la tabella di stato nell’ [!DNL Privacy Service] interfaccia utente modificato in un intervallo di 7 giorni.
* Migliore gestione delle eccezioni interne.
* Prestazioni migliorate grazie all&#39;introduzione del caching per le chiamate interne comuni con basse velocità di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per l&#39; `GET /` endpoint nell&#39; [!DNL Privacy Service] API.

## 11 aprile 2019

### Miglioramenti

* Interfaccia utente aggiornata per supportare nuove funzionalità per i clienti beta
* Nuove API metriche per il supporto delle funzionalità di UI 2.0 nella versione beta

## 9 aprile 2019

### Miglioramenti

* Sono state aggiornate tutte le chiamate API di ricerca (GET) per impostazione predefinita a un intervallo di lookback di 30 giorni
* Utilizzo API limitato per un intervallo massimo di lookback di 45 giorni

## 14 febbraio 2019

### Miglioramenti

* Applica il `include` campo in ogni invio POST.
* Applica il `include` campo quando carichi JSON.

### Correzioni di bug

* È stato risolto un problema che impediva agli utenti di caricare l&#39; [!DNL Privacy Service] interfaccia utente.