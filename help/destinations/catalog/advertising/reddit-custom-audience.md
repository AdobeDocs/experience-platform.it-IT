---
title: Modifica pubblico personalizzato
description: Reddit Ads collega i brand a persone che stanno attivamente esplorando le loro passioni e i loro problemi in tempo reale. Abbinando conversazioni ad alto intento guidate dalla community con formati di annunci flessibili e un targeting robusto, gli annunci Reddit Ads aiutano gli inserzionisti a raggiungere il pubblico coinvolto, promuovere i risultati delle prestazioni e imparare direttamente dalle comunità che modellano la cultura online. Questa guida è destinata agli inserzionisti e ai team di media che utilizzano Adobe Experience Platform per inviare tipi di pubblico a Reddit Ads. Descrive ciò di cui hai bisogno per collegare i tuoi account, mappare le identità e attivare i tipi di pubblico.
last-substantial-update: 2026-03-31T00:00:00Z
exl-id: bcce02bd-d508-47a0-8f5c-bf162db1859d
badgeBeta: label="Beta" type="Informative"
source-git-commit: 28bbad7ccbec0b669082658b912d0b52e0374667
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 3%

---

# Connessione [!DNL Reddit Custom Audience] {#reddit-custom-audience-connection}

## Panoramica {#overview}

[!DNL Reddit Ads] collega i brand a persone che stanno esplorando attivamente le loro passioni e i loro problemi in tempo reale. Associando conversazioni ad alto intento e basate sulla community a formati di annunci flessibili e a un targeting affidabile, [!DNL Reddit Ads] aiuta gli inserzionisti a raggiungere un pubblico coinvolto, ottenere risultati in termini di prestazioni e imparare direttamente dalle comunità che modellano la cultura online.

Questa guida è destinata agli inserzionisti e ai team di media che utilizzano [!DNL Adobe Experience Platform] per inviare tipi di pubblico a [!DNL Reddit Ads]. Descrive ciò di cui hai bisogno per collegare i tuoi account, mappare le identità e attivare i tipi di pubblico.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Reddit]. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo <adsapi-partner-support@reddit.com>.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Reddit Custom Audience], ecco alcuni esempi di casi d&#39;uso che i clienti [!DNL Adobe Experience Platform] possono risolvere utilizzando questa destinazione.

### Retargeting di clienti esistenti con offerte personalizzate {#use-case-1}

Un retailer online vuole raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate basate sui loro ordini precedenti. Il retailer online può acquisire gli indirizzi e-mail e gli ID dispositivo (IDFA e GAID) dal proprio CRM a [!DNL Adobe Experience Platform], creare tipi di pubblico dai propri dati offline e inviarli a [!DNL Reddit Ads], ottimizzando le spese pubblicitarie.

## Prerequisiti {#prerequisites}

Prima di configurare questa destinazione, accertati di soddisfare i seguenti prerequisiti:

* Un account [!DNL Reddit Ads] che può utilizzare tipi di pubblico ed elenchi di clienti personalizzati.
* Autorizzazione per autorizzare la connessione. Questo deve essere un utente che può accedere a [!DNL Reddit] e approvare l&#39;accesso per [!DNL Experience Platform] per gestire i tipi di pubblico per conto dell&#39;account dell&#39;annuncio.
* ID dell&#39;account dell&#39;annuncio [!DNL Reddit]: l&#39;identificatore dell&#39;account dell&#39;annuncio in cui vengono creati i tipi di pubblico. Puoi trovare il tuo ID account dell&#39;annuncio in [Account](https://ads.reddit.com/accounts). Ad esempio: `a2_1b2c34d`.

## Identità supportate {#supported-identities}

[!DNL Reddit Custom Audience] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
| --- | --- | --- |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e testo normale sono supportati da [!DNL Adobe Experience Platform]. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** in modo che [!DNL Platform] esegua automaticamente l&#39;hash dei dati all&#39;attivazione. |
| cameriera | Google Advertising ID o Apple ID per inserzionisti, entrambi con hash con l’algoritmo SHA256 | Mappa GAID o IDFA su **maid**. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** in modo che [!DNL Platform] esegua automaticamente l&#39;hash dei dati all&#39;attivazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
| --- | --- | --- |
| [!DNL Segmentation Service] | Sì | Tipi di pubblico generati tramite [!DNL Experience Platform] [Segmentation Service](../../../segmentation/home.md). |
| Tutte le altre origini del pubblico | Sì | Questa categoria include tutte le origini del pubblico al di fuori dei tipi di pubblico generati tramite il servizio di segmentazione. Leggi informazioni sulle [diverse origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). |

{style="table-layout:auto"}

Pubblico supportato per tipo di dati:

