---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 15 gennaio 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Note sulla versione di Adobe Experience Platform

## Data di rilascio: 15 gennaio 2020

## Sistema XDM (Experience Data Model)

Standardizzazione e interoperabilità sono concetti chiave della piattaforma Experience. Experience Data Model (XDM), guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che desideri comunicare con i servizi in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

### Nuove funzionalità

| Funzione | Descrizione |
|--- | ---|
| Limitazioni del tipo di campo per i campi di uguale gerarchia | Dopo che un campo XDM è stato definito come un determinato tipo, tutti gli altri campi con lo stesso nome e la stessa gerarchia devono utilizzare lo stesso tipo di campo, indipendentemente dalle classi o dai mixin in cui sono utilizzati. Ad esempio, se un mixin per la classe Profilo XDM contiene un `profile.age` campo di tipo &quot;integer&quot;, un mixin simile per XDM ExperienceEvent non può avere un `profile.age` campo di tipo &quot;string&quot;. Per utilizzare un tipo di campo diverso, il campo deve avere una gerarchia diversa rispetto al campo definito in precedenza (ad esempio, `profile.person.age`). Questa funzione ha lo scopo di evitare conflitti quando gli schemi vengono riuniti in un&#39;unione. Sebbene il vincolo non influisca retroattivamente sugli schemi esistenti, si consiglia vivamente di esaminare gli schemi in caso di conflitti di tipo campo e modificarli come necessario. |
| Convalida dei campi con distinzione tra maiuscole e minuscole | I campi personalizzati sullo stesso livello devono avere nomi diversi, indipendentemente dalle maiuscole. Ad esempio, se aggiungete un campo personalizzato denominato &quot;Email&quot;, non potete aggiungere un altro campo personalizzato allo stesso livello denominato &quot;email&quot;. |

### Problemi noti

* None

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39;interfaccia utente API del Registro di sistema e Editor schema, consultare la documentazione [di sistema](../../xdm/home.md)XDM.

## Servizio Privacy

Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta. Il servizio Adobe Experience Platform Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Il servizio Privacy consente di inviare richieste per l&#39;accesso e l&#39;eliminazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatizzata alle normative sulla privacy legali e organizzative.

### Nuove funzionalità

| Funzione | Descrizione |
|--- | ---|
| Ripristino del servizio sulla privacy | L&#39;ex &quot;GDPR Service&quot; è stato riassegnato al Privacy Service, in quanto il servizio è cresciuto per supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39;API del servizio Privacy è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nuova `regulation` proprietà obbligatoria | Quando si creano nuovi processi nell’API del servizio Privacy, nel payload della richiesta deve essere specificata una `regulation` proprietà per indicare quale regola tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. |
| Supporto per l&#39;autenticazione Adobe Primetime | Il servizio per la privacy ora accetta le richieste di accesso/eliminazione dall&#39;autenticazione Adobe Primetime, utilizzando `primetimeAuthentication` come valore del prodotto. |
| Miglioramenti all’interfaccia utente del servizio sulla privacy | Pagine separate per il monitoraggio dei processi per le normative GDPR e CCPA. Nuovo menu a discesa Tipo __ regolamento per passare dai dati di monitoraggio per GDPR e CCPA. |

### Problemi noti

* None

Per ulteriori informazioni sul servizio Privacy, consultare la panoramica [del servizio](../../privacy-service/home.md)Privacy.

## Origini

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

### Nuove funzionalità

| Funzione | Descrizione |
|--- | ---|
| Supporto per i dati attributo cliente | Supporto dell&#39;interfaccia utente e delle API per la creazione di connettori di streaming per l&#39;acquisizione dei dati attributo del cliente. |
| Supporto aggiuntivo per i formati di file per gli archivi cloud | L&#39;assimilazione dei file dagli archivi cloud ora supporta i formati di file Parquet e JSON conformi a XDM. |
| Supporto per le autorizzazioni di controllo degli accessi | Il framework di controllo degli accessi in Adobe Experience Platform fornisce le autorizzazioni necessarie per concedere l&#39;accesso alle origini nell&#39;assimilazione dei dati. A seconda del livello di autorizzazione, un utente può visualizzare le origini, gestire le origini o negare l&#39;accesso. |

**Autorizzazioni di controllo di accesso**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Ingestione dati | Gestisci origini | Accesso alle origini di lettura, creazione, modifica e disattivazione. |
| Ingestione dati | Visualizza origini | Accesso in sola lettura alle origini disponibili nella scheda *Catalogo* e alle origini autenticate nella scheda *Sfoglia* . |

### Problemi noti

* None

Per ulteriori informazioni sulle origini, consultate la panoramica [delle origini](../../source-connectors/home.md)

## Destinazioni

In [Adobe Real-time CDP](../../rtcdp/overview.md), le destinazioni sono integrazioni pre-costruite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

### Nuove funzionalità

| Funzione | Descrizione |
|--- | ---|
| Supporto per le autorizzazioni di controllo degli accessi | La funzionalità Destinations (Destinazioni) in CDP in tempo reale funziona con le autorizzazioni di controllo degli accessi della piattaforma Adobe Experience. A seconda del livello di autorizzazione dell’utente, potete visualizzare, gestire e attivare le destinazioni. |

**Autorizzazioni di controllo di accesso**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Destinazioni | Gestione destinazioni | Accesso alle destinazioni di lettura, creazione, modifica e disattivazione. |
| Destinazioni | Visualizza destinazioni | Accesso in sola lettura alle destinazioni disponibili nella scheda _Catalogo_ e alle destinazioni autenticate nella scheda _Sfoglia_ . |
| Destinazioni | Attiva destinazioni | Possibilità di attivare i dati sulle destinazioni. Per questa autorizzazione è necessario aggiungere al profilo di prodotto &quot;Gestione destinazioni&quot; o &quot;Visualizza destinazioni&quot;. |

### Problemi noti

* None

Per ulteriori informazioni, consulta la panoramica [](../../rtcdp/destinations/destinations-overview.md) Destinazioni.