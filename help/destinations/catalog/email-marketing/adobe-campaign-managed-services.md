---
title: Connessione Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 2%

---

# Connessione Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Questa integrazione funziona con [Adobe Campaign versione 8.4 o successiva](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Panoramica {#overview}

Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. [Introduzione a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Utilizza Campaign per:

* Stimolare la personalizzazione e il coinvolgimento attraverso un’unica vista accessibile del cliente,
* Integrare nel percorso clienti canali e-mail, mobili, online e offline,
* Automatizza la consegna di messaggi e offerte significativi e tempestivi.

## Guardrail {#guardrails}

Quando si utilizza la connessione Adobe Campaign Managed Cloud Services, tenere presenti le seguenti protezioni:

* Puoi [attivare](#activate) un massimo di 25 tipi di pubblico in questa destinazione.

  È possibile modificare questo limite aggiornando il valore dell&#39;opzione **NmsCdp_Aep_Audience_List_Limit** nella cartella **[!UICONTROL Amministrazione]** > **[!UICONTROL Piattaforma]** > **[!UICONTROL Opzioni]** di Esplora campagne.

* Per ogni pubblico, puoi aggiungere fino a 20 campi per [mappare](#map) ad Adobe Campaign.

  Puoi modificare questo limite aggiornando il valore dell&#39;opzione **NmsCdp_Aep_Destinations_Max_Columns** nella cartella **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** di Campaign Explorer.

* Conservazione dei dati nella zona di destinazione dati (DLZ) dell’archiviazione BLOB di Azure: 7 giorni.
* La frequenza di attivazione è di almeno 3 ore.
* La lunghezza massima del nome file supportata da questa connessione è di 255 caratteri. Quando [configuri il nome del file esportato](../../ui/activate-batch-profile-destinations.md#configure-file-names), accertati che non superi i 255 caratteri. Il superamento della lunghezza massima del nome file causa errori di attivazione.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione del servizio Adobe Campaign Manage, ecco un caso d’uso di esempio che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

* Adobe Experience Platform crea un profilo cliente che incorpora informazioni come il grafico delle identità, dati comportamentali di Analytics, unioni di dati offline e online, ecc. Con questa integrazione, puoi aumentare le funzionalità di segmentazione già esistenti in Adobe Campaign con i tipi di pubblico basati su Adobe Experience Platform e quindi attivare tali dati in Campaign.

  Ad esempio, un’azienda di abbigliamento sportivo vuole sfruttare i tipi di pubblico basati su Adobe Experience Platform e attivarli utilizzando Adobe Campaign per raggiungere la propria base di clienti tra i diversi canali supportati da Adobe Campaign. Una volta inviati i messaggi, desiderano migliorare il profilo del cliente in Adobe Experience Platform con i dati sull’esperienza di Adobe Campaign come invii, apertura e clic.

  Il risultato sono campagne cross-channel più coerenti nell’ecosistema Adobe Experience Cloud e un profilo cliente avanzato che si adatta e apprende rapidamente.


* Oltre all’attivazione del pubblico in Campaign, puoi sfruttare la destinazione Managed Services di Adobe Campaign per inserire attributi di profilo aggiuntivi associati a un profilo su Adobe Experience Platform e disporre di un processo di sincronizzazione in modo che vengano aggiornati nel database di Adobe Campaign.

  Supponiamo ad esempio che tu stia acquisendo valori di consenso e rinuncia in Adobe Experience Platform. Con questa connessione, puoi trasferire questi valori in Adobe Campaign e impostare un processo di sincronizzazione in modo che vengano aggiornati regolarmente.

  >[!NOTE]
  >
  >La sincronizzazione degli attributi del profilo è disponibile per i profili già presenti nel database di Adobe Campaign.

[Ulteriori informazioni sull&#39;integrazione di Adobe Campaign con Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=it)

## Identità supportate {#supported-identities}

*Adobe Campaign Managed Cloud Services* supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| external_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. È consigliabile utilizzare questa identità e mapparla sull’ID nell’istanza Campaign che rappresenta il cliente (loyalty_ID, account_ID, customer_ID...) |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, consulta il seguente documento su [ECID](/help/identity-service/features/ecid.md). |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un pubblico, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Seleziona istanza]**: la tua **[!DNL Campaign]** istanza di marketing.
* **[!UICONTROL Mappatura destinazione]**: selezionare la mappatura di destinazione utilizzata in **[!DNL Adobe Campaign]** per inviare le consegne. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Seleziona tipo di sincronizzazione]**:

   * **[!UICONTROL Sincronizzazione pubblico]**: utilizza questa opzione per inviare i tipi di pubblico di Adobe Experience Platform ad Adobe Campaign.
   * **[!UICONTROL Sincronizzazione profilo (solo aggiornamento)]**: utilizza questa opzione per inserire in Adobe Campaign gli attributi del profilo di Adobe Experience Platform e attivare un processo di sincronizzazione in modo che possano essere aggiornati regolarmente.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

### Politiche di governance e azioni di esecuzione {#governance}

Seleziona le azioni di marketing applicabili ai dati da esportare nella destinazione. Per Adobe Campaign, è consigliabile selezionare l&#39;azione di marketing **[!UICONTROL Targeting e-mail]**.

Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [panoramica dei criteri di utilizzo dei dati](/help/data-governance/policies/overview.md).

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei dati sul pubblico in questa destinazione, leggi [Attiva dati sul pubblico in destinazioni di esportazione del profilo batch](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html).

### Mappare attributi e identità {#map}

Seleziona i campi XDM da esportare con i profili e mappali sui campi Adobe Campaign corrispondenti.[Ulteriori informazioni sulla selezione di identità e attributi per le destinazioni di e-mail marketing](overview.md)

1. Selezionare i campi di origine:

   * Seleziona un **identificatore** (ad esempio, il campo e-mail) come identità di origine che identifica in modo univoco un profilo in Adobe Experience Platform e Adobe Campaign.

   * Seleziona tutti gli altri **attributi del profilo di origine XDM** da esportare in Adobe Campaign.

   >[!NOTE]
   >
   >Il campo &quot;segmentMembershipStatus&quot; è un mapping obbligatorio che riflette lo stato di segmentMembership. Questo campo viene aggiunto per impostazione predefinita e non può essere modificato o rimosso.

1. Mappa ciascun campo con il relativo campo di destinazione in Adobe Campaign. I campi di destinazione disponibili sono determinati dal mapping di destinazione selezionato durante la [creazione della destinazione](#destination-details).

1. Identificare gli attributi obbligatori e le chiavi di deduplicazione. I valori negli attributi contrassegnati come &quot;Obbligatori&quot; o &quot;Chiave di deduplicazione&quot; non possono essere nulli.

   * [Attributi obbligatori](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) assicurati che tutti i record di profilo contengano gli attributi selezionati. Ad esempio: tutti i profili esportati contengono un indirizzo e-mail. Si consiglia di impostare come obbligatorio sia il campo di identità che il campo utilizzato come chiave di deduplicazione.
   * [Una chiave di deduplicazione](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) è una chiave primaria che determina l&#39;identità in base alla quale gli utenti desiderano deduplicare i loro profili.

     >[!IMPORTANT]
     >
     >Assicurati che il nome dell’attributo chiave di deduplicazione corrisponda al nome di colonna della mappatura di destinazione selezionata.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Una volta eseguita la mappatura, è possibile rivedere e completare la configurazione di destinazione per iniziare a inviare dati a **[!DNL Campaign]**.
   [Scopri come rivedere e completare la configurazione della destinazione](/help/destinations/destination-types.md#review).

## Dati esportati / Convalida esportazione dati {#exported-data}

Una volta attivata la destinazione, puoi accedere al processo corrispondente e ai dati esportati in Campaign.

### Monitorare i processi di esportazione dei dati {#jobs}

Passa al menu **[!UICONTROL Amministrazione]** > **[!UICONTROL Audit]** > **[!UICONTROL Processi di caricamento del pubblico]** per monitorare tutti i processi di esportazione attivati da Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Accedere ai dati esportati {#data}

Per **[!UICONTROL Sincronizzazione pubblico]**, puoi controllare il pubblico esportato accedendo al menu **[!UICONTROL Profilo e destinazione]** > **[!UICONTROL Elenco]** > **[!UICONTROL Tipi di pubblico di AEP]**.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Per **[!UICONTROL Sincronizzazione profilo (solo aggiornamento)]**, i dati vengono aggiornati automaticamente nel database di Campaign per ogni profilo di destinazione del pubblico attivato nella destinazione.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
