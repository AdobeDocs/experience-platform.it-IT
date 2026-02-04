---
title: Acxiom Audience Connection
description: Utilizza la destinazione  [!DNL Acxiom Audience Connection]  per migliorare i tipi di pubblico con la tecnologia  [!DNL Acxiom's Real ID] e attivare i tipi di pubblico su più piattaforme, ad esempio  [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.
badge: label="Beta" type="Informative"
exl-id: bac0f337-bfab-4779-acc8-f70239552666
source-git-commit: 582b8b681163a0e40908cf36ba317954a32f73d0
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 7%

---

# Destinazione [!DNL Acxiom Audience Connection]

>[!NOTE]
>
>La destinazione [!DNL Acxiom Audience Connection] è in versione beta. Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Acxiom]. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente Acxiom [qui](mailto:acxiom-adobe-help@acxiom.com).

Utilizza la destinazione [!DNL Acxiom Audience Connection] per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) e attivare i tipi di pubblico su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

Questo tutorial fornisce istruzioni per creare un connettore di destinazione [!DNL Acxiom Audience Connection] utilizzando l&#39;interfaccia utente [!DNL Adobe Experience Platform]. Questo connettore viene utilizzato per generare e distribuire i tipi di pubblico alle destinazioni selezionate.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Acxiom Audience Connection], ecco un caso d&#39;uso di esempio che i clienti [!DNL Adobe Experience Platform] possono risolvere utilizzando questo connettore.

### Inviare tipi di pubblico da Experience Platform al tuo account Acxiom {#send-audiences}

Utilizza questo connettore di destinazione se sei un professionista del marketing che desidera inviare tipi di pubblico da [!DNL Experience Platform] al tuo account [!DNL Acxiom] per l&#39;acquisizione cross-channel.

Ad esempio, il reparto Marketing Operations di un brand di servizi finanziari globali è interessato all’acquisizione dei clienti cross-channel attraverso più piattaforme pubblicitarie. Possono utilizzare il connettore di destinazione [!DNL Acxiom Audience Connection] per inviare tipi di pubblico da [!DNL Experience Platform] a [!DNL Acxiom], migliorarli con la tecnologia [!DNL Acxiom's Real ID] e attivarli su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

## Prerequisiti {#prerequisites}

* **Conferma le condizioni per l&#39;utilizzo:** Prima di poter configurare una nuova destinazione [!DNL Acxiom Audience Connection], è necessario leggere e firmare il Contratto sulle condizioni per l&#39;utilizzo di [!DNL Acxiom's]. Riceverai il collegamento al contratto una volta completato l&#39;ordine cliente eseguito.
* **Conoscere l&#39;ID organizzazione Adobe:** Per completare i termini del Contratto utente è necessario l&#39;ID organizzazione [!DNL Adobe]. Consulta l&#39;argomento [!DNL Adobe's] *Organizzazioni in Experience Cloud* per informazioni su come [visualizzare l&#39;ID organizzazione](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

## Destinazioni supportate {#supported-destinations}

La destinazione [!DNL Acxiom Audience Connection] attualmente supporta l&#39;attivazione del pubblico per le seguenti piattaforme.<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Connettersi alla destinazione {#connect}

L&#39;autenticazione alla destinazione [!DNL Acxiom's Audience Connection] viene gestita automaticamente dietro le quinte per comodità.

## Impostazioni specifiche per la destinazione {#destination-settings}

Alcune destinazioni di [!DNL Acxiom Audience Connection] richiedono ulteriori informazioni. Le sezioni seguenti forniscono indicazioni dettagliate su come configurare queste opzioni.

### [!DNL LG Ads] {#lg-ads}

Per configurare i dettagli per la destinazione, compila i campi seguenti.

* **Categoria segmento**: la categoria di destinazione o verticale in cui rientra il segmento. Esempio: servizi finanziari, settore automobilistico, sanità, ecc.

![Dettagli destinazione LG Ads](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

>[!NOTE]
>
>La destinazione [!DNL Acxiom Audience Connection] supporta solo esportazioni di file complete.

### Mappare attributi e identità {#map}

Affinché la destinazione [!DNL Acxiom Audience Connection] riceva correttamente i dati sul pubblico, è necessario mappare i campi di origine da Experience Platform ai campi di destinazione [!DNL Acxiom Audience Connection] corretti.

[!DNL Acxiom Audience Connection] consente la mappatura solo ai seguenti campi di destinazione. I campi di destinazione descritti nella tabella seguente devono essere mappati nell’ordine indicato di seguito.

| Nome campo | Descrizione | Obbligatorio | Ordine campi | Lunghezza massima |
|---|---|---|---|---|          
| Nome | Nome della persona | No | 1 | 255 |
| In mezzo | Secondo nome o iniziale dell’individuo | No | 2 | 50 |
| Cognome | Cognome della persona | Sì | 3 | 255 |
| Suffisso generazionale | Suffisso dell’individuo | No | 4 | 10 |
| Indirizzo 1 | Indirizzo 1 campo di residenza primaria | Sì | 5 | 255 |
| Indirizzo 2 | Indirizzo 2 campo di residenza primaria | No | 6 | 255 |
| Città | Città di residenza primaria | Sì | 7 | 255 |
| Stato | Abbreviazione statale della residenza primaria | Sì | 8 | 2 |
| Codice postale | Codice postale completo della residenza principale | Sì | 9 | 10 |
| E-mail | E-mail principale Per impostazione predefinita, questo campo viene utilizzato come chiave di deduplicazione per rendere univoci i record | No | 10 | 255 |
| Telefono | Numero di telefono del singolo utente (prefisso + numero)<br> Per impostazione predefinita, questo campo viene utilizzato come chiave di deduplicazione per rendere univoci i record. | No | 11 | 10 |

Nella colonna **[!UICONTROL Source Field]** immettere il nome di ogni attributo di origine che si desidera mappare al campo di destinazione corrispondente oppure selezionare l&#39;icona freccia per aprire la schermata **[!UICONTROL  Select source field]**.<br>
![Schermata di mappatura](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

Dopo aver mappato tutti i campi, selezionare **[!UICONTROL Next]**.

Se non utilizzi lo schema standard [!DNL Adobe's], consulta la [guida dell&#39;interfaccia utente di Query Service](../../../query-service/ui/overview.md) per informazioni su come utilizzare il servizio di query per popolare lo schema standard [!DNL Adobe] con i tuoi nomi di campo.

### Rivedi {#review}

Dopo aver completato tutti i passaggi precedenti, puoi rivedere lo stato della connessione di destinazione e i dettagli del pubblico prima di attivarla (distribuirla). I tipi di pubblico selezionati verranno visualizzati nella parte inferiore di un elenco. Ogni pubblico sarà una chiamata separata all&#39;API [!DNL Acxiom Audience Connection].

Se i risultati sono soddisfacenti, selezionare **[!UICONTROL Finish]** per attivare la destinazione.

![Rivedi il pubblico](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## Risoluzione dei problemi {#troubleshooting}

Se il rappresentante di destinazione non è in grado di individuare il pubblico, contattare il rappresentante [!DNL Adobe] per assistenza.

È necessario fornire le seguenti informazioni al rappresentante [!DNL Adobe]:

* Nome del pubblico
* Nome destinazione
* Data di attivazione del pubblico
* Nome file esportato

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai attivato correttamente un pubblico sulla piattaforma di destinazione selezionata. Quindi, contatta il rappresentante della piattaforma di destinazione per iniziare a configurare la campagna.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).
