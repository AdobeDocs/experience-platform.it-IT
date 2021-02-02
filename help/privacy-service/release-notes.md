---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Note sulla versione Privacy Service
topic: release notes
description: Note aggiornate sulla versione di  Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---


# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzioni di Adobe Experience Platform [!DNL Privacy Service], nonché miglioramenti e correzioni di bug importanti.

>[!NOTE]
>
>Le ultime note sulla versione di altri servizi [!DNL Experience Platform] sono disponibili [qui](../release-notes/latest/latest.md).

## 9 settembre 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto per LGPD (Brasile) | I lavori per la privacy possono ora essere creati nell&#39;ambito della normativa brasiliana [!DNL Lei Geral de Proteção de Dados] (LGPD). Tali lavori vengono tracciati in base al codice di regolamentazione `lgpd_bra`. |

## 8 aprile 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | [!DNL Privacy] Le richieste possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando si effettuano richieste di privacy nell&#39;API, l&#39;array `regulation` accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia | Ora è possibile specificare diversi tipi di spazio nomi nel Generatore di richieste nell&#39;interfaccia [!DNL Privacy Service]. Per ulteriori informazioni, vedere la [guida utente](ui/user-guide.md). |
| Obsoleto endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| [!DNL Privacy Service] rebranding | L&#39;ex &quot;GDPR Service&quot; è stato rinominato in [!DNL Privacy Service] poiché il servizio è cresciuto fino a supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39;API [!DNL Privacy Service] è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova proprietà `regulation` obbligatoria | Durante la creazione di nuovi processi nell&#39;API [!DNL Privacy Service], nel payload della richiesta deve essere specificata una proprietà `regulation` per indicare quale regola tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. Per ulteriori informazioni, consultare il documento sui [processi di privacy](api/privacy-jobs.md) nella [!DNL Privacy Service] guida per gli sviluppatori. |
| Supporto per  autenticazione Adobe Primetime | [!DNL Privacy Service] accetta ora le richieste di accesso/eliminazione  autenticazione Adobe Primetime, utilizzando  `primetimeAuthentication` come valore del prodotto. Per ulteriori informazioni, vedere la [documentazione sull&#39;autenticazione Primetime](http://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Miglioramenti

* [!DNL Privacy Service] Miglioramenti dell’interfaccia utente:
   * Pagine separate per il monitoraggio dei processi per le normative GDPR e CCPA.
   * Nuovo menu a discesa *Tipo di regolamento* per passare dai dati di tracciamento per GDPR e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Pannello Metriche richieste | Il nuovo dashboard delle metriche nell&#39; [!DNL Privacy Service] interfaccia utente offre visibilità sulle richieste GDPR inviate, errate e completate. |
| Request Builder | Per le organizzazioni di assistenza con utenti tecnici e non tecnici che inviano richieste GDPR, all’interfaccia utente è stata aggiunta la funzionalità &quot;Crea richiesta&quot;. La funzionalità di invio dei file JSON è ancora disponibile nell&#39;interfaccia [!DNL Privacy Service] per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche evento processo GDPR | Le notifiche degli eventi relative agli stati dei processi GDPR sono un elemento critico per molti flussi di lavoro. Sebbene in precedenza le notifiche venivano servite tramite notifiche e-mail singole, le notifiche evento GDPR sono messaggi che sfruttano  eventi Adobe I/O, che vengono inviati a un webhook configurato per facilitare l&#39;automazione della richiesta di un processo. [!DNL Privacy Service] Gli utenti dell&#39;interfaccia utente possono iscriversi  eventi GDPR di Adobe I/O per ricevere aggiornamenti al termine di un processo relativo a un prodotto o al GDPR. |

## 18 aprile 2019

### Miglioramenti

* Intervallo predefinito per la tabella di stato nell&#39;interfaccia utente di [!DNL Privacy Service] modificato in un intervallo di 7 giorni.
* Migliore gestione delle eccezioni interne.
* Prestazioni migliorate grazie all&#39;introduzione del caching per le chiamate interne comuni con basse velocità di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per l&#39;endpoint `GET /` nell&#39;API [!DNL Privacy Service].

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

* Applica il campo `include` in ogni invio di POST.
* Applica il campo `include` durante il caricamento di JSON.

### Correzioni di bug

* È stato risolto un problema che impediva ai clienti di caricare l&#39;interfaccia [!DNL Privacy Service].