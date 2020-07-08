---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Note sulla versione di Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Note sulla versione di Privacy Service

Questo documento contiene informazioni sulle nuove funzioni per  Adobe Experience Platform Privacy Service, nonché miglioramenti e correzioni di bug significativi.

>[!NOTE]
>
>Le ultime note sulla versione di altri servizi Experience Platform  sono disponibili [qui](../release-notes/latest/latest.md).

## 8 aprile 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | Le richieste di privacy possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando si effettuano richieste di privacy nell&#39;API, l&#39; `regulation` array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia | Ora potete specificare diversi tipi di spazio nomi in Request Builder nell’interfaccia utente di Privacy Service. Per ulteriori informazioni, consultate la guida [](ui/user-guide.md) utente. |
| Obsoleto endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Privacy Service rebranding | L&#39;ex &quot;GDPR Service&quot; è stato riassegnato ad Privacy Service perché il servizio è cresciuto fino a supportare altre normative, oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39;API Privacy Service è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova `regulation` proprietà obbligatoria | Durante la creazione di nuovi processi nell’API Privacy Service, nel payload della richiesta deve essere specificata una `regulation` proprietà per indicare quale regola tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. Per ulteriori informazioni, consulta il documento sui processi [di](api/privacy-jobs.md) privacy nella guida per gli sviluppatori di Privacy Service. |
| Supporto per l&#39;autenticazione Adobe Primetime | Privacy Service ora accetta le richieste di accesso/eliminazione dall&#39;autenticazione Adobe Primetime, utilizzando `primetimeAuthentication` come valore di prodotto. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Miglioramenti

* Miglioramenti dell’interfaccia utente Privacy Service:
   * Pagine separate per il monitoraggio dei processi per le normative GDPR e CCPA.
   * Nuovo menu a discesa Tipo __ regolamento per passare dai dati di monitoraggio per GDPR e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Pannello Metriche richieste | Il nuovo dashboard delle metriche nell’interfaccia utente di Privacy Service fornisce visibilità sulle richieste GDPR inviate, errate e completate. |
| Request Builder | Per le organizzazioni di assistenza con utenti tecnici e non tecnici che inviano richieste GDPR, all’interfaccia utente è stata aggiunta la funzionalità &quot;Crea richiesta&quot;. La funzionalità di invio dei file JSON è ancora disponibile nell’interfaccia utente di Privacy Service per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche evento processo GDPR | Le notifiche degli eventi relative agli stati dei processi GDPR sono un elemento critico per molti flussi di lavoro. Sebbene in precedenza le notifiche venivano servite tramite notifiche e-mail singole, le notifiche evento GDPR sono messaggi che sfruttano gli eventi di I/O di Adobe, che vengono inviati a un webhook configurato per facilitare l’automazione della richiesta di un processo. Gli utenti dell&#39;interfaccia utente Privacy Service possono iscriversi agli eventi Adobe I/O GDPR per ricevere aggiornamenti al termine di un processo relativo a un prodotto o al GDPR. |

## 18 aprile 2019

### Miglioramenti

* L’intervallo predefinito per la tabella di stato nell’interfaccia utente di Privacy Service è stato modificato in un intervallo di 7 giorni.
* Migliore gestione delle eccezioni interne.
* Prestazioni migliorate grazie all&#39;introduzione del caching per le chiamate interne comuni con basse velocità di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per l&#39; `GET /` endpoint nell&#39;API di Privacy Service.

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

* È stato risolto un problema che impediva ai clienti di caricare l&#39;interfaccia utente di Privacy Service.