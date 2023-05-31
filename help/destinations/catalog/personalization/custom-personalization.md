---
keywords: personalizzazione personalizzata; destinazione; destinazione personalizzata di experience platform;
title: Connessione di personalizzazione personalizzata
description: Questa destinazione fornisce personalizzazione esterna, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sul sito per recuperare informazioni sui segmenti da Adobe Experience Platform. Questa destinazione fornisce personalizzazione in tempo reale in base all’iscrizione al segmento del profilo utente.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 1ffcbabe29994fb881ff622394d669c4340c94f1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 9%

---


# Connessione di personalizzazione personalizzata {#custom-personalization-connection}

## Registro modifiche destinazione {#changelog}

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | A partire da maggio 2023, la **[!UICONTROL Personalizzazione personalizzata]** supporto di connessione [personalizzazione basata su attributi](../../ui/activate-edge-personalization-destinations.md#map-attributes) ed è generalmente disponibile per tutti i clienti. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Gli attributi del profilo possono contenere dati sensibili. Per proteggere questi dati, è necessario **[!UICONTROL Personalizzazione personalizzata]** La destinazione richiede l&#39;utilizzo di [API server di rete Edge](/help/server-api/overview.md) durante la configurazione della destinazione per la personalizzazione basata su attributi. Tutte le chiamate API server devono essere effettuate in un [contesto autenticato](../../../server-api/authentication.md).
>
><br>Se utilizzi già Web SDK o Mobile SDK per l’integrazione, puoi recuperare gli attributi tramite l’API server aggiungendo un’integrazione lato server.
>
><br>Se non segui i requisiti di cui sopra, la personalizzazione sarà basata solo sull’iscrizione al segmento.

## Panoramica {#overview}

Questa destinazione consente di recuperare informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti.

## Prerequisiti {#prerequisites}

Questa integrazione è basata su [Adobe Experience Platform Web SDK](../../../edge/home.md) o [SDK di Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/). Per utilizzare questa destinazione, devi utilizzare uno di questi SDK.

>[!IMPORTANT]
>
>Prima di creare una connessione di personalizzazione personalizzata, consulta la guida su come [attivare i dati del pubblico nelle destinazioni di personalizzazione edge](../../ui/activate-edge-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform.

## Tipo e frequenza di esportazione {#export-type-frequency}

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo tutti i segmenti mappati nella destinazione di personalizzazione personalizzata per un singolo profilo. È possibile impostare diverse destinazioni di personalizzazione personalizzate per diversi [Adobe di flussi di dati di Raccolta dati](../../../edge/datastreams/overview.md). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

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

Letto [Attivare profili e segmenti e destinazioni di personalizzazione Edge](../../ui/activate-edge-personalization-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

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
