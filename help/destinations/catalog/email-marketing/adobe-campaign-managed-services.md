---
title: Connessione Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 4%

---

# Connessione Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Questa integrazione funziona con [Adobe Campaign versione 8.4 o successiva](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Panoramica {#overview}

Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. [Introduzione a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Utilizza Campaign per:
* Stimolare la personalizzazione e il coinvolgimento attraverso un’unica vista accessibile del cliente,
* Integrare nel percorso cliente canali e-mail, mobili, online e offline,
* Automatizzare la consegna di messaggi e offerte significativi e tempestivi.

>[!IMPORTANT]
>
>Quando si utilizza la connessione Adobe Campaign Managed Cloud Services, tenere presenti le seguenti protezioni:
>
>* È possibile creare fino a 50 segmenti [attivato](#activate) per la destinazione,
>* Per ogni segmento, puoi aggiungere fino a 20 campi per [mappa](#map) ad Adobe Campaign,
>* Conservazione dei dati in Azure Blob Storage Data Landing Zone (DLZ): 7 giorni,
>* La frequenza di attivazione è di almeno 3 ore.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione del servizio Adobe Campaign Manage, ecco un caso d’uso di esempio che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

* Adobe Experience Platform crea un profilo cliente che incorpora informazioni come il grafico delle identità, dati comportamentali di Analytics, unioni di dati offline e online, ecc. Con questa integrazione, puoi aumentare le funzionalità di segmentazione già esistenti in Adobe Campaign con i tipi di pubblico basati su Adobe Experience Platform e quindi attivare tali dati in Campaign.

  Ad esempio, un’azienda di abbigliamento sportivo vuole sfruttare i segmenti avanzati basati su Adobe Experience Platform e attivarli utilizzando Adobe Campaign per raggiungere la propria base clienti tra i diversi canali supportati da Adobe Campaign. Una volta inviati i messaggi, desiderano migliorare il profilo del cliente in Adobe Experience Platform con i dati sull’esperienza di Adobe Campaign come invii, apertura e clic.

  Il risultato sono campagne cross-channel più coerenti nell’ecosistema Adobe Experience Cloud e un profilo cliente avanzato che si adatta e apprende rapidamente.


* Oltre all’attivazione dei segmenti in Campaign, puoi sfruttare la destinazione di Adobe Campaign Managed Services per inserire attributi di profilo aggiuntivi, legati a un profilo su Adobe Experience Platform, che dispongono di un processo di sincronizzazione che consente di aggiornarli nel database di Adobe Campaign.

  Supponiamo ad esempio che tu stia acquisendo valori di consenso e rinuncia in Adobe Experience Platform. Con questa connessione, puoi trasferire questi valori in Adobe Campaign e impostare un processo di sincronizzazione in modo che vengano aggiornati regolarmente.

  >[!NOTE]
  >
  >La sincronizzazione degli attributi del profilo è disponibile per i profili già presenti nel database di Adobe Campaign.

[Ulteriori informazioni sull’integrazione di Adobe Campaign con Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=it)

## Identità supportate {#supported-identities}

*Adobe Campaign Managed Cloud Services* supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| external_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. È consigliabile utilizzare questa identità e mapparla sull’ID nell’istanza Campaign che rappresenta il cliente (loyalty_ID, account_ID, customer_ID...) |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| GAID | Google Advertising ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Seleziona istanza]**: il tuo **[!DNL Campaign]** istanza di marketing.
* **[!UICONTROL Mappatura target]**: seleziona la mappatura di destinazione in uso **[!DNL Adobe Campaign]** per inviare consegne. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Seleziona tipo di sincronizzazione]**:

   * **[!UICONTROL Sincronizzazione pubblico]**: utilizza questa opzione per inviare il pubblico di Adobe Experience Platform ad Adobe Campaign.
   * **[!UICONTROL Sincronizzazione profilo (solo aggiornamento)]**: utilizza questa opzione per inserire in Adobe Campaign gli attributi del profilo Adobe Experience Platform e disporre di un processo di sincronizzazione in modo che possano essere aggiornati regolarmente.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

### Politiche di governance e azioni di esecuzione {#governance}

Seleziona le azioni di marketing applicabili ai dati da esportare nella destinazione. Per Adobe Campaign, è consigliabile selezionare **[!UICONTROL Targeting e-mail]** azione di marketing.

Per ulteriori informazioni sulle azioni di marketing, vedi [panoramica dei criteri di utilizzo dei dati](/help/data-governance/policies/overview.md) pagina.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=it) per istruzioni sull’attivazione dei dati sul pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Seleziona i campi XDM da esportare con i profili e mappali sui campi Adobe Campaign corrispondenti.[Ulteriori informazioni sulla selezione di identità e attributi per le destinazioni di e-mail marketing](overview.md)

1. Selezionare i campi di origine:

   * Seleziona un **identificatore** (ad esempio: il campo e-mail) come identità di origine che identifica in modo univoco un profilo in Adobe Experience Platform e Adobe Campaign.

   * Seleziona tutti gli altri **Attributi del profilo sorgente XDM** che devono essere esportati in Adobe Campaign.

   >[!NOTE]
   >
   >Il campo &quot;segmentMembershipStatus&quot; è un mapping obbligatorio che riflette lo stato di segmentMembership. Questo campo viene aggiunto per impostazione predefinita e non può essere modificato o rimosso.

1. Mappa ciascun campo con il relativo campo di destinazione in Adobe Campaign. I campi di destinazione disponibili sono determinati dalla mappatura di destinazione selezionata quando [creazione della destinazione](#destination-details).

1. Identificare gli attributi obbligatori e le chiavi di deduplicazione. I valori negli attributi contrassegnati come &quot;Obbligatori&quot; o &quot;Chiave di deduplicazione&quot; non possono essere nulli.

   * [Attributi obbligatori](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) assicurarsi che tutti i record profilo contengano gli attributi selezionati. Ad esempio: tutti i profili esportati contengono un indirizzo e-mail. Si consiglia di impostare come obbligatorio sia il campo di identità che il campo utilizzato come chiave di deduplicazione.
   * [Una chiave di deduplicazione](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) è una chiave primaria che determina l’identità in base alla quale gli utenti desiderano deduplicare i propri profili.

     >[!IMPORTANT]
     >
     >Assicurati che il nome dell’attributo chiave di deduplicazione corrisponda al nome di colonna della mappatura di destinazione selezionata.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Una volta eseguita la mappatura, puoi rivedere e completare la configurazione di destinazione per iniziare a inviare dati a **[!DNL Campaign]**.
   [Scopri come rivedere e completare la configurazione della destinazione](/help/destinations/destination-types.md#review).

## Dati esportati / Convalida esportazione dati {#exported-data}

Una volta attivata la destinazione, puoi accedere al processo corrispondente e ai dati esportati in Campaign.

### Monitorare i processi di esportazione dei dati {#jobs}

Accedi a **[!UICONTROL Amministrazione]** > **[!UICONTROL Audit]** > **[!UICONTROL Processi di caricamento del pubblico]** per monitorare tutti i processi di esportazione attivati da Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Accedere ai dati esportati {#data}

Per **[!UICONTROL Sincronizzazione pubblico]**, puoi controllare il pubblico esportato accedendo al **[!UICONTROL Profilo e destinazione]** > **[!UICONTROL Elenco]** > **[!UICONTROL Pubblico AEP]** menu.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Per **[!UICONTROL Sincronizzazione profilo (solo aggiornamento)]**, i dati vengono aggiornati automaticamente nel database di Campaign per ogni profilo di destinazione del segmento attivato nella destinazione.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
