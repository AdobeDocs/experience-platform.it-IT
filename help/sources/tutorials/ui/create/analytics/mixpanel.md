---
title: Creare una connessione sorgente Mixpanel nell’interfaccia utente
description: Scopri come creare una connessione sorgente Mixpanel utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 11%

---

# Creare un [!DNL Mixpanel] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Mixpanel] connessione di origine tramite l’interfaccia utente di Adobe Experience Platform Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per connettersi [!DNL Mixpanel] In Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Nome utente | Il nome utente dell’account di servizio che corrisponde al [!DNL Mixpanel] account. Consulta la [[!DNL Mixpanel] documentazione degli account di servizio](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) per ulteriori informazioni. | `Test8.6d4ee7.mp-service-account` |
| Password | La password dell&#39;account di servizio che corrisponde al [!DNL Mixpanel] account. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID Progetto | Il tuo [!DNL Mixpanel] ID progetto. Questo ID è necessario per creare una connessione sorgente. Consulta la [[!DNL Mixpanel] documentazione sulle impostazioni del progetto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) e [[!DNL Mixpanel] guida alla creazione e alla gestione dei progetti](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) per ulteriori informazioni. | `2384945` |
| Fuso orario | Fuso orario corrispondente al [!DNL Mixpanel] progetto. Per creare una connessione di origine è necessario specificare il fuso orario. Consulta la [Documentazione sulle impostazioni dei progetti Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) per ulteriori informazioni. | `Pacific Standard Time` |

Per ulteriori informazioni sull’autenticazione di [!DNL Mixpanel] sorgente, consulta [[!DNL Mixpanel] panoramica dell’origine](../../../../connectors/analytics/mixpanel.md).

## Connetti [!DNL Mixpanel] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *Analytics* categoria, seleziona [!DNL Mixpanel], quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Il **[!UICONTROL Connetti account Mixpanel]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Mixpanel] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Seleziona l’ID del progetto e il fuso orario {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Impostare un fuso orario per l’acquisizione da Mixpanel"
>abstract="Il fuso orario deve corrispondere a quello impostato nel tuo profilo Mixpanel, poiché Platform utilizza il fuso orario del progetto designato per acquisire i dati rilevanti da Mixpanel. Prima di registrare l’evento in un suo archivio dati, Mixpanel regolerà il proprio fuso orario in base a quello del tuo progetto."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=it#project-id-and-timezone" text="Ulteriori informazioni sono disponibili nella documentazione"

Una volta autenticata l’origine, fornisci l’ID progetto e il fuso orario, quindi seleziona **[!UICONTROL Seleziona]**.

Il fuso orario designato prima dell’acquisizione del [!DNL Mixpanel] i dati da a Platform devono essere uguali ai [!DNL Mixpanel] impostazione del fuso orario del profilo. Eventuali modifiche al fuso orario dei dati verranno applicate solo ai nuovi eventi e i vecchi eventi rimarranno nel fuso orario precedentemente designato. [!DNL Mixpanel] consente di usare l’ora legale e di regolare in modo appropriato la marca temporale di acquisizione. Per ulteriori informazioni sull’effetto dei fusi orari sui dati, consulta [!DNL Mixpanel] guida su [gestione dei fusi orari dei progetti](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Dopo alcuni istanti, l’interfaccia corretta viene aggiornata a un pannello di anteprima, che consente di esaminare lo schema prima di creare un flusso di dati. Al termine, seleziona **[!UICONTROL Successivo]**.

![configurazione](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Mixpanel] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di analytics in Platform](../../dataflow/analytics.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL Mixpanel] sorgente.

### Convalida {#validation}

Di seguito sono riportati i passaggi che è possibile eseguire per verificare che la connessione sia stata eseguita correttamente [!DNL Mixpanel] sorgente e che [!DNL Mixpanel] Gli eventi vengono acquisiti in Platform.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Set di dati]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Set di dati] Workspace. Il [!UICONTROL Attività set di dati] mostra i dettagli delle esecuzioni.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Quindi, seleziona l’ID di esecuzione del flusso di dati che desideri visualizzare per visualizzare dettagli specifici su tale esecuzione.

![monitoraggio dei flussi di dati](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Infine, seleziona **[!UICONTROL Anteprima set di dati]** per visualizzare i dati acquisiti.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Puoi verificare questi dati in base ai dati presenti sul [!DNL Mixpanel] > [!DNL Events] pagina. Consulta la [[!DNL Mixpanel] documento sugli eventi](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) per ulteriori informazioni.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Schema Mixpanel

La tabella seguente elenca le mappature supportate che devono essere impostate per [!DNL Mixpanel].

>[!TIP]
>
>Consulta [API esportazione evento > Scarica](https://developer.mixpanel.com/reference/raw-event-export) per ulteriori informazioni sull’API.


| Origine | Tipo |
|---|---|
| `distinct_id` | string |
| `event_name` | string |
| `import` | booleano |
| `insert_id` | string |
| `item_id` | string |
| `item_name` | string |
| `item_price` | string |
| `mp_api_endpoint` | string |
| `mp_api_timestamp_ms` | numero intero |
| `mp_processing_time_ms` | numero intero |
| `time` | numero intero |

### Limiti {#limits}

* Hai un massimo di 100 query simultanee e 60 query all’ora come indicato in [Esporta limiti di velocità API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
