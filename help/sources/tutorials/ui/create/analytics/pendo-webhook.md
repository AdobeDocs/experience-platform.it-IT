---
title: Creare una connessione Pendo Source nell’interfaccia utente
description: Scopri come creare una connessione sorgente Pendo utilizzando l’interfaccia utente Adobe Experience Platform.
badge: "Beta"
source-git-commit: 5a199262acd517516b1e5313a25ddff8f1b11959
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 1%

---

# Crea un [!DNL Pendo] flusso di dati della connessione sorgente e nell’interfaccia utente

>[!NOTE]
>
>La [!DNL Pendo] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Pendo] connessione sorgente e flusso di dati tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questa esercitazione richiede una comprensione approfondita dei seguenti componenti dell&#39;Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Prerequisiti {#prerequisites}

La sezione seguente fornisce informazioni sui prerequisiti da completare prima di creare un [!DNL Pendo] connessione di origine.

### JSON di esempio per definire lo schema di origine per [!DNL Pendo] {#prerequisites-json-schema}

Prima di creare un [!DNL Pendo] connessione di origine, sarà necessario specificare uno schema di origine. Puoi utilizzare il JSON riportato di seguito.

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

Per ulteriori informazioni, consulta la sezione [[!DNL Pendo] guida sui webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Creare uno schema di Platform per [!DNL Pendo] {#create-platform-schema}

È inoltre necessario assicurarsi di creare prima uno schema Platform da utilizzare per la propria origine. Guarda l’esercitazione su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

![Interfaccia utente della piattaforma che mostra uno schema di esempio per Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Collega il tuo [!DNL Pendo] account {#connect-account}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] visualizza un catalogo di origini disponibili in Experience Platform.

Utilizza la *[!UICONTROL Categorie]* per filtrare le origini per categoria. In alternativa, immetti un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Analytics] per visualizzare la categoria [!DNL Pendo] scheda sorgente. Per iniziare, seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo sorgente dell’interfaccia utente della piattaforma con la scheda Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Selezionare i dati {#select-data}

La **[!UICONTROL Seleziona dati]** viene visualizzato un passaggio che fornisce un’interfaccia per selezionare i dati da portare in Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia ti consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Caricare file]** per caricare un file JSON dal tuo sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nel [!UICONTROL Trascinamento di file] pannello.

![Il passaggio Aggiungi dati del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Una volta caricato il file, l&#39;interfaccia di anteprima si aggiorna per visualizzare un&#39;anteprima dello schema caricato. L’interfaccia di anteprima ti consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare [!UICONTROL Campo di ricerca] utilità per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di anteprima del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Dettaglio del flusso di dati {#dataflow-detail}

La **Dettaglio flusso di dati** viene visualizzato un passaggio che fornisce le opzioni per utilizzare un set di dati esistente o per stabilire un nuovo set di dati per il flusso di dati, nonché l’opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione di profili, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Il passaggio del flusso di lavoro origini del flusso di lavoro del flusso di lavoro del flusso di lavoro del flusso di lavoro dei dati.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mappatura {#mapping}

La [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un&#39;interfaccia per mappare i campi di origine dallo schema di origine ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura e dei campi calcolati, consulta la sezione [Guida all’interfaccia utente della preparazione dei dati](../../../../../data-prep/ui/mapping.md).

Le mappature elencate di seguito sono obbligatorie e devono essere configurate prima di procedere alla [!UICONTROL Revisione] stadio.

| Campo di destinazione | Descrizione |
| --- | --- |
| `uniqueId` | La [!DNL Pendo] identificatore dell&#39;evento. |

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Revisione {#review}

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
* **[!UICONTROL Assegna set di dati e campi mappa]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

![Il passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Ottieni l&#39;URL dell&#39;endpoint di streaming {#get-streaming-endpoint-url}

Con il flusso di dati in streaming creato, ora puoi recuperare l’URL dell’endpoint in streaming. Questo endpoint verrà utilizzato per abbonarsi al tuo webhook, consentendo alla tua sorgente di streaming di comunicare con Experience Platform.

Per costruire l&#39;URL utilizzato per configurare il webhook su [!DNL Pendo] devi recuperare quanto segue:

* **[!UICONTROL ID flusso di dati]**
* **[!UICONTROL Endpoint di streaming]**

Per recuperare **[!UICONTROL ID flusso di dati]** e **[!UICONTROL Endpoint di streaming]**, vai al [!UICONTROL Attività del flusso di dati] della pagina del flusso di dati appena creato e copia i dettagli dalla parte inferiore della sezione [!UICONTROL Proprietà] pannello.

![L’endpoint di streaming nell’attività del flusso di dati.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Dopo aver recuperato l’endpoint di streaming e l’ID del flusso di dati, crea un URL basato sul seguente pattern: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Ad esempio, un URL webhook costruito potrebbe avere un aspetto simile a: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Imposta Webhook in [!DNL Pendo] {#set-up-webhook}

Quindi, accedi al tuo account il [[!DNL Pendo]](https://pendo.io/) e creare un webhook. Per i passaggi su come creare un webhook utilizzando [!DNL Pendo] interfaccia utente, fare riferimento alla [[!DNL Pendo] guida alla creazione del webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Una volta creato il webhook, passa alla pagina delle impostazioni del [!DNL Pendo] Webhook e inserire l&#39;URL del webhook nel [!DNL URL] campo .

![Schermata dell’interfaccia utente Pendo che mostra il campo endpoint webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Puoi abbonarti a diverse categorie di eventi per determinare il tipo di eventi che desideri inviare dal tuo [!DNL Pendo] istanza a Platform. Per ulteriori informazioni sui diversi eventi, consulta la [[!DNL Pendo] documentazione](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione hai configurato correttamente un flusso di dati in streaming per portare il tuo [!DNL Pendo] dati ad Experience Platform. Per monitorare i dati che vengono acquisiti, consulta la guida in [monitoraggio dei flussi di dati tramite l’interfaccia utente di Platform](../../monitor-streaming.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono risorse aggiuntive a cui puoi fare riferimento quando utilizzi il [!DNL Pendo] sorgente.

### Convalida {#validation}

Per verificare di aver configurato correttamente l&#39;origine e [!DNL Pendo] i messaggi vengono acquisiti e segui i passaggi seguenti:

* Puoi controllare la [!DNL Pendo] **[!UICONTROL Rapporti]** > **[!UICONTROL Cronologia chat]** per identificare gli eventi acquisiti da [!DNL Pendo].

![Schermata Pendo UI che mostra la cronologia della chat](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Visualizza flussi di dati]** accanto al [!DNL Pendo] menu scheda nel catalogo origini. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti per i webhook configurati in [!DNL Pendo].

![Schermata dell’interfaccia utente della piattaforma che mostra gli eventi acquisiti](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Quando controlli un&#39;esecuzione di un flusso di dati, potresti riscontrare il seguente messaggio di errore: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Schermata dell’interfaccia utente della piattaforma che mostra l’errore.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Per correggere questo errore, è necessario verificare che il *uniqueID* mappatura impostata. Per ulteriori informazioni, consulta [Mmpping](#mapping) sezione .

Per ulteriori informazioni, visita la pagina [[!DNL Pendo] Centro assistenza](https://www.pendo.io/help-center/).