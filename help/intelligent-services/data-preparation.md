---
keywords: Experience Platform;home;Intelligent Services;argomenti comuni;servizio intelligente;Intelligent service;Intelligent service
solution: Experience Platform
title: Preparare i dati per l’utilizzo in Intelligent Services
description: Affinché Intelligent Services possa scoprire informazioni provenienti dai dati degli eventi di marketing, i dati devono essere arricchiti semanticamente e mantenuti in una struttura standard. Per ottenere questo risultato, Intelligent Services utilizza gli schemi Experience Data Model (XDM).
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2951'
ht-degree: 0%

---

# Prepara i dati per l&#39;utilizzo in [!DNL Intelligent Services]

Affinché [!DNL Intelligent Services] possa scoprire informazioni dai dati degli eventi di marketing, i dati devono essere arricchiti semanticamente e mantenuti in una struttura standard. [!DNL Intelligent Services] sfrutta [!DNL Experience Data Model] schemi (XDM) per ottenere questo risultato. In particolare, tutti i set di dati utilizzati in [!DNL Intelligent Services] devono essere conformi allo schema XDM Consumer ExperienceEvent (CEE) o utilizzare il connettore Adobe Analytics. Inoltre, IA per l’analisi dei clienti supporta il connettore Adobe Audience Manager.

