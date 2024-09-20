---
title: Creare una connessione Source Google Big Query nell’interfaccia utente
description: Scopri come creare una connessione sorgente Google Big Query utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 55aaaa39659566de81bb161d704b6f8212e29a8b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Crea una connessione sorgente [!DNL Google BigQuery] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Google BigQuery] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Leggi questo tutorial per scoprire come collegare il tuo account [!DNL Google BigQuery] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Google BigQuery] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Leggi la [[!DNL Google BigQuery] guida all&#39;autenticazione](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) per i passaggi dettagliati sulla raccolta delle credenziali richieste.

## Connetti il tuo account Google BigQuery

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Database], selezionare **[!UICONTROL Google BigQuery]**, quindi **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con BigQuery Google selezionato.](../../../../images/tutorials/create/google-big-query/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Google Big Query]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Google BigQuery] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![Pagina dell&#39;account esistente in cui viene presentato un elenco di account esistenti.](../../../../images/tutorials/create/google-big-query/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il nuovo account [!DNL Google BigQuery].

![Nuova interfaccia account nel flusso di lavoro di origine.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB Usa autenticazione di base]

Per utilizzare l&#39;autenticazione di base, seleziona **[!UICONTROL Autenticazione di base]** e fornisci i valori per il tuo [progetto, ID client, segreto client, token di aggiornamento e ID (facoltativo) set di dati con risultati di grandi dimensioni](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Nuova interfaccia account in cui è selezionata l&#39;autenticazione di base.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB Usa autenticazione servizio]

Per utilizzare l&#39;autenticazione del servizio, selezionare **[!UICONTROL Autenticazione del servizio]** e fornire i valori per l&#39;ID del [progetto, il contenuto del file di chiave e l&#39;ID del set di dati di grandi risultati (facoltativo)](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Nuova interfaccia account in cui è selezionata l&#39;autenticazione del servizio.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Google BigQuery]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/databases.md).
