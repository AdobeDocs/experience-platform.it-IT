---
keywords: personalizzazione personalizzata; destinazione; destinazione personalizzata di experience platform;
title: Connessione di personalizzazione personalizzata
description: Questa destinazione fornisce personalizzazioni esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sul sito in modo da recuperare le informazioni sui segmenti da Adobe Experience Platform. Questa destinazione fornisce una personalizzazione in tempo reale basata sull’appartenenza al segmento del profilo utente.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# Connessione di personalizzazione personalizzata {#custom-personalization-connection}

## Panoramica {#overview}

Questa destinazione consente di recuperare le informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti.

## Prerequisiti {#prerequisites}

Questa integrazione è basata su [Adobe Experience Platform Web SDK](../../../edge/home.md) o [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Devi utilizzare uno di questi SDK per utilizzare questa destinazione.

>[!IMPORTANT]
>
>Prima di creare una connessione di personalizzazione personalizzata, consulta la guida su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](../../ui/configure-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi d’uso di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform.

## Tipo e frequenza di esportazione {#export-type-frequency}

**Richiesta profilo** : richiedi tutti i segmenti mappati nella destinazione di personalizzazione personalizzata per un singolo profilo. È possibile configurare diverse destinazioni di personalizzazione personalizzate per diverse destinazioni [Adobe Data Collection Datastreams](../../../edge/fundamentals/datastreams.md).

## Casi d’uso {#use-cases}

La [!DNL Custom personalization connection] consente di utilizzare piattaforme partner per la personalizzazione (ad esempio, [!DNL Optimizely], [!DNL Pega]), sfruttando anche le funzionalità di raccolta e segmentazione dei dati di Experience Platform Edge Network, per migliorare l’esperienza di personalizzazione dei clienti.

I casi d’uso descritti di seguito includono sia la personalizzazione del sito che la pubblicità mirata sul sito.

Per abilitare questi casi d’uso, i clienti hanno bisogno di un modo rapido e semplificato di recuperare le informazioni sui segmenti dall’Experience Platform e inviare tali informazioni ai loro sistemi designati configurati come connessioni di personalizzazione personalizzate nell’interfaccia utente di Experience Platform.

Questi sistemi possono essere piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione tra le proprietà web e mobile dei clienti.

### Personalizzazione a pagina singola {#same-page}

Un utente visita una pagina del sito web. Il cliente può utilizzare le informazioni sulla visita della pagina corrente (ad esempio, l’URL di riferimento, la lingua del browser e le informazioni sul prodotto incorporato) per selezionare l’azione o la decisione successiva (ad esempio, la personalizzazione), utilizzando la connessione di personalizzazione personalizzata per piattaforme non Adobi (ad esempio, [!DNL Pega], [!DNL Optimizely], ecc.).

### Personalizzazione di pagine successive {#next-page}

Un utente visita la pagina A sul sito web. In base a questa interazione, l’utente si è qualificato per un set di segmenti. L’utente fa quindi clic su un collegamento che li porta dalla pagina A alla pagina B. I segmenti per i quali l’utente si era qualificato durante l’interazione precedente sulla pagina A, insieme agli aggiornamenti di profilo determinati dalla visita del sito web corrente, verranno utilizzati per abilitare l’azione o la decisione successiva (ad esempio, il banner pubblicitario da visualizzare al visitatore o, in caso di test A/B, quale versione della pagina visualizzare).

### Personalizzazione di sessioni successive {#next-session}

Un utente visita diverse pagine del sito web. In base a queste interazioni, l’utente si è qualificato per un set di segmenti. L&#39;utente termina quindi la sessione di navigazione corrente.

Il giorno successivo, l&#39;utente ritorna allo stesso sito web del cliente. I segmenti per i quali si erano qualificati durante l’interazione precedente con tutte le pagine del sito web visitato, insieme agli aggiornamenti del profilo determinati dalla visita del sito web corrente, verranno utilizzati per selezionare l’azione/decisione successiva (ad esempio, il banner pubblicitario da visualizzare al visitatore o, in caso di test A/B, quale versione della pagina visualizzare).

## Collegati alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informazioni sugli ID di datastream"
>abstract="Questa opzione determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. È necessario configurare un datastream prima di poter configurare la destinazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Scopri come configurare un datastream"

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Inserisci una descrizione per la destinazione. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione. Questo campo è facoltativo.
* **[!UICONTROL Alias di integrazione]**: Questo valore viene inviato all’Experience Platform Web SDK come nome di oggetto JSON.
* **[!UICONTROL ID Datastream]**: Questo determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. Vedi [Configurazione di un datastream](../../../edge/fundamentals/datastreams.md) per ulteriori dettagli.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di richieste di profilo](../../ui/activate-profile-request-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Se utilizzi [Tag in Adobe Experience Platform](../../../tags/home.md) per implementare l’SDK web di Experience Platform, utilizza l’ [invio evento completato](../../../edge/extension/event-types.md) La funzionalità e l&#39;azione del codice personalizzato avranno un `event.destinations` che puoi utilizzare per visualizzare i dati esportati.

Di seguito è riportato un valore di esempio per `event.destinations` variabile:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Se non utilizzi [Tag](../../../tags/home.md) per implementare l’SDK web di Experience Platform, utilizza l’ [gestione delle risposte dagli eventi](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) per visualizzare i dati esportati.

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
