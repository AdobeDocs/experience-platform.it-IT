---
title: Creare una connessione Pendo Source nell’interfaccia utente
description: Scopri come creare una connessione sorgente Pendo utilizzando l’interfaccia utente di Adobe Experience Platform.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# Crea un flusso di dati della connessione di origine [!DNL Pendo] e nell&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL Pendo] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../../../home.md#terms-and-conditions).

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL Pendo] e di un flusso di dati tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Prerequisiti {#prerequisites}

Nella sezione seguente vengono fornite informazioni sui prerequisiti da completare prima di creare una connessione di origine [!DNL Pendo].

### JSON di esempio per definire lo schema di origine per [!DNL Pendo] {#prerequisites-json-schema}

Prima di creare una connessione di origine [!DNL Pendo], è necessario specificare uno schema di origine. Puoi utilizzare il codice JSON qui sotto.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Per ulteriori informazioni, leggere la [[!DNL Pendo] guida sui webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Crea uno schema di Platform per [!DNL Pendo] {#create-platform-schema}

Devi anche assicurarti di creare prima uno schema Platform da utilizzare per la tua origine. Consulta il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per i passaggi completi sulla creazione di uno schema.

![Interfaccia utente di Platform che mostra uno schema di esempio per Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Connetti il tuo account [!DNL Pendo] {#connect-account}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini] e visualizzare un catalogo delle origini disponibili in Experience Platform.

Utilizza il menu *[!UICONTROL Categorie]* per filtrare le origini per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai alla categoria [!UICONTROL Analytics] per visualizzare la scheda di origine [!DNL Pendo]. Per iniziare, selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo di origine dell&#39;interfaccia utente di Platform con la scheda Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Selezionare i dati {#select-data}

Viene visualizzato il passaggio **[!UICONTROL Seleziona dati]**, che fornisce un&#39;interfaccia per la selezione dei dati da inserire in Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nel pannello [!UICONTROL Trascina i file].

![Passaggio Aggiungi dati del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare l&#39;utilità [!UICONTROL Cerca campo] per accedere a elementi specifici dallo schema.

Al termine, selezionare **[!UICONTROL Avanti]**.

![Passaggio di anteprima del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Dettaglio del flusso di dati {#dataflow-detail}

Viene visualizzato il passaggio **Dettagli flusso di dati** che fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l&#39;opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, selezionare **[!UICONTROL Avanti]**.

![Passaggio del flusso di dati dei dettagli del flusso di lavoro delle origini.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mappatura {#mapping}

Viene visualizzato il passaggio [!UICONTROL Mappatura] che fornisce un&#39;interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

Le mappature elencate di seguito sono obbligatorie e devono essere configurate prima di procedere alla fase [!UICONTROL Revisione].

| Campo di destinazione | Descrizione |
| --- | --- |
| `uniqueId` | Identificatore [!DNL Pendo] dell&#39;evento. |

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Avanti]**.

![Passaggio di mappatura del flusso di lavoro di origine.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Controlla {#review}

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa i campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e attendi che venga creato un po&#39; di tempo.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Ottieni l’URL dell’endpoint di streaming {#get-streaming-endpoint-url}

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experience Platform.

Per creare l&#39;URL utilizzato per configurare il webhook in [!DNL Pendo], è necessario recuperare quanto segue:

* **[!UICONTROL ID flusso di dati]**
* **[!UICONTROL Endpoint di streaming]**

Per recuperare l&#39;**[!UICONTROL ID flusso di dati]** e l&#39;**[!UICONTROL endpoint di streaming]**, vai alla pagina [!UICONTROL Attività flusso di dati] del flusso di dati appena creato e copia i dettagli dalla parte inferiore del pannello [!UICONTROL Proprietà].

![Endpoint di streaming nell&#39;attività del flusso di dati.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Dopo aver recuperato l&#39;endpoint di streaming e l&#39;ID del flusso di dati, generare un URL in base al seguente pattern: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Ad esempio, un URL del webhook costruito potrebbe avere l&#39;aspetto seguente: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Configura webhook in [!DNL Pendo] {#set-up-webhook}

Quindi, accedi al tuo account il [[!DNL Pendo]](https://pendo.io/) e crea un webhook. Per i passaggi su come creare un webhook utilizzando l&#39;interfaccia utente [!DNL Pendo], fare riferimento alla [[!DNL Pendo] guida sulla creazione di un webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Una volta creato il webhook, passare alla pagina delle impostazioni del webhook [!DNL Pendo] e immettere l&#39;URL del webhook nel campo [!DNL URL].

![La schermata dell&#39;interfaccia utente Pendo mostra il campo dell&#39;endpoint del webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>È possibile iscriversi a diverse categorie di eventi per determinare il tipo di eventi che si desidera inviare dall&#39;istanza [!DNL Pendo] a Platform. Per ulteriori informazioni sui diversi eventi, consulta la [[!DNL Pendo] documentazione](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione hai configurato correttamente un flusso di dati in streaming per portare i tuoi dati di [!DNL Pendo] all&#39;Experience Platform. Per monitorare i dati che vengono acquisiti, consulta la guida su [monitoraggio dei flussi di dati in streaming tramite l&#39;interfaccia utente di Platform](../../monitor-streaming.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui fare riferimento quando si utilizza l&#39;origine [!DNL Pendo].

### Convalida {#validation}

Per verificare la corretta configurazione dell&#39;origine e l&#39;acquisizione di [!DNL Pendo] messaggi, effettua le seguenti operazioni:

* È possibile controllare la pagina [!DNL Pendo] **[!UICONTROL Report]** > **[!UICONTROL Cronologia chat]** per identificare gli eventi acquisiti da [!DNL Pendo].

![Schermata dell&#39;interfaccia utente di Pendo che mostra la cronologia delle chat](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Nell&#39;interfaccia utente di Platform, selezionare **[!UICONTROL Visualizza flussi di dati]** accanto al menu della scheda [!DNL Pendo] nel catalogo delle origini. Selezionare **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti per i webhook configurati in [!DNL Pendo].

![Schermata dell&#39;interfaccia utente di Platform che mostra gli eventi acquisiti](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Errori e risoluzione problemi {#errors-and-troubleshooting}

Durante il controllo di un&#39;esecuzione del flusso di dati, è possibile che venga visualizzato il seguente messaggio di errore: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Schermata dell&#39;interfaccia utente di Platform che mostra l&#39;errore.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Per correggere questo errore, è necessario verificare che il mapping *uniqueID* sia stato configurato. Per ulteriori informazioni, consulta la sezione [Mapping](#mapping).

Per ulteriori informazioni, visitare il [[!DNL Pendo] Centro assistenza](https://www.pendo.io/help-center/).
