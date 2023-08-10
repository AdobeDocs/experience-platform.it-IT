---
title: Creare una connessione di origine Customer.io e un flusso di dati nell’interfaccia utente
description: Scopri come creare una connessione di origine Customer.io utilizzando l’interfaccia utente di Adobe Experience Platform.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 1%

---

# Creare un [!DNL Customer.io] connessione sorgente e flusso di dati nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Customer.io] sorgente in versione beta. Leggi le [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare [!DNL Customer.io] connessione sorgente e flusso di dati tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Prerequisiti {#prerequisites}

La sezione seguente fornisce informazioni sui prerequisiti da completare prima di poter creare un [!DNL Customer.io] connessione sorgente.

### JSON di esempio per definire lo schema di origine per [!DNL Customer.io] {#prerequisites-json-schema}

Prima di creare un [!DNL Customer.io] connessione di origine, sarà necessario specificare uno schema di origine. Puoi utilizzare il codice JSON seguente.

```
{
  "event_id": "01E4C4CT6YDC7Y5M7FE1GWWPQJ",
  "object_type": "customer",
  "metric": "subscribed",
  "timestamp": 1613063089,
  "data": {
    "customer_id": "42",
    "email_address": "test@example.com",
    "identifiers": {
      "id": "42",
      "email": "test@example.com",
      "cio_id": "d9c106000001"
    }
  }
}
```

### Creare uno schema di Platform per [!DNL Customer.io] {#create-platform-schema}

Devi anche assicurarti di creare uno schema Platform da utilizzare per la tua origine. Guarda il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

![Schermata dell’interfaccia utente di Platform che mostra un esempio di schema per Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Connetti [!DNL Customer.io] account {#connect-account}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] e visualizzare un catalogo delle origini disponibili in Experienci Platform.

Utilizza il *[!UICONTROL Categorie]* per filtrare le sorgenti per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Automazione del marketing] categoria per visualizzare [!DNL Customer.io] scheda sorgente. Per iniziare, seleziona **[!UICONTROL Aggiungi dati]**.

![Schermata dell’interfaccia utente di Platform per il catalogo con la scheda Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Selezionare i dati {#select-data}

Il **[!UICONTROL Seleziona dati]** viene visualizzata un’interfaccia che consente di selezionare i dati da inserire in Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nella [!UICONTROL Trascinare i file] pannello.

![Il passaggio Aggiungi dati del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare [!UICONTROL Campo di ricerca] per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di anteprima del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Dettaglio del flusso di dati {#dataflow-detail}

Il **Dettagli del flusso di dati** Questo passaggio ti fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l’opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio del flusso di dati dettagliato del flusso di lavoro sorgenti.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Mappatura {#mapping}

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Tutte le mappature elencate di seguito sono obbligatorie e devono essere configurate prima di procedere alla [!UICONTROL Revisione] fase.

| Campo di destinazione | Descrizione |
| --- | --- |
| `object_type` | Il tipo di oggetto, fare riferimento al [!DNL Customer.io] [Eventi](https://customer.io/docs/webhooks/#events) documentazione per i tipi supportati. |
| `id` | Identificatore dell&#39;oggetto. |
| `email` | Indirizzo e-mail associato all’oggetto. |
| `event_id` | L’identificatore univoco dell’evento. |
| `cio_id` | Il [!DNL Customer.io] identificatore dell’evento. |
| `metric` | Il tipo di evento. Per ulteriori informazioni, consulta [!DNL Customer.io] [Eventi](https://customer.io/docs/webhooks/#events) documentazione per i tipi supportati. |
| `timestamp` | La marca temporale in cui si è verificato l’evento. |

>[!IMPORTANT]
>
>Non mappare `cio_id` durante l&#39;esecuzione [!DNL Customer.io] webhook in `test mode` poiché non vi saranno campi associati inviati da [!DNL Customer.io].

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Revisione {#review}

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Ottieni l’URL dell’endpoint di streaming {#get-streaming-endpoint}

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experienci Platform.

Per creare l’URL utilizzato per configurare il webhook su [!DNL Customer.io] è necessario recuperare quanto segue:

* **[!UICONTROL ID flusso di dati]**
* **[!UICONTROL Endpoint di streaming]**

Per recuperare **[!UICONTROL ID flusso di dati]** e **[!UICONTROL Endpoint di streaming]**, passare alla [!UICONTROL Attività flusso di dati] pagina del flusso di dati appena creato e copia i dettagli dalla parte inferiore della sezione [!UICONTROL Proprietà] pannello.

![Endpoint di streaming nell’attività del flusso di dati.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Dopo aver recuperato l’endpoint di streaming e l’ID del flusso di dati, crea un URL in base al seguente pattern: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Ad esempio, un URL del webhook costruito potrebbe avere l’aspetto di: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Configurare il webhook di reporting in [!DNL Customer.io] {#set-up-webhook}

Dopo aver creato l’URL del webhook, ora puoi impostare il webhook di reporting utilizzando [!DNL Customer.io] dell&#39;utente. Per i passaggi sulla configurazione dei webhook di reporting, leggi [[!DNL Customer.io] guida](https://customer.io/docs/webhooks/#setup) sulla configurazione dei webhook.

In [!DNL Customer.io] interfaccia utente, immettere [URL webhook](#get-streaming-endpoint-url) nel [!DNL WEBHOOK ENDPOINT] campo.

![Interfaccia utente Customer.io con il campo dell&#39;endpoint webhook](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Puoi abbonarti a diversi eventi per il tuo webhook di reporting. I messaggi di ogni evento verranno acquisiti in Platform quando [!DNL Customer.io] sono soddisfatti i criteri di attivazione dell’evento dell’azione. Per ulteriori informazioni sui diversi eventi, consulta [[!DNL Customer.io] documentazione sugli eventi](https://customer.io/docs/webhooks/#events).

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione hai configurato correttamente un flusso di dati in streaming per portare [!DNL Customer.io] dati di Experience Platform. Per monitorare i dati che vengono acquisiti, consulta la guida su [monitoraggio dei flussi di dati in streaming tramite l’interfaccia utente di Platform](../../monitor-streaming.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL Customer.io] sorgente.

### Guardrail {#guardrails}

Per informazioni sui guardrail, fare riferimento al [[!DNL Customer.io] pagina timeout ed errori](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Convalida {#validation}

Per verificare di aver impostato correttamente l’origine e [!DNL Customer.io] I messaggi vengono acquisiti, effettua le seguenti operazioni:

* Puoi controllare la [!DNL Customer.io] **[!UICONTROL Registri attività]** per identificare gli eventi acquisiti da [!DNL Customer.io].

![Schermata dell’interfaccia utente Customer.io con i registri delle attività](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Visualizza flussi di dati]** accanto al [!DNL Customer.io] nel catalogo sorgenti. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti per gli eventi selezionati in [!DNL Customer.io].

![Schermata dell’interfaccia utente di Platform che mostra gli eventi acquisiti](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
