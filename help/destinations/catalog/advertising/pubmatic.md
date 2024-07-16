---
title: Connessione PubMatic
description: PubMatic massimizza il valore del cliente offrendo la catena di fornitura del futuro del marketing digitale programmatico. PubMatic Connect combina tecnologia di piattaforma e servizio dedicato per migliorare il modo in cui l’inventario e i dati vengono assemblati e scambiati.
last-substantial-update: 2023-12-14T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 2%

---

# Destinazione PubMatic Connect {#pubmatic-connect}

## Panoramica {#overview}

Utilizza [!DNL PubMatic Connect] per massimizzare il valore del cliente distribuendo la catena di fornitura del marketing digitale programmatico del futuro. [!DNL PubMatic Connect] combina tecnologia Platform e servizio dedicato per migliorare il modo in cui l&#39;inventario e i dati vengono assemblati e scambiati.

Utilizzare questa destinazione per inviare i dati del pubblico alla piattaforma [!DNL PubMatic Connect].

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL PubMatic]. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo `support@pubmatic.com`.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL PubMatic Connect], ecco un esempio di caso d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Targeting degli utenti su piattaforme mobili, web e CTV {#targeting}

Gli editori o i provider di dati desiderano inviare tipi di pubblico da Adobe Experience Platform a [!DNL PubMatic Connect] per il targeting degli utenti su piattaforme mobili, web e CTV, utilizzando un&#39;ampia gamma di identificatori.

## Prerequisiti {#prerequisites}

Rivolgiti al tuo Account Manager [!DNL PubMatic] per assicurarti che il tuo account sia configurato correttamente e supporti l&#39;onboarding dei segmenti di pubblico. Inoltre, si assicureranno che tu disponga di tutti i dettagli rilevanti per utilizzare questa destinazione e per fornirti supporto durante la configurazione.

## Identità supportate {#supported-identities}

[!DNL PubMatic Connect] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
| --------------- | ------ | --- |
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
| --- | --- | --- |
| Tipo di esportazione | **[!UICONTROL Esportazione segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione PubMatic Connect. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
> Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestione destinazioni]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

![Autenticazione](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Token Bearer]**: compila il token Bearer per l&#39;autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli destinazione](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
- **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
- **[!UICONTROL ID partner dati]**: l&#39;ID partner dati configurato nell&#39;account [!DNL PubMatic] per questa integrazione.
- **[!UICONTROL Codice paese predefinito]**: il codice paese predefinito che deve essere applicato a tutte le identità se nel profilo non ne viene fornita alcuna.
- **[!UICONTROL ID account]**: ID account [!DNL PubMatic Connect].
- **[!UICONTROL Tipo di account]**: il tipo di account dell&#39;account della piattaforma [!DNL PubMatic]. In caso di domande su cui scegliere, rivolgiti al tuo account manager [!DNL PubMatic]. Le opzioni disponibili sono:
   - [!UICONTROL EDITORE]
   - [!UICONTROL PARTNER_DOMANDA]
   - [!UICONTROL ACQUIRENTE]

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
> - Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>
> - Per esportare _identità_, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](../../assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Selezione dei campi di origine:

- Seleziona un identificatore (in genere spazi dei nomi come IDFA o uno spazio dei nomi ID personalizzato).

Selezione dei campi di destinazione:

- Rivolgiti al tuo Account Manager [!DNL PubMatic] per ottenere le informazioni sul tipo di UID corretto durante questo passaggio.
- Selezionare il numero del tipo [!DNL PubMatic UID] che corrisponde all&#39;identificatore selezionato nel primo passaggio.

![Mappa attributi e identità](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

L&#39;interfaccia utente di [!DNL PubMatic] consente di verificare se i dati sono stati inviati correttamente e se i segmenti sono disponibili. L&#39;aggiornamento dell&#39;interfaccia utente [!DNL PubMatic] può richiedere fino a 24 ore dopo il push dei dati.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
