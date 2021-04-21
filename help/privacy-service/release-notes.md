---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Note sulla versione di Privacy Service
topic-legacy: release notes
description: Note aggiornate sulla versione di Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# Note sulla versione di [!DNL Privacy Service]

Questo documento contiene informazioni sulle nuove funzioni di Adobe Experience Platform [!DNL Privacy Service], nonché miglioramenti e correzioni di bug significativi.

>[!NOTE]
>
>Le ultime note sulla versione per altri servizi [!DNL Experience Platform] sono disponibili [qui](../release-notes/latest/latest.md).

## 9 settembre 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto per LGPD (Brasile) | I lavori sulla privacy possono ora essere creati in base al regolamento [!DNL Lei Geral de Proteção de Dados] (LGPD) del Brasile. Questi posti di lavoro vengono tracciati in base al codice di regolamento `lgpd_bra`. |

## 8 aprile 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | [!DNL Privacy] Le richieste possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando si effettuano richieste di privacy nell&#39;API, l&#39;array `regulation` accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia utente | Ora puoi specificare diversi tipi di namespace nel Generatore di richieste nell’ interfaccia utente [!DNL Privacy Service] . Per ulteriori informazioni, consulta la [guida utente](ui/user-guide.md) . |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| [!DNL Privacy Service] rebranding | Il nome precedentemente denominato &quot;Servizio RGPD&quot; è stato rinominato in [!DNL Privacy Service] in quanto il servizio è cresciuto per supportare altre normative oltre al RGPD. |
| Nuovi endpoint API | Il percorso di base per l&#39;API [!DNL Privacy Service] è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova proprietà `regulation` obbligatoria | Durante la creazione di nuovi lavori nell&#39;API [!DNL Privacy Service], è necessario fornire una proprietà `regulation` nel payload della richiesta per indicare il regolamento in cui tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. Per ulteriori informazioni, consulta il documento sui [processi di privacy](api/privacy-jobs.md) nella guida per gli sviluppatori [!DNL Privacy Service] . |
| Supporto per l’autenticazione Adobe Primetime | [!DNL Privacy Service] ora accetta le richieste di accesso/cancellazione dall’autenticazione di Adobe Primetime, utilizzando  `primetimeAuthentication` come valore del prodotto. Per ulteriori informazioni, consulta la [documentazione sull&#39;autenticazione di Primetime](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) . |

### Miglioramenti

* [!DNL Privacy Service] Miglioramenti all’interfaccia utente:
   * Pagine separate per il tracciamento dei processi per i regolamenti RGPD e CCPA.
   * Nuovo menu a discesa *Tipo di regolamento* per passare dai dati di tracciamento per RGPD e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
| --- | --- |
| Dashboard delle metriche di richiesta | Il nuovo dashboard delle metriche nell’ interfaccia utente di [!DNL Privacy Service] offre visibilità alle richieste RGPD inviate, errate e completate. |
| Request Builder | Per le organizzazioni con utenti tecnici e non che inviano richieste RGPD, è stata aggiunta all’interfaccia utente una funzionalità &quot;Crea richiesta&quot;. La funzionalità di invio dei file JSON è ancora disponibile nell’ interfaccia utente [!DNL Privacy Service] per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche degli eventi di lavoro RGPD | Le notifiche degli eventi sugli stati dei processi RGPD sono un elemento critico per molti flussi di lavoro. Sebbene le notifiche siano state in precedenza servite utilizzando singoli avvisi e-mail, le notifiche degli eventi RGPD sono messaggi che sfruttano gli eventi di Adobe I/O, che vengono inviati a un webhook configurato che facilita l’automazione della richiesta dei processi. [!DNL Privacy Service] Gli utenti dell’interfaccia utente possono iscriversi ad Adobi I/O eventi RGPD per ricevere aggiornamenti al completamento di un prodotto o di un lavoro RGPD. |

## 18 aprile 2019

### Miglioramenti

* L&#39;intervallo predefinito per la tabella di stato nell&#39;interfaccia utente [!DNL Privacy Service] è stato modificato in un intervallo di 7 giorni.
* Migliore gestione delle eccezioni interne.
* Sono state migliorate le prestazioni introducendo la memorizzazione in cache per chiamate interne comuni con tassi di variazione dei dati bassi.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per l’endpoint `GET /` nell’ API [!DNL Privacy Service].

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

* Applica il campo `include` in ogni invio POST.
* Applica il campo `include` durante il caricamento di JSON.

### Correzioni di bug

* È stato risolto un problema che impediva ai clienti di caricare l’ interfaccia utente [!DNL Privacy Service] .
