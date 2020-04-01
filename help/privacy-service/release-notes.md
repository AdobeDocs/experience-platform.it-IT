---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Note sulla versione del servizio sulla privacy
topic: release notes
translation-type: tm+mt
source-git-commit: d7aa1b4e3e697a504964d6eb485f536065c6718a

---


# Note sulla versione del servizio sulla privacy

Questo documento contiene informazioni sulle nuove funzioni di Adobe Experience Platform Privacy Service, nonché miglioramenti e correzioni di bug importanti.

## 14 gennaio 2020

### Nuove funzionalità

| Funzione | Descrizione |
--- | ---
| Ripristino del servizio sulla privacy | L&#39;ex &quot;GDPR Service&quot; è stato riassegnato al Privacy Service, in quanto il servizio è cresciuto per supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39;API del servizio Privacy è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuova `regulation` proprietà obbligatoria | Quando si creano nuovi processi nell’API del servizio Privacy, nel payload della richiesta deve essere specificata una `regulation` proprietà per indicare quale regola tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. Per ulteriori informazioni, consulta il documento sui processi di [privacy](api/privacy-jobs.md) nella guida per gli sviluppatori del servizio per la privacy. |
| Supporto per l&#39;autenticazione Adobe Primetime | Il servizio per la privacy ora accetta le richieste di accesso/eliminazione dall&#39;autenticazione Adobe Primetime, utilizzando `primetimeAuthentication` come valore del prodotto. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Miglioramenti

* Miglioramenti all’interfaccia utente del servizio sulla privacy:
   * Pagine separate per il monitoraggio dei processi per le normative GDPR e CCPA.
   * Nuovo menu a discesa Tipo __ regolamento per passare dai dati di monitoraggio per GDPR e CCPA.

## 25 luglio 2019

### Nuove funzionalità

| Funzione | Descrizione |
--- | ---
| Pannello Metriche richieste | Il nuovo dashboard delle metriche nell’interfaccia utente del servizio Privacy offre visibilità sulle richieste GDPR inviate, errate e completate. |
| Request Builder | Per le organizzazioni di assistenza con utenti tecnici e non tecnici che inviano richieste GDPR, all’interfaccia utente è stata aggiunta la funzionalità &quot;Crea richiesta&quot;. La funzionalità di invio dei file JSON è ancora disponibile nell’interfaccia utente del servizio Privacy per le organizzazioni che preferiscono continuare a utilizzarla. |
| Notifiche evento processo GDPR | Le notifiche degli eventi relative agli stati dei processi GDPR sono un elemento critico per molti flussi di lavoro. Sebbene in precedenza le notifiche venivano servite tramite notifiche e-mail singole, le notifiche evento GDPR sono messaggi che sfruttano gli eventi di I/O di Adobe, che vengono inviati a un webhook configurato per facilitare l’automazione della richiesta di un processo. Gli utenti dell’interfaccia utente del servizio per la privacy possono iscriversi agli eventi Adobe I/O GDPR per ricevere aggiornamenti al termine di un processo relativo a un prodotto o al GDPR. |

## 18 aprile 2019

### Miglioramenti

* L’intervallo predefinito per la tabella di stato nell’interfaccia utente del servizio sulla privacy è stato modificato in un intervallo di 7 giorni.
* Migliore gestione delle eccezioni interne.
* Prestazioni migliorate grazie all&#39;introduzione del caching per le chiamate interne comuni con basse velocità di modifica dei dati.

### Correzioni di bug

* Sono state aggiunte informazioni di registrazione mancanti per le query filtrate per l&#39; `GET /` endpoint nell&#39;API del servizio Privacy.

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

* È stato risolto un problema che impediva ai clienti di caricare l’interfaccia utente del servizio per la privacy.