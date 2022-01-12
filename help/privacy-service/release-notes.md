---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Note sulla versione di Privacy Service
topic-legacy: release notes
description: Note aggiornate sulla versione di Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzioni di Adobe Experience Platform [!DNL Privacy Service], nonché miglioramenti e correzioni di bug significativi.

>[!NOTE]
>
>Note aggiornate sulla versione per altre [!DNL Experience Platform] servizi disponibili [qui](../release-notes/latest/latest.md).

## 9 settembre 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto per LGPD (Brasile) | In Brasile è ora possibile creare posti di lavoro nel settore della privacy [!DNL Lei Geral de Proteção de Dados] Regolamento (LGPD). Questi posti di lavoro sono monitorati dal codice di regolamentazione `lgpd_bra`. |

## 8 aprile 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | [!DNL Privacy] Le richieste possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando esegui richieste di privacy nell’API, la `regulation` array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia utente | Ora puoi specificare diversi tipi di namespace nel Generatore di richieste nel [!DNL Privacy Service] Interfaccia utente. Consulta la sezione [guida utente](ui/user-guide.md) per ulteriori informazioni. |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| [!DNL Privacy Service] rebranding | Il nome precedentemente denominato &quot;Servizio RGPD&quot; è stato rinominato in [!DNL Privacy Service] poiché il servizio è cresciuto per supportare altre normative oltre al RGPD. |
| Nuovi endpoint API | Percorso di base per [!DNL Privacy Service] L’API è stata aggiornata da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuovo obbligatorio `regulation` property | Durante la creazione di nuovi lavori nel [!DNL Privacy Service] API `regulation` la proprietà deve essere fornita nel payload della richiesta per indicare quale regola monitorare il processo in. I valori accettati sono `gdpr` e `ccpa`. Visualizza il documento in [lavori sulla privacy](api/privacy-jobs.md) in [!DNL Privacy Service] Guida all’API per ulteriori informazioni. |
| Supporto per l’autenticazione Adobe Primetime | [!DNL Privacy Service] ora accetta le richieste di accesso/cancellazione dall’autenticazione di Adobe Primetime, utilizzando `primetimeAuthentication` come valore del prodotto. Consulta la sezione [Documentazione di Primetime Authentication](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) per ulteriori informazioni. |

### Miglioramenti

* [!DNL Privacy Service] Miglioramenti all’interfaccia utente:
   * Pagine separate per il tracciamento dei processi per i regolamenti RGPD e CCPA.
   * Nuovo *Tipo di regolamento* menu a discesa per passare dai dati di tracciamento per RGPD e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Dashboard delle metriche di richiesta | Il nuovo dashboard delle metriche nel [!DNL Privacy Service] L’interfaccia utente offre visibilità alle richieste RGPD inviate, errate e completate. |
| Request Builder | Per le organizzazioni con utenti tecnici e non che inviano richieste RGPD, è stata aggiunta all’interfaccia utente una funzionalità &quot;Crea richiesta&quot;. La funzionalità di invio dei file JSON è ancora disponibile nella sezione [!DNL Privacy Service] Interfaccia utente per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche degli eventi di lavoro RGPD | Le notifiche degli eventi sugli stati dei processi RGPD sono un elemento critico per molti flussi di lavoro. Sebbene le notifiche siano state in precedenza servite utilizzando singoli avvisi e-mail, le notifiche degli eventi RGPD sono messaggi che sfruttano gli eventi di Adobe I/O, che vengono inviati a un webhook configurato che facilita l’automazione della richiesta dei processi. [!DNL Privacy Service] Gli utenti dell’interfaccia utente possono iscriversi ad Adobi I/O eventi RGPD per ricevere aggiornamenti al completamento di un prodotto o di un lavoro RGPD. |

## 18 aprile 2019

### Miglioramenti

* Intervallo predefinito per la tabella di stato nel [!DNL Privacy Service] Interfaccia utente modificata in un intervallo di 7 giorni.
* Migliore gestione delle eccezioni interne.
* Sono state migliorate le prestazioni introducendo la memorizzazione in cache per chiamate interne comuni con tassi di variazione dei dati bassi.

### Correzioni di bug

* Aggiunte informazioni di registrazione mancanti per le query filtrate per la `GET /` punto finale [!DNL Privacy Service] API.

## 11 aprile 2019

### Miglioramenti

* Interfaccia aggiornata per supportare nuove funzionalità per i clienti beta
* Nuove API metriche per supportare le funzionalità di interfaccia utente 2.0 in versione beta

## 9 aprile 2019

### Miglioramenti

* Tutte le chiamate API di ricerca (GET) sono state aggiornate per impostazione predefinita a un intervallo di lookback di 30 giorni.
* Utilizzo API limitato per un intervallo di lookback massimo di 45 giorni

## 14 febbraio 2019

### Miglioramenti

* Applica `include` in ogni invio POST.
* Applica `include` campo durante il caricamento di JSON.

### Correzioni di bug

* È stato risolto un problema che impediva ai clienti di caricare il [!DNL Privacy Service] Interfaccia utente.
