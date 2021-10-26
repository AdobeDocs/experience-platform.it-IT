---
keywords: personalizzazione personalizzata; destinazione; destinazione personalizzata di experience platform;
title: Connessione di personalizzazione personalizzata (Beta)
description: Questa destinazione fornisce personalizzazioni esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sul sito per recuperare le informazioni sui segmenti da Adobe Experience Platform. Questa destinazione fornisce 1:1 in tempo reale e personalizzazione in base all’appartenenza a un segmento di un profilo utente.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 50ab34cb9147cf880e199afad88e718875fb591f
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Connessione di personalizzazione personalizzata (Beta) {#custom-personalization-connection}

## Panoramica {#overview}

>[!IMPORTANT]
>
>La connessione di personalizzazione personalizzata in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa destinazione consente di recuperare le informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti.

## Prerequisiti {#prerequisites}

Questa integrazione è basata su [Adobe Experience Platform Web SDK](../../../edge/home.md). Devi usare questo SDK per usare questa destinazione.

## Tipo di esportazione {#export-type}

**Richiesta profilo** : richiedi tutti i segmenti mappati nella destinazione di personalizzazione personalizzata per un singolo profilo. È possibile configurare diverse destinazioni di personalizzazione personalizzate per diverse destinazioni [Adobe Data Collection Datastreams](../../../edge/fundamentals/datastreams.md).

## Casi di utilizzo {#use-cases}

Questa destinazione condivide i tipi di pubblico con server di annunci e applicazioni di personalizzazione senza Adobi, da utilizzare in tempo reale, per decidere quali utenti di annunci pubblicitari visualizzare su un sito web.

### Caso d&#39;uso n. 1

**Personalizzazione di una home page**

Un sito web di noleggio e vendita di casa vuole personalizzare la propria home page in base alle qualifiche dei segmenti in Adobe Experience Platform. L’azienda può selezionare i tipi di pubblico che devono ottenere un’esperienza personalizzata e mapparli sulla destinazione di personalizzazione personalizzata impostata per l’applicazione di personalizzazione non Adobe come criteri di targeting.

**Pubblicità on-site mirata**

Utilizzando una destinazione di personalizzazione personalizzata separata per il loro server di annunci, lo stesso sito web può eseguire il targeting della pubblicità sul sito utilizzando un diverso set di segmenti da Adobe Experience Platform come criteri di targeting.

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Inserisci una descrizione per la destinazione. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione. Questo campo è facoltativo.
* **[!UICONTROL Alias di integrazione]**: Questo valore viene inviato all’Experience Platform Web SDK come nome di oggetto JSON.
* **[!UICONTROL ID Datastream]**: Questo determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. Vedi [Configurazione di un datastream](../../../edge/fundamentals/datastreams.md) per ulteriori dettagli.

## Attiva i segmenti in questa destinazione {#activate}

Leggi [Attivare profili e segmenti nelle destinazioni di richieste di profilo](../../ui/activate-profile-request-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Se utilizzi [Adobe di tag](../../../tags/home.md) per implementare l’SDK web di Experience Platform, utilizza l’ [invio evento completato](../../../edge/extension/event-types.md) La funzionalità e l&#39;azione del codice personalizzato avranno un `event.destinations` che puoi utilizzare per visualizzare i dati esportati.

Di seguito è riportato un valore di esempio per `event.destinations` variabile:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77",
            "mergePolicyId":"69638c01-2099-4032-8b41-84bee8ebcfa4"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77",
            "mergePolicyId":"69638c01-2099-4032-8b41-84bee8ebcfa4"
         }
      ]
   }
]
```

Se non utilizzi [Adobe di tag](../../../tags/home.md) per implementare l’SDK web di Experience Platform, utilizza l’ [gestione delle risposte dagli eventi](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) per visualizzare i dati esportati.

La risposta JSON di Adobe Experience Platform può essere analizzata per trovare l’alias di integrazione corrispondente dell’applicazione che si sta integrando con Adobe Experience Platform. Gli ID del segmento possono essere passati nel codice dell’applicazione come parametri di targeting. Di seguito è riportato un esempio di come potrebbe essere specifico per la risposta di destinazione.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
