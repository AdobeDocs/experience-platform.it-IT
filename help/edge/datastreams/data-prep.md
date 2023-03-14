---
title: Preparazione per la raccolta dati
description: Scopri come mappare i dati su uno schema evento Experience Data Model (XDM) durante la configurazione di uno stream di dati per Adobe Experience Platform Web e Mobile SDK.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# Preparazione per la raccolta dati

Preparazione dati è un servizio di Adobe Experience Platform che consente di mappare, trasformare e convalidare i dati da e verso [Experience Data Model (XDM)](../../xdm/home.md). Durante la configurazione di un [flusso di dati](./overview.md), puoi utilizzare le funzionalità di preparazione dati per mappare i dati di origine su XDM quando li invii alla rete Edge di Platform.

>[!NOTE]
>
>Per informazioni complete su tutte le funzionalità di preparazione dati, comprese le funzioni di trasformazione per i campi calcolati, consulta la seguente documentazione:
>
>* [Panoramica sulla preparazione dati](../../data-prep/home.md)
>* [Funzioni di mappatura della preparazione dati](../../data-prep/functions.md)
>* [Gestione dei formati dei dati con la preparazione dati](../../data-prep/data-handling.md)


Questa guida illustra come mappare i dati nell’interfaccia utente di. Per seguire insieme ai passaggi, avvia il processo di creazione di un flusso di dati fino a (e incluso) il [passaggio di configurazione di base](./overview.md#create).

Per una dimostrazione rapida del processo di preparazione dei dati per la raccolta dei dati, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Selezionare i dati] {#select-data}

Seleziona **[!UICONTROL Salva ed Aggiungi mappatura]** dopo aver completato la configurazione di base per uno stream di dati e il **[!UICONTROL Seleziona dati]** viene visualizzato il passaggio. Da qui, devi fornire un oggetto JSON campione che rappresenti la struttura dei dati che intendi inviare a Platform.

Per acquisire proprietà direttamente dal livello dati, l’oggetto JSON deve avere una singola proprietà principale `data`. Le sottoproprietà del `data` L’oggetto deve quindi essere costruito in modo da essere mappato sulle proprietà del livello dati che desideri acquisire. Seleziona la sezione seguente per visualizzare un esempio di oggetto JSON formattato correttamente con un `data` radice.

+++File JSON di esempio con `data` radice

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Per acquisire proprietà da un elemento dati di un oggetto XDM, le stesse regole si applicano all’oggetto JSON, ma la proprietà principale deve essere impostata come `xdm` invece. Seleziona la sezione seguente per visualizzare un esempio di oggetto JSON formattato correttamente con un `xdm` radice.

+++File JSON di esempio con `xdm` radice

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

È possibile selezionare l&#39;opzione per caricare l&#39;oggetto come file oppure incollarlo nella casella di testo specificata. Se il JSON è valido, nel pannello di destra viene visualizzato uno schema di anteprima. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![Esempio JSON di dati in arrivo previsti](../assets/datastreams/data-prep/select-data.png)

## [!UICONTROL Mappatura]

Il **[!UICONTROL Mappatura]** viene visualizzato un passaggio che consente di mappare i campi nei dati di origine a quelli dello schema dell’evento di destinazione in Platform. Da qui puoi configurare la mappatura in due modi:

* [Creare nuove regole di mappatura](#create-mapping) per questo flusso di dati attraverso un processo manuale.
* [Importa regole di mappatura](#import-mapping) da un flusso di dati esistente.

### Crea una nuova mappatura {#create-mapping}

Per iniziare, seleziona **[!UICONTROL Aggiungi nuova mappatura]** per creare una nuova riga di mappatura.

![Aggiunta di una nuova mappatura](../assets/datastreams/data-prep/add-new-mapping.png)

Seleziona l’icona sorgente (![Icona sorgente](../assets/datastreams/data-prep/source-icon.png)) e nella finestra di dialogo visualizzata seleziona il campo di origine che desideri mappare nell’area di lavoro fornita. Dopo aver scelto un campo, utilizza **[!UICONTROL Seleziona]** per continuare.

![Selezione del campo da mappare nello schema di origine](../assets/datastreams/data-prep/source-mapping.png)

Quindi, seleziona l’icona dello schema (![Icona schema](../assets/datastreams/data-prep/schema-icon.png)) per aprire una finestra di dialogo simile per lo schema dell’evento di destinazione. Scegli il campo in cui mappare i dati prima di confermare con **[!UICONTROL Seleziona]**.

![Selezione del campo da mappare nello schema di destinazione](../assets/datastreams/data-prep/target-mapping.png)

Viene visualizzata di nuovo la pagina di mappatura con la mappatura di campi completata. Il **[!UICONTROL Avanzamento mappatura]** La sezione viene aggiornata per riflettere il numero totale di campi mappati correttamente.

![Campo mappato correttamente con avanzamento riflesso](../assets/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>Per mappare un array di oggetti (nel campo di origine) a un array di oggetti diversi (nel campo di destinazione), aggiungere `[*]` dopo il nome dell’array nei percorsi dei campi di origine e di destinazione, come mostrato di seguito.
>
>![Mappatura di oggetti array](../assets/datastreams/data-prep/array-object-mapping.png)

### Importa regole di mappatura esistenti {#import-mapping}

Se in precedenza hai creato un flusso di dati, puoi riutilizzarne le regole di mappatura configurate per un nuovo flusso di dati.

>[!WARNING]
>
>L’importazione di regole di mappatura da un altro stream di dati sovrascriverà eventuali mappature di campo aggiunte prima dell’importazione.

Per iniziare, seleziona **[!UICONTROL Importa mappatura]**.

![Immagine che mostra [!UICONTROL Importa mappatura] pulsante selezionato](../assets/datastreams/data-prep/import-mapping-button.png)

Nella finestra di dialogo visualizzata, seleziona lo stream di dati di cui desideri importare le regole di mappatura. Una volta scelto lo stream di dati, seleziona **[!UICONTROL Anteprima]**.

![Immagine che mostra un flusso di dati esistente che viene selezionato](../assets/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Gli stream di dati possono essere importati solo all’interno dello stesso [sandbox](../../sandboxes/home.md). In altre parole, non puoi importare un flusso di dati da una sandbox all’altra.

La schermata successiva mostra un’anteprima delle regole di mappatura salvate per lo stream di dati selezionato. Assicurati che le mappature visualizzate siano quelle previste, quindi seleziona **[!UICONTROL Importa]** per confermare e aggiungere le mappature al nuovo flusso di dati.

![Immagine che mostra le regole di mappatura da importare](../assets/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Se un campo di origine nelle regole di mappatura importate non è incluso nei dati JSON di esempio [fornito in precedenza](#select-data), queste mappature di campi non saranno incluse nell’importazione.

### Completare la mappatura

Continua a seguire i passaggi precedenti per mappare il resto dei campi sullo schema di destinazione. Anche se non è necessario mappare tutti i campi sorgente disponibili, tutti i campi nello schema di destinazione impostati come richiesto devono essere mappati per completare questo passaggio. Il **[!UICONTROL Campi obbligatori]** contatore indica quanti campi obbligatori non sono ancora mappati nella configurazione corrente.

Una volta che il conteggio dei campi obbligatori raggiunge zero e la mappatura è soddisfacente, seleziona **[!UICONTROL Salva]** per finalizzare le modifiche.

![Mappatura completata](../assets/datastreams/data-prep/mapping-complete.png)

## Passaggi successivi

Questa guida illustra come mappare i dati su XDM durante la configurazione di un flusso di dati nell’interfaccia utente. Se stavi seguendo l’esercitazione generale sui flussi di dati, ora puoi tornare al passaggio su [visualizzazione dei dettagli dello stream di dati](./overview.md).
