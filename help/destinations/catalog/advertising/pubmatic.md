---
title: Connessione PubMatic
description: PubMatic massimizza il valore del cliente offrendo la catena di fornitura del futuro del marketing digitale programmatico. PubMatic Connect combina tecnologia di piattaforma e servizio dedicato per migliorare il modo in cui l’inventario e i dati vengono assemblati e scambiati.
last-substantial-update: 2023-12-14T00:00:00Z
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---


# Destinazione PubMatic Connect {#pubmatic-connect}

## Panoramica {#overview}

Utilizzare [!DNL PubMatic Connect] massimizzare il valore per il cliente offrendo la supply chain di marketing digitale programmatico del futuro. [!DNL PubMatic Connect] combina tecnologia Platform e servizio dedicato per migliorare il modo in cui inventario e dati vengono assemblati e scambiati.

Utilizza questa destinazione per inviare i dati del pubblico a [!DNL PubMatic Connect] piattaforma.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da [!DNL PubMatic] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattale direttamente all’indirizzo `support@pubmatic.com`.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL PubMatic Connect] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Targeting degli utenti su piattaforme mobili, web e CTV {#targeting}

Gli editori o i fornitori di dati desiderano inviare tipi di pubblico da Adobe Experience Platform a [!DNL PubMatic Connect] per eseguire il targeting degli utenti su piattaforme mobili, web e CTV, utilizzando un’ampia gamma di identificatori.

## Prerequisiti {#prerequisites}

Parla con il tuo [!DNL PubMatic] Account Manager per assicurarti che il tuo account sia configurato correttamente e supporti l’onboarding dei segmenti di pubblico. Inoltre, si assicureranno che tu disponga di tutti i dettagli rilevanti per utilizzare questa destinazione e per fornirti supporto durante la configurazione.

## Identità supportate {#supported-identities}

[!DNL PubMatic Connect] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
| --------------- | ------ | --- |
| GAID | Google Advertising ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
| --- | --- | --- |
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione PubMatic Connect. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experienci Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
> Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Come eseguire l’autenticazione](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Token Bearer]**: inserisci il token Bearer per l’autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli della destinazione](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
- **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
- **[!UICONTROL ID partner dati]**: l’ID del partner dati configurato nel [!DNL PubMatic] per questa integrazione.
- **[!UICONTROL Codice paese predefinito]**: codice paese predefinito da applicare a tutte le identità, se nel profilo non ne è fornita alcuna.
- **[!UICONTROL ID account]**: il tuo [!DNL PubMatic Connect] ID account.
- **[!UICONTROL Tipo di account]**: il tipo di account del [!DNL PubMatic] account della piattaforma. Parla con il tuo [!DNL PubMatic] account manager in caso di domande su cui scegliere. Opzioni disponibili:
   - [!UICONTROL EDITORE]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL ACQUIRENTE]

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
> - Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>
> - Per esportare _identità_, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](../../assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Selezione dei campi di origine:

- Seleziona un identificatore (in genere spazi dei nomi come IDFA o uno spazio dei nomi ID personalizzato).

Selezione dei campi di destinazione:

- Parla con il tuo [!DNL PubMatic] Account Manager per ottenere le informazioni sul tipo di UID corretto durante questo passaggio.
- Seleziona la [!DNL PubMatic UID] digita il numero che corrisponde all’identificatore selezionato nel primo passaggio.

![Mappare attributi e identità](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Il [!DNL PubMatic] L’interfaccia utente consente di verificare se i dati sono stati inviati correttamente e se i segmenti sono disponibili. Possono essere necessarie fino a 24 ore dopo il push dei dati per [!DNL PubMatic] Interfaccia utente da aggiornare.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
