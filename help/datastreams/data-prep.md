---
title: Preparazione dei dati per la raccolta dati
description: Scopri come mappare i dati su uno schema evento Experience Data Model (XDM) durante la configurazione di uno stream di dati per Adobe Experience Platform Web e Mobile SDK.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 60%

---

# Preparazione dei dati per la raccolta dati

La preparazione dati è un servizio di Adobe Experience Platform che consente di mappare, trasformare e convalidare i dati da e per [Experience Data Model (XDM)](../xdm/home.md). Durante la configurazione di uno [stream di dati](./overview.md), puoi utilizzare le funzionalità di preparazione dati per mappare i dati di origine su XDM quando li invii alla rete Edge di Platform.

Tutti i dati inviati da una pagina web devono arrivare ad Experience Platform come XDM. Esistono 3 modi per tradurre i dati da un livello dati su pagina a XDM accettato da Experience Platform:

1. Riformattare il livello dati in XDM sulla pagina web stessa.
2. Utilizza la funzionalità Tag elementi dati nativi per riformattare in XDM il formato di livello dati esistente di una pagina web.
3. Riformattare il formato del livello dati esistente di una pagina web in XDM tramite l’Edge Network, utilizzando la preparazione dati per la raccolta dati.

Questa guida si concentra sulla terza opzione.

## Quando utilizzare la preparazione dati per la raccolta dati {#when-to-use-data-prep}

Esistono due casi di utilizzo in cui la preparazione dei dati per la raccolta dei dati è utile:

1. Il sito web ha un livello di dati ben formato, gestito e mantenuto ed è preferibile inviarlo direttamente all’Edge Network invece di utilizzare la manipolazione di JavaScript per convertirlo in XDM sulla pagina (tramite elementi dati Tag o tramite la manipolazione manuale di JavaScript).
2. Sul sito viene distribuito un sistema di assegnazione tag diverso dai tag.

## Inviare un livello dati esistente all’Edge Network tramite Web SDK {#send-datalayer-via-websdk}

Il livello dati esistente deve essere inviato utilizzando l&#39;oggetto [`data`](/help/web-sdk/commands/sendevent/data.md) nel comando `sendEvent`.

