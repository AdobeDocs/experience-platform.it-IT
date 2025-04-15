---
keywords: personalizzazione personalizzati; destinazione; destinazione personalizzata Experience Platform;
title: Connessione personalizzazione personalizzata
description: Questa destinazione fornisce personalizzazione esterni, sistemi di gestione contenuto, server annuncio e altre applicazioni in esecuzione sul tuo sito un modo per recuperare informazioni sul pubblico dai Adobe Experience Platform. Questa destinazione fornisce personalizzazione in tempo reale in base all utente iscrizione del pubblico del profilo.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 0f70e072402bca055b96195ded91816810759fc2
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 9%

---


# Connessione personalizzazione personalizzata {#custom-personalization-connection}

## Changelog delle destinazioni {#changelog}

| Mese di uscita | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Maggio 2023 | Aggiornamento di funzionalità e documentazione | A partire da maggio 2023, la **[!UICONTROL connessione personalizzazione]** personalizzata supporta [personalizzazione](../../ui/activate-edge-personalization-destinations.md#map-attributes) basate su attributi ed è disponibile a livello generale per tutti i clienti. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Gli attributi del profilo possono contenere dati sensibili. Per proteggere questi dati, è necessario usare l&#39;API](/help/server-api/overview.md) del [server di rete Edge quando si configura la destinazione di personalizzazione **** personalizzata per personalizzazione basate su attributi. Tutte le chiamate API server devono essere effettuate in un [contesto](../../../server-api/authentication.md) autenticato.
>
><br>È possibile recuperare gli attributi del profilo tramite l&#39;API](/help/server-api/overview.md) del server di rete Edge aggiungendo un&#39;integrazione lato server che utilizza lo stesso flusso di dati già in uso per l&#39;SDK [Web o Mobile SDK implementazione.
>
><br>Se non seguire i requisiti di cui sopra, personalizzazione si baserà solo sull&#39;iscrizione del pubblico.

## Panoramica {#overview}

Configura questa destinazione per consentire alle piattaforme personalizzazione esterne, ai sistemi di gestione contenuto, ai server annuncio e ad altre applicazioni in esecuzione sui siti Web dei clienti di recuperare informazioni sul pubblico dai Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Questa destinazione richiede l&#39;utilizzo di uno dei seguenti metodi di raccolta dati, a seconda delle implementazione:

* Utilizza Adobe Experience Platform [Web SDK](/help/web-sdk/home.md) per raccogliere dati dal tuo sito Web.
* Utilizza l&#39;SDK [](https://developer.adobe.com/client-sdks/documentation/) di Adobe Experience Platform Mobile per raccogliere dati dal tuo app mobile.
* Usa l&#39;API del [server di rete Edge se non usi [Web SDK](/help/web-sdk/home.md) o [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) o se desideri personalizzare il esperienza di utilizzo in base agli attributi del](../../../server-api/overview.md) profilo.

>[!IMPORTANT]
>
>Prima di creare una connessione personalizzazione personalizzata, leggi la guida su come attivare i dati del [pubblico nelle destinazioni Edge personalizzazione](../../ui/activate-edge-personalization-destinations.md). Questa guida illustra i passaggi di configurazione necessari per i casi d&#39;uso dei personalizzazione della stessa pagina e della pagina successiva, su più componenti Experience Platform.

## Pubblico supportato {#supported-audiences}

In questa sezione vengono descritti i tipi di pubblico che puoi esportare verso questa destinazione.

| Origine del pubblico | Sostenuto | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences generati tramite il servizio](../../../segmentation/home.md) di segmentazione Experience Platform[. |
| Caricamenti personalizzati | ✓ | [Audiences importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo un unico profilo a tutti i tipi di pubblico mappati nella destinazione personalizzazione personalizzata. È possibile configurare destinazioni personalizzazione personalizzate diverse [per diversi flussi](../../../datastreams/overview.md) di dati di raccolta dati Adobe Systems dati. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l&#39;aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle destinazioni in [](/help/destinations/destination-types.md#streaming-destinations)streaming. |

## Connettersi alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informazioni sugli ID di stream di dati"
>abstract="Questa opzione determina in quale stream di dati di raccolta dati verranno inclusi i tipi di pubblico nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Prima di poter configurare la destinazione, devi configurare uno stream di dati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=it" text="Scopri come configurare uno stream di dati"

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL autorizzazioni](/help/access-control/home.md#permissions) Visualizza Destinazioni]** e **[!UICONTROL Gestisci destinazioni]** [accesso controllo. Leggi la panoramica](/help/access-control/ui/overview.md) sul [controllo accesso o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connetterti a questa destinazione, seguire i passaggi descritti nella esercitazione](../../ui/connect-destination.md) di configurazione della [destinazione.

### Parametri di connessione {#parameters}

Durante [la configurazione di](../../ui/connect-destination.md) questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: inserisci il nome che preferisci per questa destinazione.
* **[!UICONTROL Descrizione]**: inserisci una descrizione della destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
* **[!UICONTROL Alias]** di integrazione: questo valore viene inviato all&#39;SDK Web Experience Platform come nome oggetto JSON.
* **[!UICONTROL ID flusso]** di dati: determina in quale flusso di dati raccolta dati il pubblico verrà incluso nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Per ulteriori informazioni, consulta [Configurazione di un flusso](../../../datastreams/overview.md) di dati.

### Abilitare gli avvisi {#enable-alerts}

È possibile abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la destinazione. Seleziona un avviso dall&#39;elenco a cui iscriverti per ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida sulla [sottoscrizione agli avvisi relativi alle destinazioni utilizzando il interfaccia](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, selezionare **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, sono necessarie le **[!UICONTROL autorizzazioni](/help/access-control/home.md#permissions) Visualizza Destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Profili]** Visualizza e **[!UICONTROL Segmenti]** [Visualizza accesso controllo. Leggi la panoramica](/help/access-control/ui/overview.md) sul [controllo accesso o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Leggi [Attivare profili e tipi di pubblico ai margini personalizzazione destinazioni](../../ui/activate-edge-personalization-destinations.md) per istruzioni su come attivare i tipi di pubblico verso questa destinazione.

## Dati esportati {#exported-data}

Se si utilizzano [tag in Adobe Experience Platform](../../../tags/home.md) per distribuire l&#39;SDK Web Experience Platform, utilizzare la funzionalità di invio evento completo](../../../tags/extensions/client/web-sdk/event-types.md) e l&#39;azione [codice personalizzato avrà una `event.destinations` variabile che è possibile utilizzare per visualizzare i dati esportati.

Ecco un esempio di valore per la `event.destinations` variabile:

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

Se non si utilizzano [tag](/help/tags/home.md) per distribuire l&#39;SDK Web Experience Platform, utilizzare [le risposte](/help/web-sdk/commands/command-responses.md) dei comandi per visualizzare i dati esportati.

La risposta JSON di Adobe Experience Platform può essere analizzata per trovare l&#39;alias di integrazione corrispondente del applicazione che si sta integrando con Adobe Experience Platform. Gli ID pubblico possono essere passati nel codice dell&#39;applicazione come parametri targeting. Di seguito è riportato un esempio di ciò che questo aspetto like specifico per la risposta alla destinazione.

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
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Risposta di esempio per [!UICONTROL la personalizzazione personalizzata con attributi]

Quando si utilizza **[!UICONTROL la personalizzazione personalizzata con attributi]**, la risposta dell&#39;API sarà simile a quella riportata di seguito.

La differenza tra **[!UICONTROL Personalizzazione personalizzata con attributi]** e Personalizzazione **** personalizzata consiste nell&#39;inclusione `attributes` della sezione nella risposta API.

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

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le [!DNL Adobe Experience Platform] destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi la panoramica](../../../data-governance/home.md) sulla [governance dei dati.
