---
title: Distribuzione del pubblico di Acxiom
description: Utilizza la destinazione  [!DNL Acxiom Audience Distribution]  per migliorare i tipi di pubblico con la tecnologia  [!DNL Acxiom's Real ID] e attivare i tipi di pubblico su più piattaforme, ad esempio  [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.
badge: Beta
source-git-commit: 7db60161b638cce1845c430f6086441599a0bc61
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 6%

---


# [!DNL Acxiom Audience Distribution] destinazione

>[!NOTE]
>
>La destinazione [!DNL Acxiom Audience Distribution] è in versione beta. Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Acxiom]. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente Acxiom [qui](mailto:acxiom-adobe-help@acxiom.com).

Utilizza la destinazione [!DNL Acxiom Audience Distribution] per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) e attivare i tipi di pubblico su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

Questo tutorial fornisce istruzioni per creare un connettore di destinazione [!DNL Acxiom Audience Distribution] utilizzando l&#39;interfaccia utente [!DNL Adobe Experience Platform]. Questo connettore viene utilizzato per generare e distribuire i tipi di pubblico alle destinazioni selezionate.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Acxiom Audience Distribution], ecco un caso d&#39;uso di esempio che i clienti [!DNL Adobe Experience Platform] possono risolvere utilizzando questo connettore.

### Inviare tipi di pubblico da Experience Platform all’account Acxiom {#send-audiences}

Utilizza questo connettore di destinazione se sei un professionista del marketing che desidera inviare tipi di pubblico da [!DNL Experience Platform] al tuo account [!DNL Acxiom] per l&#39;acquisizione cross-channel.

Ad esempio, il reparto Marketing Operations di un brand di servizi finanziari globali è interessato all’acquisizione dei clienti cross-channel attraverso più piattaforme pubblicitarie. Possono utilizzare il connettore di destinazione [!DNL Acxiom Audience Distribution] per inviare tipi di pubblico da [!DNL Experience Platform] a [!DNL Acxiom], migliorarli con la tecnologia [!DNL Acxiom's Real ID] e attivarli su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

## Prerequisiti {#prerequisites}

* **Conferma le condizioni per l&#39;utilizzo:** Prima di poter configurare una nuova destinazione [!DNL Acxiom Audience Distribution], è necessario leggere e firmare il Contratto sulle condizioni per l&#39;utilizzo di [!DNL Acxiom's]. Riceverai il collegamento al contratto una volta completato l&#39;ordine cliente eseguito. Fino alla firma del contratto, la scheda di destinazione [!DNL Acxiom Audience Distribution] non verrà visualizzata nel catalogo di destinazione di Experience Platform. Dopo aver accettato e firmato il contratto, [!DNL Adobe] completerà il processo di onboarding e verrà visualizzata la scheda di destinazione [!DNL Acxiom Audience Distribution].
* **Conoscere l&#39;ID organizzazione Adobe:** L&#39;ID organizzazione [!DNL Adobe] è necessario per completare le Condizioni d&#39;uso. Consulta l&#39;argomento [!DNL Adobe's] *Organizzazioni in Experience Cloud* per informazioni su come [visualizzare l&#39;ID organizzazione](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

## Destinazioni supportate {#supported-destinations}

La destinazione [!DNL Acxiom Audience Distribution] attualmente supporta l&#39;attivazione del pubblico per le seguenti piattaforme.<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Connettersi alla destinazione {#connect}

L&#39;autenticazione alla destinazione [!DNL Acxiom's Audience Distribution] viene gestita automaticamente dietro le quinte per comodità.

## Impostazioni specifiche per la destinazione {#destination-settings}

Alcune destinazioni di [!DNL Acxiom Audience Distribution] richiedono ulteriori informazioni. Le sezioni seguenti forniscono indicazioni dettagliate su come configurare queste opzioni.

### [!DNL LG Ads] {#lg-ads}

Per configurare i dettagli per la destinazione, compila i campi seguenti.

* **Categoria segmento**: la categoria di destinazione o verticale in cui rientra il segmento. Esempio: servizi finanziari, settore automobilistico, sanità, ecc.

![Dettagli destinazione LG Ads](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

>[!NOTE]
>
>La destinazione [!DNL Acxiom Audience Distribution] supporta solo esportazioni di file complete.

### Mappare attributi e identità {#map}

Affinché la destinazione [!DNL Acxiom Audience Distribution] riceva correttamente i dati del pubblico, è necessario mappare i campi di origine da Experience Platform ai campi di destinazione [!DNL Acxiom Audience Distribution] corretti.

[!DNL Acxiom Audience Distribution] consente la mappatura solo ai seguenti campi di destinazione. I campi di destinazione descritti nella tabella seguente devono essere mappati nell’ordine indicato di seguito.

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

Nella colonna **[!UICONTROL Campo Source]** immettere il nome di ogni attributo di origine che si desidera mappare al campo di destinazione corrispondente oppure selezionare l&#39;icona freccia per aprire la schermata **[!UICONTROL Seleziona campo di origine]**.<br>
![Schermata di mappatura](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

Dopo aver mappato tutti i campi, seleziona **[!UICONTROL Avanti]**.

Se non utilizzi lo schema standard [!DNL Adobe's], consulta la [guida dell&#39;interfaccia utente di Query Service](../../../query-service/ui/overview.md) per informazioni su come utilizzare il servizio di query per popolare lo schema standard [!DNL Adobe] con i tuoi nomi di campo.

### Controlla {#review}

Dopo aver completato tutti i passaggi precedenti, puoi rivedere lo stato della connessione di destinazione e i dettagli del pubblico prima di attivarla (distribuirla). I tipi di pubblico selezionati verranno visualizzati nella parte inferiore di un elenco. Ogni pubblico sarà una chiamata separata all&#39;API [!DNL Acxiom Audience Distribution].

Se sei soddisfatto dei risultati, seleziona **[!UICONTROL Fine]** per attivare la destinazione.

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


