---
title: Connessione pubblico Acxiom Real ID
description: Utilizza la destinazione  [!DNL Acxiom Real ID Audience Connection]  per migliorare i tipi di pubblico con la tecnologia  [!DNL Acxiom's Real ID] e attivare i tipi di pubblico su più piattaforme, ad esempio  [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.
badge: label="Beta" type="Informative"
exl-id: 5f1f0f7f-ac46-42bd-8002-be50fab5a76b
source-git-commit: 582b8b681163a0e40908cf36ba317954a32f73d0
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 6%

---

# Destinazione [!DNL Acxiom Real ID Audience Connection]

>[!NOTE]
>
>La destinazione [!DNL Acxiom Real ID Audience Connection] è in versione beta. Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Acxiom]. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente Acxiom [qui](mailto:acxiom-adobe-help@acxiom.com).

Utilizza la destinazione [!DNL Acxiom Real ID Audience Connection] per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) e attivare i tipi di pubblico su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

Questo tutorial fornisce istruzioni per creare un connettore di destinazione [!DNL Acxiom Real ID Audience Connection] utilizzando l&#39;interfaccia utente [!DNL Adobe Experience Platform]. Questo connettore viene utilizzato per generare e distribuire i tipi di pubblico alle destinazioni selezionate.

## Casi d’uso {#use-cases}

Questo connettore supporta i client che hanno Acxiom Real Identity caricato in Real-Time CDP come identificatore. Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Acxiom Real ID Audience Connection], ecco un caso d&#39;uso di esempio che i clienti [!DNL Adobe Experience Platform] possono risolvere utilizzando questo connettore.

### Inviare tipi di pubblico da Experience Platform al tuo account Acxiom {#send-audiences}

Utilizza questo connettore di destinazione se sei un professionista del marketing che desidera inviare tipi di pubblico da [!DNL Experience Platform] al tuo account [!DNL Acxiom] per l&#39;acquisizione cross-channel.

