---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2020
description: Note sulla versione di Adobe Experience Platform di gennaio 2020.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 14%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 15 gennaio 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull&#39;esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Limitazioni del tipo di campo per i campi della gerarchia uguale | Dopo aver definito un campo XDM come un determinato tipo, tutti gli altri campi con lo stesso nome e gerarchia devono utilizzare lo stesso tipo di campo, indipendentemente dalle classi o dai gruppi di campi dello schema in cui vengono utilizzati. Ad esempio, se un gruppo di campi per la classe XDM [!DNL Profile] contiene un campo `profile.age` di tipo &quot;integer&quot;, un gruppo di campi simile per XDM [!DNL ExperienceEvent] non può avere un campo `profile.age` di tipo &quot;string&quot;. Per utilizzare un tipo di campo diverso, il campo deve essere di una gerarchia diversa rispetto al campo definito in precedenza, ad esempio `profile.person.age`. Questa funzione ha lo scopo di evitare conflitti quando gli schemi vengono riuniti in un’unione. Sebbene il vincolo non influisca retroattivamente sugli schemi esistenti, si consiglia vivamente di rivedere gli schemi per i conflitti di tipo campo e modificarli in base alle esigenze. |
| Convalida del campo con distinzione tra maiuscole e minuscole | I campi personalizzati dello stesso livello devono avere nomi diversi, indipendentemente dalle maiuscole. Ad esempio, se aggiungi un campo personalizzato denominato &quot;E-mail&quot;, non puoi aggiungere un altro campo personalizzato allo stesso livello denominato &quot;e-mail&quot;. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM con l&#39;API [!DNL Schema Registry] e l&#39;interfaccia utente [!DNL Schema Editor], leggere la [documentazione del sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Nuove norme legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi di dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire queste richieste di dati dei clienti. Con [!DNL Privacy Service] è possibile inviare richieste di accesso ed eliminazione di dati personali o privati dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| [!DNL Privacy Service] rebranding | Il servizio precedentemente denominato &quot;GDPR Service&quot; è stato rinominato [!DNL Privacy Service] in quanto è cresciuto fino a supportare altre normative oltre al GDPR. |
| Nuovi endpoint API | Il percorso di base per l&#39;API [!DNL Privacy Service] è stato aggiornato da `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nuova proprietà `regulation` richiesta | Quando si creano nuovi processi nell&#39;API [!DNL Privacy Service], è necessario fornire una proprietà `regulation` nel payload della richiesta per indicare in quale regolamento tenere traccia del processo. I valori accettati sono `gdpr` e `ccpa`. |
| Supporto per [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ora accetta le richieste di accesso/eliminazione dall&#39;Adobe [!DNL Primetime Authentication], utilizzando `primetimeAuthentication` come valore di prodotto. |
| Miglioramenti all’interfaccia utente di Privacy Service | Pagine di tracciamento del lavoro separate per le normative RGPD e CCPA. Nuovo **Tipo di regolamento **a discesa per passare dai dati di tracciamento per RGPD e CCPA e viceversa. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Privacy Service], leggere la [panoramica Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

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
| Acquisizione dei dati | Visualizza origini | Accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalogo]** e alle origini autenticate nella scheda **[!UICONTROL Sfoglia]**. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md)

## Destinazioni {#destinations}

In [Real-Time CDP](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto per le autorizzazioni di controllo degli accessi | La funzionalità Destinazioni di Real-Time CDP funziona con le autorizzazioni di controllo degli accessi di Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, è possibile visualizzare, gestire e attivare le destinazioni. |

**Autorizzazioni di controllo degli accessi**

| Categoria | Autorizzazione | Descrizione |
|--- | --- | ---|
| Destinazioni | Gestire le destinazioni | Accesso a destinazioni di lettura, creazione, modifica e disattivazione. |
| Destinazioni | Visualizza destinazioni | Accesso in sola lettura alle destinazioni disponibili nella scheda **[!UICONTROL Catalogo]** e alle destinazioni autenticate nella scheda **Sfoglia**. |
| Destinazioni | Attivare le destinazioni | Possibilità di attivare i dati nelle destinazioni. Questa autorizzazione richiede l’aggiunta di &quot;Gestisci destinazioni&quot; o &quot;Visualizza destinazioni&quot; al profilo di prodotto. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, consulta la [Panoramica sulle destinazioni](../../destinations/home.md).