| Tipo di dati del pubblico | Supportato | Descrizione | Casi d’uso |
| --- | --- | --- | --- |
| [Tipi di pubblico per persone](/help/segmentation/types/people-audiences.md) | Sì | In base ai profili dei clienti, consente di eseguire il targeting di gruppi specifici di persone per campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](/help/segmentation/types/prospect-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti che non sono ancora clienti, ma che condividono alcune caratteristiche con il tuo pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](/help/catalog/datasets/overview.md) | No | Raccolte di dati strutturati archiviati nel Data Lake [!DNL Adobe Experience Platform]. | Reporting, flussi di lavoro di data science |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
| --- | --- | --- |
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione [!DNL Reddit Custom Audience]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**.

![Nella schermata di autenticazione della destinazione Pubblico personalizzato Reddit sono visualizzati i campi necessari per la connessione.](../../assets/catalog/advertising/redditcustomaudience/configure_new_destination_fields.png)

Sei stato reindirizzato per accedere con [!DNL Reddit]. Dopo aver esaminato le autorizzazioni richieste, seleziona **[!UICONTROL Allow]** in modo che [!DNL Experience Platform] possa creare tipi di pubblico e aggiornare l&#39;iscrizione per conto del tuo account annuncio.

![Schermata delle autorizzazioni Reddit OAuth.](../../assets/catalog/advertising/redditcustomaudience/reddit_oauth.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dei dettagli della destinazione del pubblico personalizzato Reddit.](../../assets/catalog/advertising/redditcustomaudience/reddit_account_details.png)

* **[!UICONTROL Name]**: nome utilizzato per riconoscere la destinazione.
* **[!UICONTROL Description]**: descrizione che consente di identificare questa destinazione.
* **[!UICONTROL Ad Account ID]**: ID del tuo account annuncio [!DNL Reddit].

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

I seguenti spazi dei nomi delle identità di destinazione devono essere mappati a seconda del caso d’uso:

| Campo origine | Campo di destinazione | Note |
| --- | --- | --- |
| E-mail (testo normale o con hash) | email_lc_sha256 | È possibile eseguire l&#39;hashing o l&#39;unhashing del campo di origine. [!DNL Reddit] accetta solo valori con hash. Abilita **[!UICONTROL Apply transformation]** in modo che [!DNL Experience Platform] esegua l&#39;hash dell&#39;e-mail prima dell&#39;invio. |
| MAID (testo normale o con hash) | cameriera | È possibile eseguire l&#39;hashing o l&#39;unhashing del campo di origine. [!DNL Reddit] accetta solo valori con hash. Abilita **[!UICONTROL Apply transformation]** in modo che [!DNL Experience Platform] esegua l&#39;hash del valore prima dell&#39;invio. |

Devi mappare almeno una delle identità.

![La schermata di mappatura identità mostra i campi di origine e di destinazione configurati per Reddit Custom Audience.](../../assets/catalog/advertising/redditcustomaudience/mapping.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver attivato i tipi di pubblico, puoi visualizzarli nell&#39;account [!DNL Reddit] Ads Manager.

I tipi di pubblico appena creati in [!DNL Reddit] vengono visualizzati in uno stato in sospeso. Una volta eseguito il flusso di dati e esportati i profili, [!DNL Reddit] corrisponde ai profili rispetto a [!DNL Reddit] utenti. Una volta elaborati i dati, lo stato del pubblico cambia in **[!UICONTROL Valid]**. La dimensione del pubblico deve raggiungere [1.000 utenti o più](https://ads-api.reddit.com/docs/v3/manage-customer-lists) per essere considerata valida. I tipi di pubblico che non soddisfano le dimensioni richieste vengono visualizzati come **[!UICONTROL Invalid]**.

![Il gestore di Reddit Ads mostra un pubblico esportato e il relativo stato.](../../assets/catalog/advertising/redditcustomaudience/see_audience_in_reddit.png)

Di seguito è riportato un esempio del payload inviato a [!DNL Reddit]:

```json
{
  "data": {
    "action_type": "ADD",
    "column_order": [
      "EMAIL_SHA256",
      "MAID_SHA256"
    ],
    "user_data": [
      [
        "d7ef2e7b2a3663c25284a3d6d13b1ca727fc8c659474b81afe0cec997a4737d2",
        "510870d7b3e47a28a2b2f3aef27a4c81aab0b2eefda27dea50bc4c991d9e5435"
      ]
    ]
  }
}
```

Per ulteriori informazioni, consulta la [documentazione dell&#39;API Reddit](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users).

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Consulta la [documentazione dell&#39;API Reddit](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) per informazioni dettagliate sul funzionamento dell&#39;endpoint dei tipi di pubblico personalizzati.
