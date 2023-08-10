---
title: Creare una connessione sorgente Pendo nell’interfaccia utente
description: Scopri come creare una connessione sorgente Pendo utilizzando l’interfaccia utente di Adobe Experience Platform.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 249a12e6a079e3c99bf13bec4bf83b2a53cd522b
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 1%

---

# Creare un [!DNL Pendo] flusso di dati della connessione sorgente e nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Pendo] sorgente in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare [!DNL Pendo] connessione sorgente e flusso di dati tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Prerequisiti {#prerequisites}

La sezione seguente fornisce informazioni sui prerequisiti da completare prima di poter creare un [!DNL Pendo] connessione sorgente.

### JSON di esempio per definire lo schema di origine per [!DNL Pendo] {#prerequisites-json-schema}

Prima di creare un [!DNL Pendo] connessione di origine, sarà necessario specificare uno schema di origine. Puoi utilizzare il codice JSON qui sotto.

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

Per ulteriori informazioni, leggere [[!DNL Pendo] guida sui webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Creare uno schema di Platform per [!DNL Pendo] {#create-platform-schema}

Devi anche assicurarti di creare prima uno schema Platform da utilizzare per la tua origine. Guarda il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

![Interfaccia utente di Platform che mostra un esempio di schema per Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Connetti [!DNL Pendo] account {#connect-account}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] e visualizzare un catalogo delle origini disponibili in Experienci Platform.

Utilizza il *[!UICONTROL Categorie]* per filtrare le sorgenti per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Analytics] categoria per visualizzare [!DNL Pendo] scheda sorgente. Per iniziare, seleziona **[!UICONTROL Aggiungi dati]**.

![Il catalogo sorgente dell’interfaccia utente di Platform con la scheda Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Selezionare i dati {#select-data}

Il **[!UICONTROL Seleziona dati]** viene visualizzata un’interfaccia che consente di selezionare i dati da inserire in Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nella [!UICONTROL Trascinare i file] pannello.

![Il passaggio Aggiungi dati del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare [!UICONTROL Campo di ricerca] per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di anteprima del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Dettaglio del flusso di dati {#dataflow-detail}

Il **Dettagli del flusso di dati** Questo passaggio ti fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l’opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio del flusso di dati dettagliato del flusso di lavoro sorgenti.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mappatura {#mapping}

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Le mappature elencate di seguito sono obbligatorie e devono essere configurate prima di procedere alla [!UICONTROL Revisione] fase.

| Campo di destinazione | Descrizione |
| --- | --- |
| `uniqueId` | Il [!DNL Pendo] identificatore dell’evento. |

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Revisione {#review}

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Ottieni l’URL dell’endpoint di streaming {#get-streaming-endpoint-url}

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experienci Platform.

Per creare l’URL utilizzato per configurare il webhook su [!DNL Pendo] è necessario recuperare quanto segue:

* **[!UICONTROL ID flusso di dati]**
* **[!UICONTROL Endpoint di streaming]**

Per recuperare **[!UICONTROL ID flusso di dati]** e **[!UICONTROL Endpoint di streaming]**, passare alla [!UICONTROL Attività flusso di dati] pagina del flusso di dati appena creato e copia i dettagli dalla parte inferiore della sezione [!UICONTROL Proprietà] pannello.

![Endpoint di streaming nell’attività del flusso di dati.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Dopo aver recuperato l’endpoint di streaming e l’ID del flusso di dati, crea un URL in base al seguente pattern: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Ad esempio, un URL del webhook costruito potrebbe avere l’aspetto di: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Configurazione webhook in [!DNL Pendo] {#set-up-webhook}

Quindi, accedi al tuo account su [[!DNL Pendo]](https://pendo.io/) e creare un webhook. Per i passaggi su come creare un webhook utilizzando [!DNL Pendo] dell&#39;interfaccia utente, fare riferimento al [[!DNL Pendo] guida alla creazione di webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Una volta creato il webhook, accedi alla pagina delle impostazioni del [!DNL Pendo] e immettere l&#39;URL del webhook nel [!DNL URL] campo.

![La schermata dell’interfaccia utente Pendo che mostra il campo dell’endpoint del webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Puoi iscriverti a diverse categorie di eventi per determinare il tipo di eventi che desideri inviare dal tuo [!DNL Pendo] da un’istanza a Platform. Per ulteriori informazioni sui diversi eventi, consulta [[!DNL Pendo] documentazione](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione hai configurato correttamente un flusso di dati in streaming per portare [!DNL Pendo] dati di Experience Platform. Per monitorare i dati che vengono acquisiti, consulta la guida su [monitoraggio dei flussi di dati in streaming tramite l’interfaccia utente di Platform](../../monitor-streaming.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL Pendo] sorgente.

### Convalida {#validation}

Per verificare di aver impostato correttamente l’origine e [!DNL Pendo] I messaggi vengono acquisiti, effettua le seguenti operazioni:

* Puoi controllare la [!DNL Pendo] **[!UICONTROL Rapporti]** > **[!UICONTROL Cronologia chat]** per identificare gli eventi acquisiti da [!DNL Pendo].

![Schermata dell’interfaccia utente Pendo che mostra la cronologia della chat](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Visualizza flussi di dati]** accanto al [!DNL Pendo] nel catalogo sorgenti. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti per i webhook configurati in [!DNL Pendo].

![Schermata dell’interfaccia utente di Platform che mostra gli eventi acquisiti](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Errori e risoluzione problemi {#errors-and-troubleshooting}

Durante il controllo di un’esecuzione del flusso di dati, è possibile che venga visualizzato il seguente messaggio di errore: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![La schermata dell’interfaccia utente di Platform mostra l’errore.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Per correggere questo errore, è necessario verificare che *uniqueID* la mappatura è stata impostata. Per ulteriori informazioni, consulta [Mappatura](#mapping) sezione.

Per ulteriori informazioni, visitare il [[!DNL Pendo] Centro risorse](https://www.pendo.io/help-center/).
