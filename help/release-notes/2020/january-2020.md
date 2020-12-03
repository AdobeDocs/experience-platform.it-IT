---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 15 gennaio 2020'
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 15 gennaio 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi di Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Limitazioni del tipo di campo per i campi di uguale gerarchia | Dopo che un campo XDM è stato definito come un determinato tipo, tutti gli altri campi con lo stesso nome e la stessa gerarchia devono utilizzare lo stesso tipo di campo, indipendentemente dalle classi o dai mixin in cui sono utilizzati. Ad esempio, se un mixin per la [!DNL Profile] classe XDM contiene un `profile.age` campo di tipo &quot;integer&quot;, un mixin simile per XDM non [!DNL ExperienceEvent] può avere un `profile.age` campo di tipo &quot;string&quot;. Per utilizzare un tipo di campo diverso, il campo deve avere una gerarchia diversa rispetto al campo definito in precedenza (ad esempio, `profile.person.age`). Questa funzione ha lo scopo di evitare conflitti quando gli schemi vengono riuniti in un&#39;unione. Sebbene il vincolo non influisca retroattivamente sugli schemi esistenti, si consiglia vivamente di esaminare gli schemi in caso di conflitti di tipo campo e modificarli come necessario. |
| Convalida dei campi con distinzione tra maiuscole e minuscole | I campi personalizzati sullo stesso livello devono avere nomi diversi, indipendentemente dalle maiuscole. Ad esempio, se aggiungete un campo personalizzato denominato &quot;Email&quot;, non potete aggiungere un altro campo personalizzato allo stesso livello denominato &quot;email&quot;. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39; [!DNL Schema Registry] API e l&#39;interfaccia [!DNL Schema Editor] utente, consulta la documentazione [di sistema](../../xdm/home.md)XDM.

## [!DNL Privacy Service] {#privacy}

Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Con [!DNL Privacy Service]questa opzione puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| [!DNL Privacy Service] rebranding | L&#39;ex &quot;GDPR Service&quot; è stato rinominato [!DNL Privacy Service] in quanto il servizio è cresciuto per supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39; [!DNL Privacy Service] API è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nuova `regulation` proprietà obbligatoria | Durante la creazione di nuovi processi nell&#39; [!DNL Privacy Service] API, nel payload della richiesta deve essere specificata una `regulation` proprietà per indicare quale regola tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. |
| Supporto per [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] accetta ora le richieste di accesso/eliminazione da  Adobe [!DNL Primetime Authentication], utilizzando `primetimeAuthentication` come valore di prodotto. |
| Miglioramenti dell&#39;interfaccia Privacy Service | Pagine separate per il monitoraggio dei processi per le normative GDPR e CCPA. Nuovo **a discesa Tipo di regolamento **per passare dai dati di tracciamento per GDPR e CCPA. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Privacy Service]questo argomento, leggete la panoramica [Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Supporto per i dati attributo cliente | Supporto dell&#39;interfaccia utente e delle API per la creazione di connettori di streaming per l&#39;acquisizione dei dati attributo del cliente. |
| Supporto aggiuntivo per i formati di file per gli archivi cloud | L&#39;assimilazione dei file dagli archivi cloud ora supporta i formati di file Parquet e JSON conformi a XDM. |
| Supporto per le autorizzazioni di controllo degli accessi | Il framework di controllo degli accessi in Adobe Experience Platform fornisce le autorizzazioni necessarie per concedere l&#39;accesso alle origini nell&#39;assimilazione dei dati. A seconda del livello di autorizzazione, un utente può visualizzare le origini, gestire le origini o negare l&#39;accesso. |

**Autorizzazioni di controllo di accesso**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Acquisizione dei dati | Gestisci origini | Accesso alle origini di lettura, creazione, modifica e disattivazione. |
| Acquisizione dei dati | Visualizza origini | Accesso in sola lettura alle origini disponibili nella **[!UICONTROL Catalog]** scheda e alle origini autenticate nella **[!UICONTROL Browse]** scheda. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, consultate la panoramica [delle origini](../../sources/home.md)

## Destinazioni {#destinations}

In CDP [in tempo](../../rtcdp/overview.md)reale, le destinazioni sono integrazioni precostruite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Supporto per le autorizzazioni di controllo degli accessi | La funzionalità Destinazioni in CDP in tempo reale funziona con le autorizzazioni di controllo degli accessi Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, potete visualizzare, gestire e attivare le destinazioni. |

**Autorizzazioni di controllo di accesso**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Destinazioni | Gestione destinazioni | Accesso alle destinazioni di lettura, creazione, modifica e disattivazione. |
| Destinazioni | Visualizza destinazioni | Accesso in sola lettura alle destinazioni disponibili nella **[!UICONTROL Catalog]** scheda e alle destinazioni autenticate nella scheda **Sfoglia** . |
| Destinazioni | Attiva destinazioni | Possibilità di attivare i dati sulle destinazioni. Per questa autorizzazione è necessario aggiungere al profilo di prodotto &quot;Gestione destinazioni&quot; o &quot;Visualizza destinazioni&quot;. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, consulta la panoramica [](../../destinations/home.md) Destinazioni.