---
keywords: personalizzazione personalizzata; destinazione; destinazione personalizzata di experience platform;
title: Connessione di personalizzazione personalizzata
description: Questa destinazione fornisce personalizzazione esterna, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sul sito per recuperare informazioni sui segmenti da Adobe Experience Platform. Questa destinazione fornisce personalizzazione in tempo reale in base all’iscrizione al segmento del profilo utente.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# Connessione di personalizzazione personalizzata {#custom-personalization-connection}

## Registro modifiche destinazione {#changelog}

Con la versione beta di **[!UICONTROL Personalizzazione personalizzata]** connettore di destinazione, è possibile che siano presenti due **[!UICONTROL Personalizzazione personalizzata]** nel catalogo delle destinazioni.

Il **[!UICONTROL Personalizzazione Personalizzata Con Attributi]** il connettore è attualmente in versione beta e disponibile solo per un numero selezionato di clienti. Oltre alle funzionalità fornite dal **[!UICONTROL Personalizzazione personalizzata]**, il **[!UICONTROL Personalizzazione Personalizzata Con Attributi]** il connettore aggiunge un [passaggio di mappatura](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) al flusso di lavoro di attivazione, che consente di mappare gli attributi del profilo alla destinazione di personalizzazione personalizzata, abilitando la personalizzazione della stessa pagina e della pagina successiva basata su attributi.

>[!IMPORTANT]
>
>Gli attributi del profilo possono contenere dati sensibili. Per proteggere questi dati, è necessario **[!UICONTROL Personalizzazione Personalizzata Con Attributi]** La destinazione richiede l&#39;utilizzo di [API server di rete Edge](/help/server-api/overview.md) per la raccolta di dati. Inoltre, tutte le chiamate API server devono essere effettuate in un [contesto autenticato](../../../server-api/authentication.md).
>
>Se utilizzi già Web SDK o Mobile SDK per l’integrazione, puoi recuperare gli attributi tramite l’API server in due modi:
>
> * Aggiungi un’integrazione lato server che recupera gli attributi tramite l’API server.
> * Aggiorna la configurazione lato client con un codice JavaScript personalizzato per recuperare gli attributi tramite l’API server.
>
> Se non segui i requisiti di cui sopra, la personalizzazione sarà basata solo sull’iscrizione al segmento, identica all’esperienza offerta da **[!UICONTROL Personalizzazione personalizzata]** connettore.

