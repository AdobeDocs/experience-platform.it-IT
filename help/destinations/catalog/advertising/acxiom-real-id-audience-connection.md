---
title: Acxiom Real ID&trade; Connessione pubblico
description: Utilizza la destinazione  [!DNL Acxiom Real ID&trade; Audience Connection]  per migliorare e attivare tipi di pubblico tra piattaforme quali  [!DNL Altice], [!DNL Ampersand] e [!DNL Comcast].
source-git-commit: 3aefb36bbf525a5eebe3a9330e25587501167a64
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 4%

---


# Destinazione [!DNL Acxiom Real ID™ Audience Connection]

Utilizza la destinazione [!DNL Acxiom Real ID Audience Connection] per migliorare i tipi di pubblico con la tecnologia [Real ID™](https://www.acxiom.com/real-id/real-id/) di [!DNL Acxiom]. Quindi attiva tali tipi di pubblico su piattaforme quali [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

>[!NOTE]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Acxiom]. Per richieste di informazioni o richieste di aggiornamento, contattare [!DNL Acxiom] direttamente all&#39;indirizzo [acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com).

Per creare un connettore di destinazione [!DNL Acxiom Real ID Audience Connection] tramite l&#39;interfaccia utente [!DNL Adobe Experience Platform], eseguire la procedura seguente. Utilizza questo connettore per generare e distribuire i tipi di pubblico alle destinazioni selezionate.

## Casi d’uso {#use-cases}

Utilizzare questa destinazione se [!DNL Real ID] di [!DNL Acxiom] è stato caricato in [!DNL Real-Time CDP] come identificatore. I seguenti casi d&#39;uso mostrano come utilizzare la destinazione [!DNL Acxiom Real ID Audience Connection].

### Invia tipi di pubblico da [!DNL Experience Platform] al tuo account [!DNL Acxiom] {#send-audiences}

Utilizza questo connettore di destinazione per inviare i tipi di pubblico da [!DNL Experience Platform] all&#39;account [!DNL Acxiom] per l&#39;acquisizione cross-channel.

Ad esempio, il reparto Marketing Operations di un brand di servizi finanziari globali è interessato all’acquisizione dei clienti cross-channel attraverso più piattaforme pubblicitarie. Possono utilizzare il connettore di destinazione [!DNL Acxiom Real ID Audience Connection] per inviare tipi di pubblico da [!DNL Experience Platform] a [!DNL Acxiom], migliorarli con la tecnologia [!DNL Real ID] di [!DNL Acxiom] e attivarli su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora.

## Prerequisiti {#prerequisites}

Prima di configurare la destinazione [!DNL Acxiom Real ID Audience Connection], completare i seguenti prerequisiti.

* **Conferma le condizioni d&#39;uso:** Leggi e firma il Contratto sulle condizioni d&#39;uso di [!DNL Acxiom]. Riceverai il collegamento al contratto una volta completato l&#39;ordine cliente eseguito. Fino alla firma del contratto, la scheda di destinazione [!DNL Acxiom Real ID Audience Connection] non viene visualizzata nel catalogo di destinazione [!DNL Experience Platform]. Dopo aver accettato e firmato il contratto, [!DNL Adobe] completa la configurazione e la scheda di destinazione [!DNL Acxiom Real ID Audience Connection] diventa visibile.
* **Conoscere l&#39;ID organizzazione [!DNL Adobe]:** L&#39;ID organizzazione [!DNL Adobe] è necessario per completare il Contratto sulle condizioni d&#39;uso. Consulta l&#39;*Organizzazioni in Experience Cloud* di [!DNL Adobe] per informazioni su come [visualizzare l&#39;ID organizzazione](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Ottenere una licenza per il prodotto [!DNL Real ID] di [!DNL Acxiom]:** Dopo aver ottenuto una licenza, rendere disponibili [!DNL Real ID] di [!DNL Acxiom] entro [!DNL Real-Time CDP]. Per ulteriori informazioni, vedere [Miglioramento dati Acxiom](/help/destinations/catalog/data-partner/acxiom-data-enhancement.md).

