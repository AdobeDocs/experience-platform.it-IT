---
title: Preparazione per la raccolta dati
description: Scopri come mappare i dati su uno schema evento Experience Data Model (XDM) durante la configurazione di un datastream per gli SDK Adobe Experience Platform Web e Mobile.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# Preparazione per la raccolta dati

Data Prep è un servizio Adobe Experience Platform che ti consente di mappare, trasformare e convalidare i dati da e verso [Experience Data Model (XDM)](../../xdm/home.md). Durante la configurazione di una piattaforma abilitata [datastream](./overview.md), puoi utilizzare le funzionalità di preparazione dei dati per mappare i dati di origine a XDM al momento dell’invio a Platform Edge Network.

>[!NOTE]
>
>Per una guida completa su tutte le funzionalità di preparazione dei dati, comprese le funzioni di trasformazione per i campi calcolati, consulta la seguente documentazione:
>
>* [Panoramica sulla preparazione dei dati](../../data-prep/home.md)
>* [Funzioni di mappatura della preparazione dei dati](../../data-prep/functions.md)
>* [Gestione dei formati di dati con Data Prep](../../data-prep/data-handling.md)


Questa guida illustra come mappare i dati nell’interfaccia utente di . Per seguire questi passaggi, avvia il processo di creazione di un datastream fino a (e includere) il [passaggio di configurazione di base](./overview.md#create).

Per una rapida dimostrazione del processo di preparazione dei dati per la raccolta dei dati, fai riferimento al seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Seleziona dati] {#select-data}

Seleziona **[!UICONTROL Salvare e aggiungere mappature]** dopo aver completato la configurazione di base per un datastream, e **[!UICONTROL Seleziona dati]** viene visualizzato il passaggio . Da qui, devi fornire un oggetto JSON di esempio che rappresenti la struttura dei dati che intendi inviare a Platform.

Per acquisire le proprietà direttamente dal livello dati, l’oggetto JSON deve avere una singola proprietà principale `data`. Le sottoproprietà della `data` L&#39;oggetto deve quindi essere costruito in modo da essere mappato sulle proprietà del livello dati che si desidera acquisire. Seleziona la sezione seguente per visualizzare un esempio di oggetto JSON formattato correttamente con un `data` radice.

++Esempio di file JSON con `data` root

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

Per acquisire le proprietà da un elemento dati oggetto XDM, le stesse regole si applicano all’oggetto JSON, ma la proprietà principale deve essere impostata come chiave `xdm` invece. Seleziona la sezione seguente per visualizzare un esempio di oggetto JSON formattato correttamente con un `xdm` radice.

++Esempio di file JSON con `xdm` root

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

È possibile selezionare l’opzione per caricare l’oggetto come file oppure incollare l’oggetto non elaborato nella casella di testo fornita. Se il JSON è valido, nel pannello di destra viene visualizzato uno schema di anteprima. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![Esempio JSON di dati in arrivo previsti](../assets/datastreams/data-prep/select-data.png)

## [!UICONTROL Mappatura]

La **[!UICONTROL Mappatura]** viene visualizzato un passaggio che ti consente di mappare i campi nei dati di origine a quelli dello schema dell’evento di destinazione in Platform. Da qui, puoi configurare la mappatura in due modi:

* [Creare nuove regole di mappatura](#create-mapping) per questo datastream attraverso un processo manuale.
* [Importa regole di mappatura](#import-mapping) da un datastream esistente.

### Creare una nuova mappatura {#create-mapping}

Per iniziare, seleziona **[!UICONTROL Aggiungi nuova mappatura]** per creare una nuova riga di mappatura.

![Aggiunta di una nuova mappatura](../assets/datastreams/data-prep/add-new-mapping.png)

Seleziona l’icona sorgente (![Icona Sorgente](../assets/datastreams/data-prep/source-icon.png)) e nella finestra di dialogo visualizzata seleziona il campo sorgente da mappare nell’area di lavoro fornita. Dopo aver scelto un campo, utilizza le **[!UICONTROL Seleziona]** per continuare.

![Selezione del campo da mappare nello schema di origine](../assets/datastreams/data-prep/source-mapping.png)

Quindi, seleziona l’icona dello schema (![Icona Schema](../assets/datastreams/data-prep/schema-icon.png)) per aprire una finestra di dialogo simile per lo schema dell’evento di destinazione. Scegli il campo a cui desideri mappare i dati prima di confermare con **[!UICONTROL Seleziona]**.

![Selezione del campo da mappare nello schema di destinazione](../assets/datastreams/data-prep/target-mapping.png)

Viene visualizzata nuovamente la pagina di mappatura con la mappatura del campo completata. La **[!UICONTROL Avanzamento mappatura]** aggiornamenti della sezione per riflettere il numero totale di campi mappati correttamente.

![Campo mappato con avanzamento riflesso](../assets/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>Se si desidera mappare una matrice di oggetti (nel campo di origine) a una matrice di oggetti diversi (nel campo di destinazione), aggiungere `[*]` dopo il nome della matrice nei percorsi dei campi di origine e di destinazione, come illustrato di seguito.
>
>![Mappatura degli oggetti array](../assets/datastreams/data-prep/array-object-mapping.png)

### Importa regole di mappatura esistenti {#import-mapping}

Se in precedenza hai creato un datastream, puoi riutilizzarne le regole di mappatura configurate per un nuovo datastream.

>[!WARNING]
>
>L’importazione di regole di mappatura da un altro datastream sovrascrive eventuali mappature di campo aggiunte prima dell’importazione.

Per iniziare, seleziona **[!UICONTROL Mapping importazione]**.

![Immagine che mostra [!UICONTROL Mapping importazione] pulsante selezionato](../assets/datastreams/data-prep/import-mapping-button.png)

Nella finestra di dialogo visualizzata, seleziona il datastream di cui desideri importare le regole di mappatura. Una volta selezionato il datastream, seleziona **[!UICONTROL Anteprima]**.

![Immagine che mostra un datastream esistente selezionato](../assets/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>I datastreams possono essere importati solo all’interno dello stesso [sandbox](../../sandboxes/home.md). In altre parole, non è possibile importare un datastream da una sandbox all’altra.

La schermata successiva mostra un&#39;anteprima delle regole di mappatura salvate per il datastream selezionato. Assicurati che le mappature visualizzate siano quelle previste, quindi seleziona **[!UICONTROL Importa]** per confermare e aggiungere le mappature al nuovo datastream.

![Immagine che mostra le regole di mappatura da importare](../assets/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Se i campi di origine nelle regole di mappatura importate non sono inclusi nei dati JSON di esempio che [precedente](#select-data), tali mappature dei campi non verranno incluse nell’importazione.

### Completare la mappatura

Continua seguendo i passaggi precedenti per mappare il resto dei campi allo schema di destinazione. Anche se non è necessario mappare tutti i campi di origine disponibili, per completare questo passaggio è necessario mappare tutti i campi dello schema di destinazione impostati come necessario. La **[!UICONTROL Campi obbligatori]** contatore indica quanti campi obbligatori non sono ancora stati mappati nella configurazione corrente.

Una volta che il conteggio dei campi obbligatori raggiunge lo zero e si è soddisfatti della mappatura, selezionare **[!UICONTROL Salva]** per finalizzare le modifiche.

![Mapping completato](../assets/datastreams/data-prep/mapping-complete.png)

## Passaggi successivi

Questa guida illustra come mappare i dati su XDM durante la configurazione di un datastream nell’interfaccia utente di . Se stavi seguendo un&#39;esercitazione generale sui datastreams, ora puoi tornare al passaggio [visualizzazione dei dettagli del datastream](./overview.md).
