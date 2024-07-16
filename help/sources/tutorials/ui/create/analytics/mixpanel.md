---
title: Creare una connessione Source Mixpanel nell’interfaccia utente
description: Scopri come creare una connessione sorgente Mixpanel utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 11%

---

# Crea una connessione sorgente [!DNL Mixpanel] nell&#39;interfaccia utente

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL Mixpanel] tramite l&#39;interfaccia utente di Adobe Experience Platform Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per connettere [!DNL Mixpanel] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Nome utente | Il nome utente dell&#39;account del servizio che corrisponde all&#39;account [!DNL Mixpanel]. Per ulteriori informazioni, consulta la [[!DNL Mixpanel] documentazione degli account del servizio](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account). | `Test8.6d4ee7.mp-service-account` |
| Password | La password dell&#39;account del servizio che corrisponde all&#39;account [!DNL Mixpanel]. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID Progetto | ID progetto [!DNL Mixpanel]. Questo ID è necessario per creare una connessione sorgente. Per ulteriori informazioni, vedere la [[!DNL Mixpanel] documentazione delle impostazioni del progetto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) e la [[!DNL Mixpanel] guida alla creazione e alla gestione dei progetti](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects). | `2384945` |
| Fuso orario | Fuso orario corrispondente al progetto [!DNL Mixpanel]. Per creare una connessione di origine è necessario specificare il fuso orario. Per ulteriori informazioni, consulta la [documentazione sulle impostazioni del progetto Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings). | `Pacific Standard Time` |

Per ulteriori informazioni sull&#39;autenticazione dell&#39;origine [!DNL Mixpanel], vedere [[!DNL Mixpanel] panoramica origine](../../../../connectors/analytics/mixpanel.md).

## Connetti il tuo account [!DNL Mixpanel]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *Analytics*, selezionare [!DNL Mixpanel], quindi **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account Mixpanel]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Mixpanel] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Selezionare l’ID del progetto e il fuso orario {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Impostare un fuso orario per l’acquisizione da Mixpanel"
>abstract="Il fuso orario deve corrispondere a quello impostato nel tuo profilo Mixpanel, poiché Platform utilizza il fuso orario del progetto designato per acquisire i dati rilevanti da Mixpanel. Prima di registrare l’evento in un suo archivio dati, Mixpanel regolerà il proprio fuso orario in base a quello del tuo progetto."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=it#project-id-and-timezone" text="Ulteriori informazioni sono disponibili nella documentazione"

Una volta autenticata l&#39;origine, fornisci l&#39;ID progetto e il fuso orario, quindi seleziona **[!UICONTROL Seleziona]**.

Il fuso orario designato prima dell&#39;acquisizione dei dati [!DNL Mixpanel] in Platform deve essere uguale all&#39;impostazione del fuso orario del profilo [!DNL Mixpanel]. Eventuali modifiche al fuso orario dei dati verranno applicate solo ai nuovi eventi e i vecchi eventi rimarranno nel fuso orario precedentemente designato. [!DNL Mixpanel] è compatibile con l&#39;ora legale e regolerà in modo appropriato il timestamp di acquisizione. Per ulteriori informazioni sull&#39;effetto dei fusi orari sui dati, vedere la guida di [!DNL Mixpanel] alla gestione dei fusi orari per i progetti [.](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel)

Dopo alcuni istanti, l’interfaccia corretta viene aggiornata a un pannello di anteprima, che consente di esaminare lo schema prima di creare un flusso di dati. Al termine, selezionare **[!UICONTROL Avanti]**.

![configurazione](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Mixpanel]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati di analisi in Platform](../../dataflow/analytics.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui è possibile fare riferimento quando si utilizza l&#39;origine [!DNL Mixpanel].

### Convalida {#validation}

Di seguito vengono descritti i passaggi che è possibile eseguire per verificare che la connessione all&#39;origine [!DNL Mixpanel] sia stata completata e che gli eventi [!DNL Mixpanel] vengano acquisiti in Platform.

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Set di dati]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Set di dati]. Nella schermata [!UICONTROL Attività set di dati] vengono visualizzati i dettagli delle esecuzioni.

![attività-set di dati](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Quindi, seleziona l’ID di esecuzione del flusso di dati che desideri visualizzare per visualizzare dettagli specifici su tale esecuzione.

![monitoraggio dei flussi di dati](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Infine, seleziona **[!UICONTROL Anteprima set di dati]** per visualizzare i dati acquisiti.

![anteprima-set di dati](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

È possibile verificare questi dati rispetto ai dati nella pagina [!DNL Mixpanel] > [!DNL Events]. Per ulteriori informazioni, vedere il documento [[!DNL Mixpanel] sugli eventi](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-).

![eventi mixpanel](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Schema Mixpanel

Nella tabella seguente sono elencati i mapping supportati che devono essere impostati per [!DNL Mixpanel].

>[!TIP]
>
>Per ulteriori informazioni sull&#39;API, vedere [API esportazione eventi > Download](https://developer.mixpanel.com/reference/raw-event-export).


| Origine | Tipo |
|---|---|
| `distinct_id` | stringa |
| `event_name` | stringa |
| `import` | booleano |
| `insert_id` | stringa |
| `item_id` | stringa |
| `item_name` | stringa |
| `item_price` | stringa |
| `mp_api_endpoint` | stringa |
| `mp_api_timestamp_ms` | intero |
| `mp_processing_time_ms` | intero |
| `time` | intero |

### Limiti {#limits}

* Hai un massimo di 100 query simultanee e 60 query all&#39;ora, come indicato in [Esporta limiti di velocità API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