Questo documento fornisce indicazioni generali sulla mappatura dei dati degli eventi di marketing da più canali allo schema CEE, delineando informazioni su campi importanti all’interno dello schema per aiutarti a determinare come mappare in modo efficace i dati alla relativa struttura. Se prevedi di utilizzare i dati di Adobe Analytics, consulta la sezione per [Preparazione dati di Adobe Analytics](#analytics-data). Se prevedi di utilizzare i dati di Adobe Audience Manager (solo IA per l&#39;analisi dei clienti), consulta la sezione per la [preparazione dei dati di Adobe Audience Manager](#AAM-data).

## Requisiti dei dati

[!DNL Intelligent Services] richiedono quantità diverse di dati storici a seconda dell&#39;obiettivo creato. I dati preparati per **all** [!DNL Intelligent Services] devono comunque includere percorsi/eventi di clienti positivi e negativi. La presenza di eventi negativi e positivi migliora la precisione e l&#39;accuratezza del modello.

Ad esempio, se utilizzi IA per l’analisi dei clienti per prevedere la propensione all’acquisto di un prodotto, il modello di IA per l’analisi dei clienti richiede sia esempi di percorsi di acquisto riusciti che esempi di percorsi non riusciti. Questo perché durante la formazione sul modello, IA per l’analisi dei clienti cerca di capire quali eventi e percorsi portano a un acquisto. Sono incluse anche le azioni intraprese dai clienti che non hanno effettuato l’acquisto, ad esempio da un utente che ha interrotto il percorso per aggiungere un articolo al carrello. Questi clienti possono mostrare comportamenti simili, tuttavia, IA per l’analisi dei clienti può fornire informazioni approfondite e approfondire le principali differenze e i fattori che portano a un punteggio di propensione più elevato. Analogamente, IA per l’attribuzione richiede sia tipi di eventi che percorsi per visualizzare metriche quali l’efficacia dei punti di contatto, i percorsi di conversione principali e i raggruppamenti per posizione dei punti di contatto.

Per ulteriori esempi e informazioni sui requisiti dei dati storici, visita la sezione [Customer AI](./customer-ai/data-requirements.md#data-requirements) o [Attribution AI](./attribution-ai/input-output.md#data-requirements) relativa ai requisiti dei dati storici nella documentazione di input/output.

### Linee guida per l’unione dei dati

È consigliabile unire gli eventi di un utente in un ID comune, quando possibile. Ad esempio, potresti avere dati utente con &quot;id1&quot; su 10 eventi. Successivamente, lo stesso utente ha eliminato l’ID cookie e viene registrato come &quot;id2&quot; nei successivi 20 eventi. Se sai che id1 e id2 corrispondono allo stesso utente, la best practice consiste nell’unire tutti e 30 gli eventi con un ID comune.

Se ciò non è possibile, ogni set di eventi deve essere trattato come un utente diverso durante la creazione dei dati di input del modello. Questo garantisce i migliori risultati durante l’apprendimento dei modelli e il punteggio.

## Riepilogo del flusso di lavoro

Il processo di preparazione varia a seconda che i dati siano memorizzati in Adobe Experience Platform o esternamente. In questa sezione vengono riepilogati i passaggi necessari da effettuare, in uno dei due scenari.

### Preparazione dati esterni

Se i dati sono archiviati all&#39;esterno di Experience Platform, è necessario mappare i dati ai campi richiesti e rilevanti in uno [schema ExperienceEvent consumer](#cee-schema). Questo schema può essere potenziato con gruppi di campi personalizzati per acquisire meglio i dati dei clienti. Una volta eseguito il mapping, puoi creare un set di dati utilizzando lo schema Consumer ExperienceEvent e [acquisire i dati in Experience Platform](../ingestion/home.md). È quindi possibile selezionare il set di dati CEE durante la configurazione di [!DNL Intelligent Service].

A seconda dei [!DNL Intelligent Service] che desideri utilizzare, potrebbero essere necessari campi diversi. È consigliabile aggiungere dati a un campo se si dispone dei dati disponibili. Per ulteriori informazioni sui campi obbligatori, visita la [Guida ai dati di Attribution](./attribution-ai/input-output.md) o [Customer AI](./customer-ai/data-requirements.md).

### Preparazione dei dati di Adobe Analytics {#analytics-data}

Customer AI e Attribution AI supportano in modo nativo i dati di Adobe Analytics. Per utilizzare i dati di Adobe Analytics, segui i passaggi descritti nella documentazione per configurare un [connettore di origine di Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Una volta che il connettore di origine effettua lo streaming dei dati in Experience Platform, puoi selezionare Adobe Analytics come origine dati seguito da un set di dati durante la configurazione dell’istanza. Tutti i gruppi di campi dello schema e i singoli campi richiesti vengono creati automaticamente durante la configurazione della connessione. Non è necessario effettuare operazioni di ETL (Extract, Transform, Load, cioè Estrai, Trasforma, Carica) dei set di dati nel formato CEE.

Se confronti i dati trasmessi tramite il connettore di origine di Adobe Analytics su Adobe Experience Platform con quelli di Adobe Analytics, potresti notare alcune discrepanze. Il connettore Source di Analytics potrebbe rilasciare righe durante la trasformazione in uno schema Experience Data Model (XDM). Ci possono essere diversi motivi per cui l’intera riga non è adatta alla trasformazione, tra cui marche temporali mancanti, ID persona mancanti, ID persona non validi o grandi, valori analitici non validi e altro ancora.

Per ulteriori informazioni ed esempi, consulta la documentazione di [confronto dei dati di Adobe Analytics e Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Questo articolo è progettato per aiutarti a diagnosticare e risolvere tali differenze in modo che tu e il tuo team possiate utilizzare i dati di Adobe Experience Platform per Intelligent Services senza problemi di integrità dei dati.

In Adobe Experience Platform Query Services, esegui i seguenti record totali tra le marche temporali di inizio e fine per query channel.typeAtSource per trovare il conteggio per canali di marketing.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Il connettore Adobe Analytics impiega fino a quattro settimane per eseguire la retrocompilazione dei dati. Se hai impostato di recente una connessione, verifica che il set di dati abbia la lunghezza minima dei dati richiesta per IA per l’attribuzione o per la gestione dei clienti. Controlla le sezioni dei dati storici in [IA per l&#39;analisi dei clienti](./customer-ai/data-requirements.md#data-requirements) o [IA per l&#39;attribuzione](./attribution-ai/input-output.md#data-requirements) e verifica di disporre di dati sufficienti per l&#39;obiettivo di previsione.

### Preparazione dei dati di Adobe Audience Manager (solo IA per l’analisi dei clienti) {#AAM-data}

IA per l’analisi dei clienti supporta in modo nativo i dati di Adobe Audience Manager. Per utilizzare i dati di Audience Manager, segui i passaggi descritti nella documentazione per configurare un [connettore di origine Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Una volta che il connettore di origine effettua lo streaming dei dati in Experience Platform, puoi selezionare Adobe Audience Manager come origine dati seguito da un set di dati durante la configurazione di Customer AI. Tutti i gruppi di campi dello schema e i singoli campi vengono creati automaticamente durante la configurazione della connessione. Non è necessario effettuare operazioni di ETL (Extract, Transform, Load, cioè Estrai, Trasforma, Carica) dei set di dati nel formato CEE.

>[!IMPORTANT]
>
>Se hai impostato di recente un connettore, verifica che il set di dati abbia la lunghezza minima di dati richiesta. Controlla la sezione dei dati storici nella [documentazione di input/output](./customer-ai/data-requirements.md) per IA per l&#39;analisi dei clienti e verifica di disporre di dati sufficienti per l&#39;obiettivo di previsione.

### [!DNL Experience Platform] preparazione dati

Se i dati sono già memorizzati in [!DNL Experience Platform] e non vengono trasmessi tramite i connettori di origine di Adobe Analytics o Adobe Audience Manager (solo IA per l&#39;analisi dei clienti), segui la procedura riportata di seguito. È comunque consigliabile comprendere lo schema CEE.

1. Rivedi la struttura dello schema [Consumer ExperienceEvent](#cee-schema) e determina se i dati possono essere mappati ai relativi campi.
2. Contatta i servizi Adobe Consulting per aiutarti a mappare i tuoi dati sullo schema e a acquisirli in [!DNL Intelligent Services], oppure [segui i passaggi descritti in questa guida](#mapping) se desideri mappare i dati da solo.

## Informazioni sullo schema CEE {#cee-schema}

Lo schema Consumer ExperienceEvent descrive il comportamento di un individuo in relazione a eventi di marketing digitale (web o mobile) e ad attività di e-commerce online o offline. L&#39;utilizzo di questo schema è necessario per [!DNL Intelligent Services] a causa dei campi (colonne) semanticamente ben definiti, evitando nomi sconosciuti che altrimenti renderebbero i dati meno chiari.

Lo schema CEE, come tutti gli schemi ExperienceEvent XDM, acquisisce lo stato del sistema basato su serie temporali quando si è verificato un evento (o un set di eventi), compreso il momento e l’identità del soggetto interessato. Gli Eventi di esperienza sono registri di ciò che è accaduto, e quindi non sono modificabili e rappresentano ciò che è accaduto senza aggregazione o interpretazione.

[!DNL Intelligent Services] utilizza diversi campi chiave all&#39;interno di questo schema per generare informazioni dai dati degli eventi di marketing, che possono essere trovati a livello principale ed espansi per mostrare i relativi sottocampi richiesti.

![Demo dell&#39;espansione dello schema nell&#39;interfaccia utente di Adobe Experience Platform, con visualizzazione dei dettagli di navigazione e dei sottocampi.](./images/data-preparation/schema-expansion.gif)

Come tutti gli schemi XDM, il gruppo di campi dello schema CEE è estensibile. In altre parole, è possibile aggiungere campi aggiuntivi al gruppo di campi CEE e, se necessario, è possibile includere varianti diverse in più schemi.

Un esempio completo del gruppo di campi è disponibile nell&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Inoltre, è possibile visualizzare e copiare il seguente [file JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) per un esempio di come i dati possono essere strutturati in modo da essere conformi allo schema CEE. Per informazioni sui campi chiave descritti nella sezione seguente e su come mappare i propri dati sullo schema, consulta entrambi gli esempi.

## Campi chiave

Ci sono diversi campi chiave all&#39;interno del gruppo di campi CEE che devono essere utilizzati affinché [!DNL Intelligent Services] possa generare informazioni utili. Questa sezione descrive il caso d’uso e i dati previsti per questi campi e fornisce i collegamenti alla documentazione di riferimento per ulteriori esempi.

### Campi obbligatori

Anche se l&#39;utilizzo di tutti i campi chiave è fortemente consigliato, sono presenti due campi **obbligatori** affinché [!DNL Intelligent Services] funzioni:

* [Un campo di identità principale](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obbligatorio solo per IA per l&#39;attribuzione)

#### Identità primaria {#identity}

Uno dei campi dello schema deve essere impostato come campo di identità principale, che consente a [!DNL Intelligent Services] di collegare ogni istanza di dati di serie temporali a una singola persona.

Devi determinare il campo migliore da utilizzare come identità primaria in base all’origine e alla natura dei dati. Un campo di identità deve includere uno spazio dei nomi **identità** che indica il tipo di dati di identità previsti dal campo come valore. Alcuni valori validi dello spazio dei nomi includono:

>[!NOTE]
>
>L’Experience Cloud ID (ECID) è anche noto come MCID e continua a essere utilizzato nei namespace.

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (per Adobe Audience Manager ID)
* &quot;aaid&quot; (per Adobe Analytics ID)

Se non sai quale campo utilizzare come identità principale, contatta i servizi Adobe Consulting per determinare la soluzione migliore. Se non è impostata un’identità primaria, l’applicazione Intelligent Service utilizza il seguente comportamento predefinito:

| Predefinito | IA per l’attribuzione | IA per l’analisi dei clienti |
| --- | --- | --- |
| Colonna identità | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Per impostare un&#39;identità primaria, passare allo schema dalla scheda **[!UICONTROL Schemi]** e selezionare il collegamento ipertestuale del nome dello schema per aprire **[!DNL Schema Editor]**.

![Navigazione allo schema nell&#39;interfaccia utente di Adobe Experience Platform.](./images/data-preparation/navigate_schema.png)

Quindi, passa al campo che desideri impostare come identità principale e selezionalo. Viene visualizzato il menu **[!UICONTROL Proprietà campo]** per tale campo.

![Processo di selezione del campo desiderato nell&#39;interfaccia utente di Adobe Experience Platform.](./images/data-preparation/find_field.png)

Nel menu **[!UICONTROL Proprietà campo]**, scorri verso il basso fino a trovare la casella di controllo **[!UICONTROL Identità]**. Dopo aver selezionato la casella, viene visualizzata l&#39;opzione per impostare l&#39;identità selezionata come **[!UICONTROL identità primaria]**. Seleziona anche questa casella.

![Casella di controllo per impostare l&#39;identità primaria nell&#39;interfaccia utente di Adobe Experience Platform.](./images/data-preparation/set_primary_identity.png)

Successivamente, devi fornire uno spazio dei nomi **[!UICONTROL Identity]** dall&#39;elenco di spazi dei nomi predefiniti nel menu a discesa. In questo esempio, lo spazio dei nomi ECID è selezionato poiché è in uso un ID Adobe Audience Manager `mcid.id`. Seleziona **[!UICONTROL Applica]** per confermare gli aggiornamenti, quindi seleziona **[!UICONTROL Salva]** nell&#39;angolo in alto a destra per salvare le modifiche allo schema.

![Menu a discesa che mostra la selezione dello spazio dei nomi ECID nell&#39;interfaccia utente di Adobe Experience Platform.](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Questo campo rappresenta il datetime in cui si è verificato l&#39;evento. Questo valore deve essere fornito come stringa, in base allo standard ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Questo campo è obbligatorio solo quando si utilizza IA per l’attribuzione.

Questo campo rappresenta il canale di marketing relativo all’ExperienceEvent. Il campo include informazioni sul tipo di canale, il tipo di supporto e il tipo di posizione.

![Diagramma che mostra la struttura del campo xdm:channel, inclusi i sottocampi type, mediaType e mediaAction.](./images/data-preparation/channel.png)

**Esempio di schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Per informazioni complete su ciascuno dei sottocampi richiesti per `xdm:channel`, fare riferimento alle specifiche dello [schema del canale esperienza](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Per alcuni mapping di esempio, vedere la [tabella seguente](#example-channels).

#### Esempi di mappature dei canali {#example-channels}

Nella tabella seguente vengono forniti alcuni esempi di canali di marketing mappati allo schema `xdm:channel`:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Ricerca pagata | https:/<span>/ns.adobe.com/xdm/channel-types/search | pagato | clic |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | guadagnato | clic |
| Visualizzazione | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagato | clic |
| E-mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | pagato | clic |
| Referente interno | https:/<span>/ns.adobe.com/xdm/channel-types/direct | di proprietà | clic |
| Visualizza viewThrough | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagato | impressioni |
| Reindirizzamento codice QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | di proprietà | clic |
| Dispositivi mobili | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | di proprietà | clic |

### Campi consigliati

I restanti campi chiave sono descritti in questa sezione. Anche se questi campi non sono necessariamente necessari per il funzionamento di [!DNL Intelligent Services], si consiglia vivamente di utilizzarne il maggior numero possibile per ottenere informazioni più approfondite.

#### xdm:productListItems

Questo campo è un array di articoli che rappresentano i prodotti selezionati da un cliente, inclusi SKU prodotto, nome, prezzo e quantità.

![Il campo xdm:productListItems, inclusi i sottocampi SKU, name, currencyCode, quantity e priceTotal.](./images/data-preparation/productListItems.png)

**Esempio di schema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Per informazioni complete su ciascuno dei sottocampi richiesti per `xdm:productListItems`, fare riferimento alle specifiche dello [schema dei dettagli di e-commerce](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Questo campo contiene informazioni specifiche di Commerce su ExperienceEvent, tra cui il numero dell’ordine di acquisto e le informazioni sul pagamento.

![Struttura del campo xdm:commerce, inclusi i sottocampi quali ordine, acquisti e pagamenti.](./images/data-preparation/commerce.png)

**Esempio di schema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Per informazioni complete su ciascuno dei sottocampi richiesti per `xdm:commerce`, fare riferimento alle specifiche dello [schema dei dettagli di e-commerce](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Questo campo rappresenta i dettagli web relativi all’ExperienceEvent, ad esempio l’interazione, i dettagli della pagina e il referente.

![Il campo xdm:web, inclusi i sottocampi come webPageDetails e webReferrer.](./images/data-preparation/web.png)

**Esempio di schema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Per informazioni complete su ciascuno dei sottocampi richiesti per `xdm:productListItems`, fare riferimento alle specifiche dello schema dei dettagli Web di [ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md).

#### xdm:marketing

Questo campo contiene informazioni relative alle attività di marketing che sono attive con il punto di contatto.

![Struttura del campo xdm:marketing, inclusi i sottocampi trackingCode, campaignGroup e campaignName.](./images/data-preparation/marketing.png)

**Esempio di schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, fare riferimento alle specifiche [sechma di marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Mappatura e acquisizione dei dati {#mapping}

Dopo aver stabilito se i dati degli eventi di marketing possono essere mappati sullo schema CEE, il passaggio successivo consiste nel determinare quali dati inserire in [!DNL Intelligent Services]. Tutti i dati storici utilizzati in [!DNL Intelligent Services] devono rientrare nell&#39;intervallo di tempo minimo di quattro mesi di dati più il numero di giorni previsti come periodo di lookback.

Dopo aver stabilito l’intervallo di dati da inviare, contatta i servizi Adobe Consulting per aiutarti a mappare i dati sullo schema e a acquisirli nel servizio.

Se disponi di un abbonamento a [!DNL Adobe Experience Platform] e desideri mappare e acquisire i dati autonomamente, segui i passaggi descritti nella sezione seguente.

### Utilizzo di Adobe Experience Platform

>[!NOTE]
>
>I passaggi seguenti richiedono un abbonamento ad Experience Platform. Se non hai accesso ad Experience Platform, passa alla sezione [passaggi successivi](#next-steps).

Questa sezione descrive il flusso di lavoro per la mappatura e l&#39;acquisizione di dati in Experience Platform da utilizzare in [!DNL Intelligent Services], inclusi i collegamenti alle esercitazioni per i passaggi dettagliati.

#### Creare uno schema e un set di dati CEE

Quando sei pronto per iniziare a preparare i dati per l’acquisizione, il primo passaggio consiste nel creare un nuovo schema XDM che utilizza il gruppo di campi CEE. Le seguenti esercitazioni descrivono come creare un nuovo schema nell’interfaccia utente o nell’API:

* [Creare uno schema nell’interfaccia utente](../xdm/tutorials/create-schema-ui.md)
* [Creare uno schema nell’API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>I tutorial di cui sopra seguono un flusso di lavoro generico per la creazione di uno schema. Quando si sceglie una classe per lo schema, è necessario utilizzare la **classe ExperienceEvent XDM**. Una volta scelta questa classe, è possibile aggiungere il gruppo di campi CEE allo schema.

Dopo aver aggiunto il gruppo di campi CEE allo schema, è possibile aggiungere altri gruppi di campi in base alle esigenze per campi aggiuntivi all’interno dei dati.

Dopo aver creato e salvato lo schema, puoi creare un nuovo set di dati basato su tale schema. Le seguenti esercitazioni descrivono come creare un nuovo set di dati nell’interfaccia utente o nell’API:

* [Crea un set di dati nell&#39;interfaccia utente](../catalog/datasets/user-guide.md#create) (segui il flusso di lavoro per utilizzare uno schema esistente)
* [Creare un set di dati nell’API](../catalog/datasets/create.md)

Una volta creato il set di dati, è possibile trovarlo nell&#39;interfaccia utente di Experience Platform all&#39;interno dell&#39;area di lavoro **[!UICONTROL Set di dati]**.

![](images/data-preparation/dataset-location.png)

#### Aggiungere campi di identità al set di dati

Se si importano dati da [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] o da un&#39;altra origine esterna, è possibile impostare un campo schema come campo di identità. Per impostare un campo schema come campo identità, visualizzare la sezione relativa all&#39;impostazione dei campi identità nell&#39;esercitazione dell&#39;[interfaccia utente](../xdm/tutorials/create-schema-ui.md#identity-field) o nell&#39;esercitazione dell&#39;[API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) per la creazione di uno schema.

Se acquisisci dati da un file CSV locale, puoi passare alla sezione successiva sulla [mappatura e acquisizione dei dati](#ingest).

#### Mappare e acquisire dati {#ingest}

Dopo aver creato uno schema CEE e un set di dati, puoi iniziare a mappare le tabelle di dati sullo schema e acquisire tali dati in Experience Platform. Consulta l&#39;esercitazione su [mappatura di un file CSV a uno schema XDM](../ingestion/tutorials/map-csv/overview.md) per i passaggi su come eseguire questa operazione nell&#39;interfaccia utente. Puoi utilizzare il seguente [file JSON di esempio](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) per testare il processo di acquisizione prima di utilizzare i tuoi dati.

Una volta popolato un set di dati, è possibile utilizzarlo per acquisire file di dati aggiuntivi.

Se i dati sono archiviati in un&#39;applicazione di terze parti supportata, puoi anche scegliere di creare un [connettore di origine](../sources/home.md) per acquisire i dati degli eventi di marketing in [!DNL Experience Platform] in tempo reale.

## Passaggi successivi {#next-steps}

Questo documento fornisce indicazioni generali sulla preparazione dei dati da utilizzare in [!DNL Intelligent Services]. Se hai bisogno di consulenza aggiuntiva in base al tuo caso d’uso, contatta il supporto Adobe Consulting.

Dopo aver popolato correttamente un set di dati con i dati sull&#39;esperienza del cliente, puoi utilizzare [!DNL Intelligent Services] per generare approfondimenti. Per iniziare, consulta i seguenti documenti:

* [Panoramica di Attribution AI](./attribution-ai/overview.md)
* [Panoramica di Customer AI](./customer-ai/overview.md)
