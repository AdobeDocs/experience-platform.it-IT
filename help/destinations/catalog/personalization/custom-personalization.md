---
keywords: personalizzazione personalizzata; destinazione; destinazione personalizzata di experience platform;
title: Connessione di personalizzazione personalizzata
description: Questa destinazione fornisce personalizzazione esterna, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sul sito in modo da recuperare informazioni sul pubblico da Adobe Experience Platform. Questa destinazione fornisce una personalizzazione in tempo reale in base all’iscrizione al pubblico del profilo utente.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 0f70e072402bca055b96195ded91816810759fc2
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 9%

---


# Connessione di personalizzazione personalizzata {#custom-personalization-connection}

## Registro modifiche destinazione {#changelog}

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | A maggio 2023, la connessione **[!UICONTROL Personalizzazione personalizzata]** supporta la [personalizzazione basata su attributi](../../ui/activate-edge-personalization-destinations.md#map-attributes) ed è generalmente disponibile per tutti i clienti. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Gli attributi del profilo possono contenere dati sensibili. Per proteggere questi dati, è necessario utilizzare l&#39;[API server Edge Network](/help/server-api/overview.md) durante la configurazione della destinazione **[!UICONTROL Personalization]** personalizzata per la personalizzazione basata su attributi. Tutte le chiamate API server devono essere effettuate in un [contesto autenticato](../../../server-api/authentication.md).
>
><br>È possibile recuperare gli attributi del profilo tramite [Edge Network Server API](/help/server-api/overview.md) aggiungendo un&#39;integrazione lato server che utilizza lo stesso flusso di dati già in uso per l&#39;implementazione Web o Mobile SDK.
>
><br>Se non segui i requisiti di cui sopra, la personalizzazione sarà basata solo sull&#39;iscrizione al pubblico.

## Panoramica {#overview}

Configura questa destinazione per consentire alle piattaforme di personalizzazione esterne, ai sistemi di gestione dei contenuti, ai server di annunci e ad altre applicazioni in esecuzione sui siti web dei clienti di recuperare informazioni sul pubblico da Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Questa destinazione richiede l’utilizzo di uno dei seguenti metodi di raccolta dati, a seconda dell’implementazione:

* Utilizza [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) se desideri raccogliere dati dal tuo sito Web.
* Utilizza [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) se desideri raccogliere dati dalla tua app mobile.
* Utilizza l&#39;[Edge Network Server API](../../../server-api/overview.md) se non utilizzi [Web SDK](/help/web-sdk/home.md) o [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) o se desideri personalizzare l&#39;esperienza utente in base agli attributi del profilo.

>[!IMPORTANT]
>
>Prima di creare una connessione di personalizzazione personalizzata, leggi la guida su come [attivare i dati sul pubblico nelle destinazioni di personalizzazione Edge](../../ui/activate-edge-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo per un singolo profilo tutti i tipi di pubblico mappati nella destinazione di personalizzazione personalizzata. È possibile impostare diverse destinazioni di personalizzazione personalizzata per diversi [flussi di dati di raccolta dati di Adobe](../../../datastreams/overview.md). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Connettersi alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informazioni sugli ID di stream di dati"
>abstract="Questa opzione determina in quale stream di dati di raccolta dati verranno inclusi i tipi di pubblico nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Prima di poter configurare la destinazione, devi configurare uno stream di dati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=it" text="Scopri come configurare uno stream di dati"

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
* **[!UICONTROL Alias di integrazione]**: questo valore viene inviato all&#39;SDK Web Experience Platform come nome di oggetto JSON.
* **[!UICONTROL ID flusso di dati]**: determina in quale flusso di dati della raccolta dati i tipi di pubblico verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Per ulteriori dettagli, vedere [Configurazione di uno stream di dati](../../../datastreams/overview.md).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Leggi [Attiva profili e tipi di pubblico destinazioni di personalizzazione edge](../../ui/activate-edge-personalization-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

## Dati esportati {#exported-data}

Se utilizzi [Tag in Adobe Experience Platform](../../../tags/home.md) per distribuire Experience Platform Web SDK, utilizza la funzionalità [Invia evento completato](../../../tags/extensions/client/web-sdk/event-types.md) e l&#39;azione del codice personalizzato avrà una variabile `event.destinations` che puoi utilizzare per visualizzare i dati esportati.

Di seguito è riportato un valore di esempio per la variabile `event.destinations`:

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

Se non utilizzi [Tag](/help/tags/home.md) per distribuire Experience Platform Web SDK, utilizza [risposte ai comandi](/help/web-sdk/commands/command-responses.md) per visualizzare i dati esportati.

È possibile analizzare la risposta JSON di Adobe Experience Platform per trovare l’alias di integrazione corrispondente dell’applicazione che si sta integrando con Adobe Experience Platform. Gli ID del pubblico possono essere trasmessi nel codice dell’applicazione come parametri di targeting. Di seguito è riportato un esempio di ciò che dovrebbe apparire specifico per la risposta di destinazione.

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

### Risposta di esempio per [!UICONTROL Personalization personalizzato con attributi]

Quando si utilizza **[!UICONTROL Personalization personalizzato con attributi]**, la risposta API sarà simile a quella riportata di seguito.

La differenza tra **[!UICONTROL Personalization personalizzato con attributi]** e **[!UICONTROL Personalization personalizzato]** è l&#39;inclusione della sezione `attributes` nella risposta API.

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

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](../../../data-governance/home.md).
