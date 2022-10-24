---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2020
description: Le note sulla versione di gennaio 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 15 gennaio 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base della [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che offre informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Restrizioni di tipo campo per i campi della gerarchia uguale | Dopo aver definito un campo XDM come un determinato tipo, tutti gli altri campi con lo stesso nome e la stessa gerarchia devono utilizzare lo stesso tipo di campo, indipendentemente dalle classi o dai gruppi di campi dello schema in cui sono utilizzati. Ad esempio, se un gruppo di campi per XDM [!DNL Profile] la classe contiene `profile.age` campo di tipo &quot;integer&quot;, un gruppo di campi simile per XDM [!DNL ExperienceEvent] non può avere `profile.age` campo di tipo &quot;string&quot;. Per utilizzare un tipo di campo diverso, il campo deve avere una gerarchia diversa rispetto al campo definito in precedenza, ad esempio `profile.person.age`). Questa funzione ha lo scopo di evitare conflitti quando gli schemi vengono riuniti in un’unione. Anche se il vincolo non influisce retroattivamente sugli schemi esistenti, si consiglia vivamente di rivedere gli schemi per i conflitti di tipo campo e modificarli in base alle necessità. |
| Convalida dei campi con distinzione tra maiuscole e minuscole | I campi personalizzati sullo stesso livello devono avere nomi diversi, a prescindere dalle maiuscole. Ad esempio, se aggiungi un campo personalizzato denominato &quot;Email&quot;, non puoi aggiungere un altro campo personalizzato allo stesso livello denominato &quot;email&quot;. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull’utilizzo di XDM con [!DNL Schema Registry] API e [!DNL Schema Editor] interfaccia utente, leggere [Documentazione del sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere ai propri dati o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire queste richieste di dati dai clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| [!DNL Privacy Service] rebranding | Il nome precedentemente denominato &quot;Servizio RGPD&quot; è stato rinominato in [!DNL Privacy Service] poiché il servizio è cresciuto per supportare altre normative oltre al RGPD. |
| Nuovi endpoint API | Percorso di base per [!DNL Privacy Service] L’API è stata aggiornata da `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nuovo obbligatorio `regulation` property | Durante la creazione di nuovi lavori nel [!DNL Privacy Service] API `regulation` la proprietà deve essere fornita nel payload della richiesta per indicare quale regola monitorare il processo in. I valori accettati sono `gdpr` e `ccpa`. |
| Supporto per [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ora accetta richieste di accesso/cancellazione da Adobe [!DNL Primetime Authentication], utilizzando `primetimeAuthentication` come valore del prodotto. |
| Miglioramenti all’interfaccia utente di Privacy Service | Pagine separate per il tracciamento dei processi per i regolamenti RGPD e CCPA. Nuovo elenco a discesa **Regulation Type (Tipo di regolamento) **per passare dai dati di tracciamento per RGPD e CCPA. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni [!DNL Privacy Service], si prega di iniziare leggendo il [Panoramica di Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto per i dati degli attributi del cliente | Supporto per interfaccia utente e API per la creazione di connettori di streaming per l’acquisizione dei dati degli attributi del cliente. |
| Supporto di formati di file aggiuntivi per gli archivi cloud | L’acquisizione di file da archivi cloud ora supporta i formati di file Parquet e JSON conformi a XDM. |
| Supporto per le autorizzazioni di controllo degli accessi | Il framework di controllo degli accessi in Adobe Experience Platform fornisce le autorizzazioni necessarie per concedere l’accesso alle origini nell’acquisizione dei dati. A seconda del livello di autorizzazione, un utente può visualizzare le origini, gestire le origini o ottenere un accesso negato. |

**Autorizzazioni di controllo di accesso**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Acquisizione dei dati | Gestisci origini | Accesso a fonti di lettura, creazione, modifica e disattivazione. |
| Acquisizione dei dati | Visualizza origini | Accesso in sola lettura alle origini disponibili nel **[!UICONTROL Catalogo]** e le origini autenticate nel **[!UICONTROL Sfoglia]** scheda . |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md)

## Destinazioni {#destinations}

In [Real-Time CDP](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto per le autorizzazioni di controllo degli accessi | La funzionalità Destinazioni in Real-Time CDP funziona con le autorizzazioni di controllo accessi di Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, puoi visualizzare, gestire e attivare le destinazioni. |

**Autorizzazioni di controllo di accesso**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Destinazioni | Gestire le destinazioni | Accesso a destinazioni in lettura, creazione, modifica e disattivazione. |
| Destinazioni | Visualizzare le destinazioni | Accesso in sola lettura alle destinazioni disponibili nel **[!UICONTROL Catalogo]** le destinazioni autenticate nel **Sfoglia** scheda . |
| Destinazioni | Attivare le destinazioni | Possibilità di attivare i dati sulle destinazioni. Questa autorizzazione richiede l’aggiunta di &quot;Gestisci destinazioni&quot; o &quot;Visualizza destinazioni&quot; al profilo di prodotto. |

**Problemi noti**

* Nessuna

Consulta la sezione [Panoramica sulle destinazioni](../../destinations/home.md) per ulteriori informazioni.