Se utilizzi Tag, devi utilizzare il campo **[!UICONTROL Dati]** del tipo di azione **[!UICONTROL Invia evento]**, come descritto nella [documentazione sull&#39;estensione tag di Web SDK](/help/tags/extensions/client/web-sdk/action-types.md).

Il resto di questa guida si concentrerà su come mappare il livello dati agli standard XDM dopo che è stato inviato da WebSDK.

>[!NOTE]
>
>Per informazioni complete su tutte le funzionalità di preparazione dati, comprese le funzioni di trasformazione per i campi calcolati, consulta la seguente documentazione:
>
>* [Panoramica sulla preparazione dei dati](../data-prep/home.md)
>* [Funzioni di mappatura della preparazione dei dati](../data-prep/functions.md)
>* [Gestione dei formati dei dati con la preparazione dei dati](../data-prep/data-handling.md)

Questa guida illustra come mappare i dati nell’interfaccia utente. Per seguire i passaggi, avvia il processo di creazione di uno stream di dati fino al [passaggio di configurazione di base](./overview.md#create) (incluso).

Per una dimostrazione rapida del processo di preparazione dei dati per la raccolta dati, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Selezionare i dati] {#select-data}

Dopo aver completato la configurazione di base per uno stream di dati, seleziona **[!UICONTROL Salva e Aggiungi mappatura]** e verrà visualizzato il passaggio **[!UICONTROL Seleziona dati]**. Da qui, devi fornire un oggetto JSON di esempio che rappresenta la struttura dei dati che intendi inviare a Platform.

Per acquisire proprietà direttamente dal livello dati, l’oggetto JSON deve avere una singola proprietà principale `data`. Le sottoproprietà dell&#39;oggetto `data` devono quindi essere costruite in modo da eseguire il mapping alle proprietà del livello dati che si desidera acquisire. Seleziona la sezione seguente per visualizzare un esempio di oggetto JSON formattato correttamente con una radice `data`.

+++File JSON di esempio con radice `data`

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

Per acquisire proprietà da un elemento dati di un oggetto XDM, all’oggetto JSON si applicano le stesse regole, ma la proprietà principale deve essere invece impostata come `xdm`. Seleziona la sezione seguente per visualizzare un esempio di oggetto JSON formattato correttamente con una radice `xdm`.

+++File JSON di esempio con radice `xdm`

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

È possibile selezionare l’opzione per caricare l’oggetto come file oppure incollarlo nella casella di testo specificata. Se il JSON è valido, nel pannello di destra viene visualizzato uno schema di anteprima. Seleziona **[!UICONTROL Avanti]** per continuare.

![Esempio JSON di dati in arrivo previsti.](assets/data-prep/select-data.png)

>[!NOTE]
>
> Utilizza un oggetto JSON di esempio che rappresenta ogni elemento del livello dati che può essere utilizzato su qualsiasi pagina. Ad esempio, non tutte le pagine utilizzano gli elementi del livello dati del carrello. Tuttavia, gli elementi del livello dati del carrello devono essere inclusi in questo oggetto JSON di esempio.

## [!UICONTROL Mappatura]

Viene visualizzato il passaggio di **[!UICONTROL mappatura]**, consentendoti di mappare i campi nei dati di origine su quelli dello schema dell’evento di destinazione in Platform. Da qui puoi configurare la mappatura in due modi:

* [Crea regole di mappatura](#create-mapping) per questo flusso di dati tramite un processo manuale.
* [Importare regole di mappatura](#import-mapping) da un flusso di dati esistente.

### Creare regole di mappatura {#create-mapping}

Per creare una regola di mapping, selezionare **[!UICONTROL Aggiungi nuovo mapping]**.

![Aggiunta di una nuova mappatura.](assets/data-prep/add-new-mapping.png)

Seleziona l’icona della sorgente (![Icona sorgente](/help/images/icons/source.png)) e nella finestra di dialogo visualizzata seleziona il campo di origine che desideri mappare nell’area di lavoro fornita. Dopo aver scelto un campo, utilizza il pulsante **[!UICONTROL Seleziona]** per continuare.

![Selezione del campo da mappare nello schema di origine.](assets/data-prep/source-mapping.png)

Quindi, seleziona l’icona dello schema (![Icona dello schema](/help/images/icons/schema.png)) per aprire una finestra di dialogo simile per lo schema dell’evento di destinazione. Scegli il campo in cui mappare i dati prima di confermare con **[!UICONTROL Seleziona]**.

![Selezione del campo da mappare nello schema di destinazione.](assets/data-prep/target-mapping.png)

Viene visualizzata di nuovo la pagina della mappatura con la mappatura di campi completata. La sezione **[!UICONTROL Avanzamento della mappatura]** viene aggiornata per riflettere il numero totale di campi mappati correttamente.

![Il campo è stato mappato correttamente con l&#39;avanzamento riflesso.](assets/data-prep/field-mapped.png)

>[!TIP]
>
>Per mappare un array di oggetti (nel campo di origine) su un array di oggetti diversi (nel campo di destinazione), aggiungi `[*]` dopo il nome dell’array nei percorsi dei campi di origine e di destinazione, come illustrato di seguito.
>
>![Mappatura oggetto array.](assets/data-prep/array-object-mapping.png)

### Importare regole di mappatura esistenti {#import-mapping}

Se in precedenza hai creato un flusso di dati, puoi riutilizzarne le regole di mappatura configurate per un nuovo flusso di dati.

>[!WARNING]
>
>L’importazione di regole di mappatura da un altro stream di dati sovrascrive eventuali mappature di campo aggiunte prima dell’importazione.

Per iniziare, seleziona **[!UICONTROL Importa mappatura]**.

![Pulsante Importa mapping selezionato.](assets/data-prep/import-mapping-button.png)

Nella finestra di dialogo visualizzata, seleziona lo stream di dati di cui desideri importare le regole di mappatura. Una volta scelto lo stream di dati, seleziona **[!UICONTROL Anteprima]**.

![Selezione di uno stream di dati esistente.](assets/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Gli stream di dati possono essere importati solo all’interno della stessa [sandbox](../sandboxes/home.md). In altre parole, non puoi importare uno stream di dati da una sandbox all’altra.

La schermata successiva mostra un’anteprima delle regole di mappatura salvate per lo stream di dati selezionato. Assicurati che le mappature visualizzate siano quelle previste, quindi seleziona **[!UICONTROL Importa]** per confermare e aggiungere le mappature al nuovo stream di dati.

![Regole di mappatura da importare.](assets/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Se un campo di origine nelle regole di mappatura importate non è incluso nei dati JSON di esempio [forniti in precedenza](#select-data), tali mappature di campi non saranno incluse nell’importazione.

### Completare la mappatura

Continua a seguire i passaggi precedenti per mappare il resto dei campi sullo schema di destinazione. Anche se non è necessario mappare tutti i campi sorgente disponibili, tutti i campi nello schema di destinazione impostati come richiesto devono essere mappati per completare questo passaggio. Il contatore dei **[!UICONTROL Campi obbligatori]** indica quanti campi obbligatori non sono ancora mappati nella configurazione corrente.

Una volta che il conteggio dei campi richiesto raggiunge zero e la mappatura è soddisfacente, seleziona **[!UICONTROL Salva]** per finalizzare le modifiche.

![Mappatura completata](assets/data-prep/mapping-complete.png)

## Passaggi successivi

Questa guida illustra come mappare i dati su XDM durante la configurazione di uno stream di dati nell’interfaccia utente. Se stavi seguendo il tutorial generale sugli stream di dati, ora puoi tornare al passaggio sulla [visualizzazione dei dettagli dello stream di dati](./overview.md).