## Identità supportate {#supported-identities}

La destinazione [!DNL Real ID] di Connessione pubblico di [!DNL Acxiom] supporta le seguenti attivazioni di identità. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
| --------------- | ----------- | -------------- |
| [!DNL Real ID] | [!DNL Real ID] | Mappa un campo di origine a questa identità di destinazione. Il campo di origine può essere un [!DNL Acxiom] [!DNL Real ID] o un identificatore personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
| --------------- | --------- | ----------- |
| [!DNL Segmentation Service] | Sì | Tipi di pubblico generati tramite [!DNL Experience Platform] [Segmentation Service](/help/segmentation/home.md). |
| Tutte le altre origini del pubblico | Sì | Questa categoria include tutte le origini del pubblico al di fuori dei tipi di pubblico generati tramite [!DNL Segmentation Service]. Leggi informazioni sulle [diverse origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). Alcuni esempi includono: <ul><li>i tipi di pubblico per caricamento personalizzati [importati](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] da file CSV,</li><li>pubblico simile,</li><li>pubblico federato,</li><li>tipi di pubblico generati in altre app [!DNL Experience Platform] come [!DNL Adobe Journey Optimizer],</li><li>e altro ancora.</li></ul> |

{style="table-layout:auto"}

### Tipi di pubblico supportati per tipo di dati {#supported-audiences-data-type}

La tabella seguente descrive i tipi di dati sul pubblico che puoi esportare in questa destinazione.

| Tipo di dati del pubblico | Supportato | Descrizione | Casi d’uso |
| -------------------- | --------- | ----------- | --------- |
| [Tipi di pubblico per persone](/help/segmentation/types/people-audiences.md) | Sì | In base ai profili dei clienti. Utilizzali per targetizzare gruppi specifici di persone per campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](/help/segmentation/types/prospect-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti che non sono ancora clienti, ma che condividono alcune caratteristiche con il tuo pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](/help/catalog/datasets/overview.md) | No | Raccolte di dati strutturati archiviati nel Data Lake [!DNL Adobe Experience Platform]. | Reporting, flussi di lavoro di data science |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

La tabella seguente descrive il tipo e la frequenza di esportazione della destinazione.

