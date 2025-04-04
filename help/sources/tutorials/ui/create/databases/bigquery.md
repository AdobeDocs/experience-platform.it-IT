---
title: Connetti [!DNL Google BigQuery] Ad Experience Platform Utilizzando L'Interfaccia Utente
description: Scopri come creare una connessione sorgente Google Big Query utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Connetti [!DNL Google BigQuery] ad Experience Platform tramite l&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Google BigQuery] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggi questo tutorial per scoprire come collegare il tuo account [!DNL Google BigQuery] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Google BigQuery] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Leggi la [[!DNL Google BigQuery] guida all&#39;autenticazione](../../../../connectors/databases/bigquery.md#prerequisites) per i passaggi dettagliati sulla raccolta delle credenziali richieste.

## Navigare nel catalogo delle origini {#navigate}

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. È possibile selezionare la categoria appropriata nel pannello *[!UICONTROL Categorie]* In alternativa, è possibile utilizzare la barra di ricerca per passare all&#39;origine specifica che si desidera utilizzare.

Per utilizzare [!DNL Google BigQuery], selezionare la scheda di origine **[!UICONTROL Google BigQuery]** in *[!UICONTROL Database]*, quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con BigQuery Google selezionato.](../../../../images/tutorials/create/google-big-query/catalog.png)

## Usa un account esistente {#existing}

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Google BigQuery] con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Pagina dell&#39;account esistente in cui viene presentato un elenco di account esistenti.](../../../../images/tutorials/create/google-big-query/existing.png)

## Crea un nuovo account {#create}

Se non disponi di un account esistente, devi crearne uno nuovo fornendo le credenziali di autenticazione necessarie che corrispondono all’origine.

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account.

![Nuova interfaccia account nel flusso di lavoro di origine.](../../../../images/tutorials/create/google-big-query/new.png)

### Connettersi ad Experience Platform in Azure {#azure}

È possibile connettere l&#39;account [!DNL Google BigQuery] ad Experience Platform su Azure utilizzando l&#39;autenticazione di base o di servizio.

>[!BEGINTABS]

>[!TAB Usa autenticazione di base]

Per utilizzare l&#39;autenticazione di base, seleziona **[!UICONTROL Autenticazione di base]** e fornisci i valori per il tuo [progetto, ID client, segreto client, token di aggiornamento e ID (facoltativo) set di dati con risultati di grandi dimensioni](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Nuova interfaccia account in cui è selezionata l&#39;autenticazione di base.](../../../../images/tutorials/create/google-big-query/basic-auth.png)

>[!TAB Usa autenticazione servizio]

Per utilizzare l&#39;autenticazione del servizio, selezionare **[!UICONTROL Autenticazione del servizio]** e fornire i valori per l&#39;ID del [progetto, il contenuto del file di chiave e l&#39;ID del set di dati di grandi risultati (facoltativo)](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Nuova interfaccia account in cui è selezionata l&#39;autenticazione del servizio.](../../../../images/tutorials/create/google-big-query/service-auth.png)

>[!ENDTABS]

### Connettersi ad Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per creare un nuovo account [!DNL Google BigQuery] e connettersi ad Experience Platform su AWS, verificare di essere in una sandbox VA6 e quindi fornire le credenziali necessarie per l&#39;autenticazione.

* **ID progetto**: l&#39;ID progetto corrispondente al tuo account [!DNL Google BigQuery].
* **Contenuto file chiave**: file chiave utilizzato per autenticare l&#39;account del servizio. Puoi recuperare questo valore dal [[!DNL Google Cloud service accounts] dashboard](https://console.cloud.google.com). Il contenuto del file chiave è in formato JSON. È necessario codificarlo in [!DNL Base64] durante l&#39;autenticazione in Experience Platform.
* **ID set di dati**: ID del set di dati [!DNL Google BigQuery]. Questo ID rappresenta dove si trovano le tabelle di dati e deve essere creato anticipatamente per abilitare il supporto per set di risultati di grandi dimensioni.

![Nuova interfaccia account per una connessione AWS.](../../../../images/tutorials/create/google-big-query/aws.png)

## Ignora anteprima dei dati di esempio {#skip-preview-of-sample-data}

Durante il passaggio di selezione dei dati, potrebbe verificarsi un timeout durante l’acquisizione di tabelle o file di dati di grandi dimensioni. Puoi saltare l’anteprima dei dati per evitare il timeout e visualizzare comunque lo schema, anche senza dati di esempio. Per ignorare l&#39;anteprima dei dati, abilitare l&#39;interruttore **[!UICONTROL Ignora anteprima dati di esempio]**.

Il resto del flusso di lavoro rimarrà invariato. L’unica avvertenza è che ignorare l’anteprima dei dati potrebbe impedire la convalida automatica dei campi calcolati e obbligatori durante il passaggio di mappatura, per cui dovrai convalidarli manualmente durante la mappatura.

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Google BigQuery]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Experience Platform](../../dataflow/databases.md).
