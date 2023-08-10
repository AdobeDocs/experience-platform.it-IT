---
title: Creare una connessione sorgente del catalogo nell’interfaccia utente
description: Scopri come creare una connessione sorgente di Chatlio utilizzando l’interfaccia utente di Adobe Experience Platform.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 1%

---

# Creare un [!DNL Chatlio] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Chatlio] sorgente in versione beta. Leggi le [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare [!DNL Chatlio] connessione sorgente mediante l’interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Prerequisiti {#prerequisites}

La sezione seguente fornisce informazioni sui prerequisiti da completare prima di poter creare un [!DNL Chatlio] connessione sorgente.

### JSON di esempio per definire lo schema di origine per [!DNL Chatlio] {#prerequisites-json-schema}

Prima di creare un [!DNL Chatlio] connessione di origine, sarà necessario specificare uno schema di origine. Puoi utilizzare il codice JSON qui sotto.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Creare uno schema di Platform per [!DNL Chatlio] {#create-platform-schema}

Devi anche assicurarti di creare uno schema Platform da utilizzare per la tua origine. Leggi l’esercitazione su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

![L’interfaccia utente di Platform mostra un esempio di schema per il catalogo](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Connetti [!DNL Chatlio] account {#connect-account}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] e visualizzare un catalogo delle origini disponibili in Experienci Platform.

Utilizza il *[!UICONTROL Categorie]* per filtrare le sorgenti per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Automazione del marketing] categoria per visualizzare [!DNL Chatlio] scheda sorgente. Per iniziare, seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo dell’interfaccia utente di Platform con scheda Catalogo](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Selezionare i dati {#select-data}

Il **[!UICONTROL Seleziona dati]** viene visualizzata un’interfaccia che consente di selezionare i dati da inserire in Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nella [!UICONTROL Trascinare i file] pannello.

![Il passaggio Aggiungi dati del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare [!UICONTROL Campo di ricerca] per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di anteprima del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Dettaglio del flusso di dati {#dataflow-detail}

Il **Dettagli del flusso di dati** Questo passaggio ti fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l’opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio del flusso di dati dettagliato del flusso di lavoro sorgenti.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Mappatura {#mapping}

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Le mappature elencate di seguito sono obbligatorie e devono essere configurate prima di procedere alla [!UICONTROL Revisione] fase.

| Campo di destinazione | Descrizione |
| --- | --- |
| `UUID` | Il [!DNL Chatlio] identificatore dell’evento. |

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Revisione {#review}

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Ottieni l’URL dell’endpoint di streaming {#get-streaming-endpoint-url}

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experienci Platform.

Per creare l’URL utilizzato per configurare il webhook su [!DNL Chatlio] è necessario recuperare quanto segue:

* **[!UICONTROL ID flusso di dati]**
* **[!UICONTROL Endpoint di streaming]**

Per recuperare **[!UICONTROL ID flusso di dati]** e **[!UICONTROL Endpoint di streaming]**, passare alla [!UICONTROL Attività flusso di dati] pagina del flusso di dati appena creato e copia i dettagli dalla parte inferiore della sezione [!UICONTROL Proprietà] pannello.

![Endpoint di streaming nell’attività del flusso di dati.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Dopo aver recuperato l’endpoint di streaming e l’ID del flusso di dati, crea un URL in base al seguente pattern: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Ad esempio, un URL del webhook costruito potrebbe avere l’aspetto di: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Configurazione webhook in [!DNL Chatlio] {#set-up-webhook}

Dopo aver creato l’URL del webhook, puoi configurarlo utilizzando [!DNL Chatlio] dell&#39;utente.

Accedi al tuo [[!DNL Chatlio]](https://chatlio.com/) account e follow [la guida alla configurazione e all&#39;installazione](https://chatlio.com/docs/setup/) per creare un widget.

Una volta creato un widget, passa alla pagina delle impostazioni del widget per aggiungere l’URL del webhook a tale widget.

![La pagina delle impostazioni del webhook su Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Quindi, seleziona la **[!DNL Behavior]** e aggiungi l’URL del webhook al *[!DNL Webhook when a new conversation starts]* e qualsiasi altro campo di eventi webhook a cui desideri iscriverti.

![Interfaccia utente di Chatlio che mostra il campo dell’endpoint del webhook.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>È possibile iscriversi a diversi eventi per [!DNL Chatlio] webhook. Per ulteriori informazioni sui diversi eventi, consulta [[!DNL Chatlio] documentazione sugli eventi](https://chatlio.com/docs/webhooks/).

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione hai configurato correttamente un flusso di dati in streaming per portare [!DNL Chatlio] dati di Experience Platform. Per monitorare i dati che vengono acquisiti, consulta la guida su [monitoraggio dei flussi di dati in streaming tramite l’interfaccia utente di Platform](../../monitor-streaming.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL Chatlio] sorgente.

### Convalida {#validation}

Per verificare di aver impostato correttamente l’origine e [!DNL Chatlio] I messaggi vengono acquisiti, effettua le seguenti operazioni:

* Puoi controllare la [!DNL Chatlio] **[!UICONTROL Rapporti]** > **[!UICONTROL Cronologia chat]** per identificare gli eventi acquisiti da [!DNL Chatlio].

![Schermata dell’interfaccia utente di Chatlio che mostra la cronologia della chat](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Visualizza flussi di dati]** accanto al [!DNL Chatlio] nel catalogo sorgenti. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti per i webhook configurati in [!DNL Chatlio].

![Schermata dell’interfaccia utente di Platform che mostra gli eventi acquisiti](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Per ulteriori informazioni su [!DNL Chatlio], visita il [[!DNL Chatlio] documentazione](https://chatlio.com/docs/) e [Domande frequenti](https://chatlio.com/pricing/#FAQ).