Ad esempio, il reparto Marketing Operations di un brand di servizi finanziari globali è interessato all’acquisizione dei clienti cross-channel attraverso più piattaforme pubblicitarie. Possono utilizzare il connettore di destinazione [!DNL Acxiom Real ID Audience Connection] per inviare tipi di pubblico da [!DNL Experience Platform] a [!DNL Acxiom], migliorarli con la tecnologia [!DNL Acxiom's Real ID] e attivarli su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.


## Prerequisiti {#prerequisites}

* **Conferma le condizioni per l&#39;utilizzo:** Prima di poter configurare una nuova destinazione [!DNL Acxiom Real ID Audience Connection], è necessario leggere e firmare il Contratto sulle condizioni per l&#39;utilizzo di [!DNL Acxiom's]. Riceverai il collegamento al contratto una volta completato l&#39;ordine cliente eseguito.
* **Conoscere l&#39;ID organizzazione Adobe:** Per completare i termini del Contratto utente è necessario l&#39;ID organizzazione [!DNL Adobe]. Consulta l&#39;argomento [!DNL Adobe's] *Organizzazioni in Experience Cloud* per informazioni su come [visualizzare l&#39;ID organizzazione](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Ottenere la licenza per [!DNL Acxiom's Real ID] prodotto:** Una volta ottenuta la licenza, rendere disponibile il Real ID di Acxiom in Real-Time CDP. Per ulteriori informazioni, vedere [Acxiom Data Enhancement](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/catalog/data-partner/acxiom-data-enhancement).


## Identità supportate {#supported-identities}

La destinazione [!DNL Acxiom's Real ID Audience Connection] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/it/docs/experience-platform/identity/features/namespaces).

| Identità di destinazione | Descrizione | Considerazioni |
|---------------|----------------|----------------|
| ID reale | [!DNL Acxiom Real ID] | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi Acxiom Real ID. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------------|----------------|----------------|
| Servizio di segmentazione | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/home). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/ui/audience-portal#import-audience) in Experience Platform da file CSV. |


## Destinazioni supportati {#supported-destinations}

La destinazione [!DNL Acxiom's Real ID Audience Connection] supporta attualmente l&#39;attivazione del pubblico per le seguenti piattaforme.

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Connettersi alla destinazione {#connect}

L&#39;autenticazione alla destinazione [!DNL Acxiom's Real ID Audience Connection] viene gestita automaticamente dietro le quinte per comodità.

## Impostazioni specifiche per la destinazione {#destination-settings}

Alcune destinazioni di [!DNL Acxiom Real ID Audience Connection] richiedono ulteriori informazioni. Le sezioni seguenti forniscono indicazioni dettagliate su come configurare queste opzioni.

### [!DNL LG Ads] {#lg-ads}

Per configurare i dettagli per la destinazione, compila i campi seguenti.

* **Categoria segmento**: la categoria di destinazione o verticale in cui rientra il segmento. Esempio: servizi finanziari, settore automobilistico, sanità, ecc.

![Dettagli destinazione LG Ads](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png)


## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}



Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations).

>[!NOTE]
>
>La destinazione [!DNL Acxiom Real ID Audience Connection] supporta solo esportazioni di file complete.


### Mappare attributi e identità {#map}

Affinché la destinazione [!DNL Acxiom Real ID Audience Connection] riceva correttamente i dati sul pubblico, è necessario mappare il campo di origine da Experience Platform al campo di destinazione [!DNL Acxiom Real ID Audience Connection] corretto.

[!DNL Acxiom Real ID Audience Connection] consente solo la mappatura al seguente campo di destinazione.

| Nome campo | Descrizione | Obbligatorio |
|--------------------|------------|--------| 
| ID reale | Un Real ID è un identificatore alfanumerico (ID) univoco a 36 byte dal grafo di risoluzione delle identità proprietario di Acxiom, simile a una chiave primaria per un database relazionale. È un identificatore che rappresenta una persona, una famiglia o un indirizzo. | Sì |



Nella colonna **[!UICONTROL Source Field]** immettere il nome dell&#39;attributo di origine che si desidera mappare al campo di destinazione corrispondente oppure selezionare l&#39;icona freccia per aprire la schermata **[!UICONTROL &#x200B; Select source field]**. Quindi, selezionare **[!UICONTROL Next]**.
![Schermata di mappatura](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png)


Se non utilizzi lo schema standard [!DNL Adobe's], consulta la [guida dell&#39;interfaccia utente di Query Service](../../../query-service/ui/overview.md) per informazioni su come utilizzare il servizio di query per popolare lo schema standard [!DNL Adobe] con i tuoi nomi di campo.


### Rivedi {#review}

Dopo aver completato tutti i passaggi precedenti, puoi rivedere lo stato della connessione di destinazione e i dettagli del pubblico prima di attivarla (distribuirla). I tipi di pubblico selezionati verranno visualizzati nella parte inferiore di un elenco. Ogni pubblico sarà una chiamata separata all&#39;API [!DNL Acxiom Real ID Audience Connection].

Se i risultati sono soddisfacenti, selezionare **[!UICONTROL Finish]** per attivare la destinazione.

![Rivedi il pubblico](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png)


## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/it/docs/experience-platform/data-governance/home).

## Risoluzione dei problemi {#troubleshooting}

Se il rappresentante di destinazione non è in grado di individuare il pubblico, contattare il rappresentante [!DNL Adobe] per assistenza.

È necessario fornire le seguenti informazioni al rappresentante [!DNL Adobe]:

* Nome del pubblico
* Nome destinazione
* Data di attivazione del pubblico
* Nome file esportato

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai attivato correttamente un pubblico sulla piattaforma di destinazione selezionata. Quindi, contatta il rappresentante della piattaforma di destinazione per iniziare a configurare la campagna.