![Immagine delle due schede di destinazione di personalizzazione personalizzata in una visualizzazione affiancata.](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## Panoramica {#overview}

Questa destinazione consente di recuperare informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti.

## Prerequisiti {#prerequisites}

Questa integrazione è basata su [Adobe Experience Platform Web SDK](../../../edge/home.md) o [SDK di Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/). Per utilizzare questa destinazione, devi utilizzare uno di questi SDK.

>[!IMPORTANT]
>
>Prima di creare una connessione di personalizzazione personalizzata, consulta la guida su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](../../ui/configure-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform.

## Tipo e frequenza di esportazione {#export-type-frequency}

**Richiesta profilo** : stai richiedendo tutti i segmenti mappati nella destinazione di personalizzazione personalizzata per un singolo profilo. È possibile impostare diverse destinazioni di personalizzazione personalizzate per diversi [Adobe di flussi di dati di Raccolta dati](../../../edge/datastreams/overview.md).

## Casi d’uso {#use-cases}

Il [!DNL Custom Personalization Connection] consente di utilizzare piattaforme di personalizzazione partner personalizzate (ad esempio, [!DNL Optimizely], [!DNL Pega]), nonché i sistemi proprietari (ad esempio, CMS interno), sfruttando al contempo le funzionalità di raccolta e segmentazione dei dati di Experience Platform Edge Network, per fornire ai clienti un&#39;esperienza di personalizzazione più approfondita.

I casi d’uso descritti di seguito includono sia la personalizzazione del sito che la pubblicità mirata nel sito.

Per abilitare questi casi d’uso, i clienti hanno bisogno di un modo rapido e semplificato per recuperare le informazioni sui segmenti da Experience Platform e inviarle ai sistemi designati che hanno configurato come connessioni di personalizzazione personalizzate nell’interfaccia utente di Experience Platform.

Questi sistemi possono essere piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione nelle proprietà web e mobili dei clienti.

### Personalizzazione stessa pagina {#same-page}

Un utente visita una pagina del sito web. Il cliente può utilizzare le informazioni sulla visita della pagina corrente (ad esempio, URL di riferimento, lingua del browser, informazioni sul prodotto incorporate) per selezionare l’azione o la decisione successiva (ad esempio, personalizzazione), utilizzando la connessione di personalizzazione personalizzata per piattaforme non di Adobe (ad esempio, [!DNL Pega], [!DNL Optimizely], ecc.).

### Personalizzazione della pagina successiva {#next-page}

Un utente visita la pagina A del sito web. In base a questa interazione, l’utente si è qualificato per un set di segmenti. L’utente fa quindi clic su un collegamento che li porta dalla pagina A alla pagina B. I segmenti per i quali l’utente si era qualificato durante la precedente interazione sulla pagina A, insieme agli aggiornamenti del profilo determinati dalla visita del sito web corrente, verranno utilizzati per potenziare l’azione/decisione successiva (ad esempio, quale banner pubblicitario mostrare al visitatore o, in caso di test A/B, quale versione della pagina visualizzare).

### Personalizzazione sessione successiva {#next-session}

Un utente visita diverse pagine del sito web. In base a queste interazioni, l’utente si è qualificato per un set di segmenti. L’utente termina quindi la sessione di navigazione corrente.

Il giorno successivo, l’utente ritorna allo stesso sito web del cliente. I segmenti per i quali erano qualificati durante la precedente interazione con tutte le pagine del sito web visitate, insieme agli aggiornamenti del profilo determinati dalla visita del sito web corrente, verranno utilizzati per selezionare l’azione/decisione successiva (ad esempio, quale banner pubblicitario mostrare al visitatore o, in caso di test A/B, quale versione della pagina visualizzare).

## Connetti alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informazioni sugli ID di stream di dati"
>abstract="Questa opzione determina in quale stream di dati di raccolta dati verranno inclusi i segmenti nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Prima di poter configurare la destinazione, devi configurare uno stream di dati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it" text="Scopri come configurare uno stream di dati"

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
* **[!UICONTROL Alias di integrazione]**: questo valore viene inviato all’SDK web per Experience Platform come nome di oggetto JSON.
* **[!UICONTROL ID flusso di dati]**: questo determina in quale flusso di dati di Raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Consulta [Configurazione di uno stream di dati](../../../edge/datastreams/overview.md) per ulteriori dettagli.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e segmenti nelle destinazioni delle richieste di profilo](../../ui/activate-profile-request-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

## Dati esportati {#exported-data}

Se sta usando [Tag in Adobe Experience Platform](../../../tags/home.md) per distribuire Experience Platform Web SDK, utilizza [invio evento completato](../../../edge/extension/event-types.md) e l&#39;azione del codice personalizzato avrà un `event.destinations` che è possibile utilizzare per visualizzare i dati esportati.

Esempio di valore per `event.destinations` variabile:

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

Se non utilizza [Tag](../../../tags/home.md) per distribuire Experience Platform Web SDK, utilizza [gestione delle risposte dagli eventi](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) per visualizzare i dati esportati.

È possibile analizzare la risposta JSON di Adobe Experience Platform per trovare l’alias di integrazione corrispondente dell’applicazione che si sta integrando con Adobe Experience Platform. Gli ID segmento possono essere trasmessi nel codice dell’applicazione come parametri di targeting. Di seguito è riportato un esempio di ciò che dovrebbe apparire specifico per la risposta di destinazione.

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Esempio di risposta per [!UICONTROL Personalizzazione Personalizzata Con Attributi]

Quando si utilizza **[!UICONTROL Personalizzazione Personalizzata Con Attributi]**, la risposta API sarà simile all’esempio seguente.

La differenza tra **[!UICONTROL Personalizzazione Personalizzata Con Attributi]** e **[!UICONTROL Personalizzazione personalizzata]** è l&#39;inclusione di `attributes` nella risposta API.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