| Elemento | Tipo | Note |
| ---- | ---- | ----- |
| Tipo di esportazione | **[!UICONTROL Audience export]** | Esporta tutti i membri di un pubblico con gli identificatori utilizzati nella destinazione [!DNL Acxiom Real ID Audience Connection]. |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Destinazioni supportati {#supported-destinations}

Attiva i tipi di pubblico nelle seguenti piattaforme tramite la destinazione [!DNL Acxiom Real ID Audience Connection].

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## Connettersi alla destinazione {#connect}

[!DNL Experience Platform] gestisce automaticamente l&#39;autenticazione per la destinazione [!DNL Acxiom Real ID Audience Connection].

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Impostazioni specifiche per la destinazione {#destination-settings}

Alcune destinazioni di [!DNL Acxiom Real ID Audience Connection] richiedono ulteriori informazioni. Le sezioni seguenti forniscono indicazioni dettagliate su come configurare queste opzioni.

### [!DNL Amazon] {#amazon}

Per configurare i dettagli per la destinazione, completa i campi seguenti.

* **[!UICONTROL Publisher Account ID]**: immettere l&#39;ID account editore associato a questa destinazione.

  ![Schermata del pannello dei dettagli della destinazione [!DNL Amazon] che mostra il campo ID account di pubblicazione.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Per configurare i dettagli per la destinazione, completa i campi seguenti.

* **[!UICONTROL Destination Account ID]**: immettere l&#39;ID account di destinazione per questa destinazione.

  ![Schermata del pannello dei dettagli della destinazione [!DNL Facebook] che mostra il campo ID account di destinazione.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Per configurare i dettagli per la destinazione, completa i campi seguenti.

* **[!UICONTROL Segment Category]**: la categoria di destinazione o verticale in cui rientra il segmento. Esempio: servizi finanziari, settore automobilistico o sanità.

  ![Schermata del pannello dei dettagli della destinazione [!DNL LG Ads] che mostra il campo Categoria segmento.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Per configurare i dettagli per la destinazione, completa i campi seguenti.

* **[!UICONTROL Destination Account ID]**: immettere l&#39;ID account di destinazione per questa destinazione.

  ![Schermata del pannello dei dettagli della destinazione [!DNL Pinterest] che mostra il campo ID account di destinazione.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Per configurare i dettagli per la destinazione, completa i campi seguenti.

* **[!UICONTROL Advertiser Name]**: immettere il nome dell&#39;inserzionista per questa destinazione.

  ![Schermata del pannello dei dettagli della destinazione [!DNL Vizio] che mostra il campo Nome inserzionista.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_vizio_destination_details.png){zoomable="yes"}

## Attivare tipi di pubblico in questa destinazione {#activate}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

>[!IMPORTANT]
>
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>La destinazione [!DNL Acxiom Real ID Audience Connection] supporta solo esportazioni di file complete.

### Mappare attributi e identità {#map}

Affinché la destinazione [!DNL Acxiom Real ID Audience Connection] riceva correttamente i dati sul pubblico, mappare il campo di origine da [!DNL Experience Platform] al campo di destinazione [!DNL Acxiom Real ID Audience Connection] corretto.

Il campo di destinazione **[!UICONTROL Real ID]** viene precompilato automaticamente nel passaggio di mappatura. Mappa il campo di origine su di esso: uno spazio dei nomi dell&#39;identificatore personalizzato o un [!DNL Acxiom] [!DNL Real ID] effettivo memorizzato nello schema del profilo.

| Nome campo | Descrizione | Obbligatorio |
| ---------- | ----------- | -------- |
| [!DNL Real ID] | [!DNL Real ID] è un identificatore alfanumerico univoco a 36 byte del grafico di risoluzione delle identità proprietario di [!DNL Acxiom]. È un identificatore che rappresenta una persona, una famiglia o un indirizzo. | Sì |

{style="table-layout:auto"}

Nella colonna **[!UICONTROL Source Field]** immettere il nome dell&#39;attributo di origine che si desidera mappare al campo di destinazione **[!UICONTROL Real ID]**. In alternativa, selezionare **[!UICONTROL Select source field]** per sfogliare i campi di origine disponibili. Quindi selezionare **[!UICONTROL Next]**.

![Schermata della schermata di mappatura che mostra la colonna [!UICONTROL Source Field] e il pannello [!UICONTROL Select source field].](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png){zoomable="yes"}

Se non utilizzi lo schema standard di [!DNL Adobe], consulta la [guida dell&#39;interfaccia utente di Query Service](/help/query-service/ui/overview.md) per popolare lo schema standard [!DNL Adobe] con i tuoi nomi di campo.

### Verifica la destinazione {#review}

Dopo aver completato tutti i passaggi, controlla lo stato della connessione di destinazione e i dettagli del pubblico prima di attivarla. Il pubblico selezionato viene visualizzato in un elenco. Ogni pubblico è una chiamata separata all&#39;API [!DNL Acxiom Real ID Audience Connection].

Quando i risultati sono corretti, selezionare **[!UICONTROL Finish]** per attivare la destinazione.

![Schermata della schermata Review che mostra lo stato della connessione di destinazione e i tipi di pubblico selezionati prima dell&#39;attivazione.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png){zoomable="yes"}

## Risoluzione dei problemi {#troubleshooting}

Se il rappresentante di destinazione non è in grado di individuare il pubblico, contattare il rappresentante [!DNL Adobe] per assistenza.

Fornisci le seguenti informazioni al tuo rappresentante [!DNL Adobe]:

* Nome del pubblico
* Nome destinazione
* Data di attivazione del pubblico
* Nome file esportato

## Passaggi successivi {#next-steps}

Un pubblico è stato attivato correttamente sulla piattaforma di destinazione selezionata. Quindi, contatta il rappresentante della piattaforma di destinazione per iniziare a configurare la campagna.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
