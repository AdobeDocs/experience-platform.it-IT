---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2020
description: Note sulla versione di gennaio 2020 per Adobe Experience Platform.
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

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Limitazioni del tipo di campo per i campi della gerarchia uguale | Dopo aver definito un campo XDM come un determinato tipo, tutti gli altri campi con lo stesso nome e gerarchia devono utilizzare lo stesso tipo di campo, indipendentemente dalle classi o dai gruppi di campi dello schema in cui vengono utilizzati. Ad esempio, se un gruppo di campi per XDM [!DNL Profile] la classe contiene un `profile.age` campo di tipo &quot;integer&quot;, un gruppo di campi simile per XDM [!DNL ExperienceEvent] non può avere `profile.age` campo di tipo &quot;string&quot;. Per utilizzare un tipo di campo diverso, il campo deve essere di una gerarchia diversa rispetto al campo definito in precedenza (ad esempio, `profile.person.age`). Questa funzione ha lo scopo di evitare conflitti quando gli schemi vengono riuniti in un’unione. Sebbene il vincolo non influisca retroattivamente sugli schemi esistenti, si consiglia vivamente di rivedere gli schemi per i conflitti di tipo campo e modificarli in base alle esigenze. |
| Convalida del campo con distinzione tra maiuscole e minuscole | I campi personalizzati dello stesso livello devono avere nomi diversi, indipendentemente dalle maiuscole. Ad esempio, se aggiungi un campo personalizzato denominato &quot;E-mail&quot;, non puoi aggiungere un altro campo personalizzato allo stesso livello denominato &quot;e-mail&quot;. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM con [!DNL Schema Registry] API e [!DNL Schema Editor] dell&#39;interfaccia utente, leggere il [Documentazione del sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere ai propri dati o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| [!DNL Privacy Service] rebranding | Il servizio precedentemente denominato &quot;GDPR Service&quot; è stato rinominato in [!DNL Privacy Service] in quanto il servizio è cresciuto fino a supportare altre normative oltre al RGPD. |
| Nuovi endpoint API | Percorso di base per [!DNL Privacy Service] L’API è stata aggiornata da `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nuovo obbligatorio `regulation` proprietà | Quando si creano nuovi processi in [!DNL Privacy Service] API, a `regulation` La proprietà deve essere fornita nel payload della richiesta per indicare in quale regolamento tracciare il processo. I valori accettati sono `gdpr` e `ccpa`. |
| Supporto per [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ora accetta le richieste di accesso/eliminazione da Adobe [!DNL Primetime Authentication], utilizzando `primetimeAuthentication` come valore del prodotto. |
| Miglioramenti all’interfaccia utente di Privacy Service | Pagine di tracciamento del lavoro separate per le normative RGPD e CCPA. Nuovo **Tipo di regolamento **a discesa per passare dai dati di tracciamento per RGPD e CCPA e viceversa. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Privacy Service], inizia leggendo il [Panoramica di Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di configurare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto per i dati degli attributi del cliente | Supporto di interfaccia utente e API per la creazione di connettori di streaming per l’acquisizione dei dati degli attributi del cliente. |
| Supporto di formati di file aggiuntivi per gli archivi cloud | L’acquisizione di file da archivi cloud ora supporta i formati di file Parquet e JSON conformi a XDM. |
| Supporto per le autorizzazioni di controllo degli accessi | Il framework di controllo degli accessi in Adobe Experience Platform fornisce le autorizzazioni necessarie per concedere l’accesso alle origini nell’acquisizione dei dati. A seconda del loro livello di autorizzazione, un utente può visualizzare le origini, gestirle o vederne negato l’accesso. |

**Autorizzazioni di controllo degli accessi**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Acquisizione dei dati | Gestisci origini | Accesso per leggere, creare, modificare e disabilitare le origini. |
| Acquisizione dei dati | Visualizza origini | Accesso in sola lettura alle origini disponibili in **[!UICONTROL Catalogo]** e le origini autenticate in **[!UICONTROL Sfoglia]** scheda. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, vedere [panoramica sulle origini](../../sources/home.md)

## Destinazioni {#destinations}

In entrata [Real-Time CDP](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto per le autorizzazioni di controllo degli accessi | La funzionalità Destinazioni di Real-Time CDP funziona con le autorizzazioni di controllo degli accessi di Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, è possibile visualizzare, gestire e attivare le destinazioni. |

**Autorizzazioni di controllo degli accessi**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Destinazioni | Gestire le destinazioni | Accesso a destinazioni di lettura, creazione, modifica e disattivazione. |
| Destinazioni | Visualizza destinazioni | Accesso in sola lettura alle destinazioni disponibili in **[!UICONTROL Catalogo]** e le destinazioni autenticate in **Sfoglia** scheda. |
| Destinazioni | Attivare le destinazioni | Possibilità di attivare i dati nelle destinazioni. Questa autorizzazione richiede l’aggiunta di &quot;Gestisci destinazioni&quot; o &quot;Visualizza destinazioni&quot; al profilo di prodotto. |

**Problemi noti**

* Nessuna

Consulta la [Panoramica sulle destinazioni](../../destinations/home.md) per ulteriori informazioni.
