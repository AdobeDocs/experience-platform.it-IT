---
keywords: Experience Platform;casa;servizi intelligenti;argomenti comuni;servizio intelligente;servizio intelligente
solution: Experience Platform
title: Preparare i dati da utilizzare nei servizi intelligenti
topic-legacy: Intelligent Services
description: Affinché i servizi intelligenti possano scoprire informazioni dai dati degli eventi di marketing, i dati devono essere arricchiti e mantenuti in una struttura standard in modo semantico. Per ottenere questo risultato, i servizi intelligenti utilizzano gli schemi Experience Data Model (XDM).
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '2936'
ht-degree: 0%

---

# Preparare i dati da utilizzare in [!DNL Intelligent Services]

Per [!DNL Intelligent Services] per scoprire informazioni dai dati degli eventi di marketing, i dati devono essere arricchiti e mantenuti in una struttura standard in modo semantico. [!DNL Intelligent Services] sfruttare [!DNL Experience Data Model] (XDM) schemi per ottenere questo risultato. In particolare, tutti i set di dati utilizzati in [!DNL Intelligent Services] deve essere conforme allo schema XDM di Consumer ExperienceEvent (CEE) o utilizzare il connettore Adobe Analytics. Inoltre, Customer AI supporta il connettore Adobe Audience Manager.

Questo documento fornisce indicazioni generali sulla mappatura dei dati degli eventi di marketing da più canali allo schema CEE, delineando informazioni su campi importanti all&#39;interno dello schema per aiutarti a determinare come mappare efficacemente i dati alla struttura. Se prevedi di utilizzare i dati di Adobe Analytics, visualizza la sezione per [Preparazione dei dati di Adobe Analytics](#analytics-data). Se prevedi di utilizzare i dati di Adobe Audience Manager (solo Customer AI), consulta la sezione per [Preparazione dei dati di Adobe Audience Manager](#AAM-data).

## Requisiti dei dati

[!DNL Intelligent Services] richiedono quantità diverse di dati storici a seconda dell’obiettivo creato. Indipendentemente dai dati per i quali ti prepari **tutto** [!DNL Intelligent Services] devono includere percorsi/eventi cliente positivi e negativi. La presenza di eventi negativi e positivi migliora la precisione e l&#39;accuratezza del modello.

Ad esempio, se utilizzi Customer AI per prevedere la propensione all’acquisto di un prodotto, il modello per Customer AI richiede sia esempi di percorsi di acquisto riusciti sia esempi di percorsi di acquisto non riusciti. Questo perché durante la formazione sul modello, Customer AI cerca di capire quali eventi e percorsi portano ad un acquisto. Ciò include anche le azioni dei clienti che non hanno acquistato, ad esempio una persona che ha interrotto il percorso aggiungendo un articolo al carrello. Tuttavia, questi clienti possono mostrare comportamenti simili, Customer AI può fornire informazioni approfondite ed approfondire le principali differenze e fattori che portano a un punteggio di propensione più elevato. Allo stesso modo, Attribution AI richiede sia tipi di eventi che percorsi per visualizzare metriche quali l’efficacia dei punti di contatto, i migliori percorsi di conversione e le suddivisioni per posizione dei punti di contatto.

Per ulteriori esempi e informazioni sui requisiti storici dei dati, visita il [Customer AI](./customer-ai/input-output.md#data-requirements) o [Attribution AI](./attribution-ai/input-output.md#data-requirements) la sezione sui requisiti dei dati storici nella documentazione di input/output.

### Linee guida per l’unione dei dati

È consigliabile unire gli eventi di un utente in un ID comune quando possibile. Ad esempio, puoi avere dati utente con &quot;id1&quot; in 10 eventi. Successivamente, lo stesso utente ha eliminato l&#39;id cookie e viene registrato come &quot;id2&quot; nei successivi 20 eventi. Se sai che l’id1 e l’id2 corrispondono allo stesso utente, la best practice consiste nell’unire tutti e 30 gli eventi con un ID comune.

Se ciò non è possibile, è necessario trattare ogni set di eventi come un utente diverso durante la creazione dei dati di input del modello. Questo garantisce i migliori risultati durante l&#39;addestramento e il punteggio del modello.

## Riepilogo del flusso di lavoro

Il processo di preparazione varia a seconda che i dati siano memorizzati in Adobe Experience Platform o esternamente. In questa sezione vengono riepilogati i passaggi necessari, in base a entrambi gli scenari.

### Preparazione dei dati esterni

Se i dati sono memorizzati al di fuori dell’Experience Platform, devi mappare i tuoi dati sui campi obbligatori e rilevanti in un [Schema di Consumer ExperienceEvent](#cee-schema). Questo schema può essere migliorato con gruppi di campi personalizzati per acquisire meglio i dati dei clienti. Una volta mappato, puoi creare un set di dati utilizzando lo schema Consumer ExperienceEvent e [Inserire i dati in Platform](../ingestion/home.md). È quindi possibile selezionare il set di dati CEE al momento della configurazione di un [!DNL Intelligent Service].

A seconda del [!DNL Intelligent Service] si desidera utilizzare campi diversi. È consigliabile aggiungere dati a un campo se i dati sono disponibili. Per ulteriori informazioni sui campi obbligatori, visita il [Attribution AI](./attribution-ai/input-output.md) o [Customer AI](./customer-ai/input-output.md) guida di ingresso/uscita.

### Preparazione dei dati di Adobe Analytics {#analytics-data}

Customer AI e Attribution AI supportano i dati di Adobe Analytics in modo nativo. Per utilizzare i dati di Adobe Analytics, segui i passaggi descritti nella documentazione per configurare un [Connettore sorgente di Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Una volta che il connettore di origine trasmette i dati in Experience Platform, puoi selezionare Adobe Analytics come origine dati seguita da un set di dati durante la configurazione dell’istanza. Durante la configurazione della connessione vengono creati automaticamente tutti i gruppi di campi dello schema richiesti e i singoli campi. Non è necessario ETL (Extract, Transform, Load) dei set di dati nel formato CEE.

Se confronti i dati che scorrono attraverso il connettore di origine Adobe Analytics su Adobe Experience Platform con quelli di Adobe Analytics, potresti notare alcune discrepanze. Il connettore di origine di Analytics potrebbe rilasciare righe durante la trasformazione in uno schema Experience Data Model (XDM). Ci possono essere diversi motivi per cui l’intera riga non è adatta alla trasformazione, tra cui marche temporali mancanti, ID persona mancanti, ID persona non validi o di grandi dimensioni, valori analitici non validi e altro ancora.

Per ulteriori informazioni ed esempi, visita la documentazione di [confronto tra i dati di Adobe Analytics e Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Questo articolo è progettato per aiutarti a diagnosticare e risolvere tali differenze in modo che tu e il tuo team possiate utilizzare i dati di Adobe Experience Platform per i servizi intelligenti senza problemi per motivi di integrità dei dati.

In Adobe Experience Platform Query Services, esegui la seguente query Total Records tra l’inizio e la fine della marca temporale per channel.typeAtSource per trovare il conteggio per canali di marketing.

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
>Il connettore Adobe Analytics impiega fino a quattro settimane per eseguire il backfill dei dati. Se hai recentemente configurato una connessione, devi verificare che il set di dati abbia la lunghezza minima dei dati richiesti per Cliente o Attribution AI. Controlla le sezioni dei dati storici in [Customer AI](./customer-ai/input-output.md#data-requirements) o [Attribution AI](./attribution-ai/input-output.md#data-requirements)e verifica di disporre di dati sufficienti per l&#39;obiettivo di previsione.

### Preparazione dei dati Adobe Audience Manager (solo Customer AI) {#AAM-data}

Customer AI supporta in modo nativo i dati di Adobe Audience Manager. Per utilizzare i dati di Audience Manager, segui i passaggi descritti nella documentazione per impostare un [Connettore sorgente di Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Una volta che il connettore di origine trasmette i dati in Experience Platform, puoi selezionare Adobe Audience Manager come origine dati seguita da un set di dati durante la configurazione di Customer AI. Durante la configurazione della connessione vengono creati automaticamente tutti i gruppi di campi dello schema e i singoli campi. Non è necessario ETL (Extract, Transform, Load) dei set di dati nel formato CEE.

>[!IMPORTANT]
>
>Se recentemente hai impostato un connettore, devi verificare che il set di dati abbia la lunghezza minima necessaria per i dati. Consulta la sezione relativa ai dati storici nel [documentazione di ingresso/uscita](./customer-ai/input-output.md) per Customer AI e verifica di disporre di dati sufficienti per l’obiettivo di previsione.

### [!DNL Experience Platform] preparazione dei dati

Se i dati sono già memorizzati in [!DNL Platform] e senza lo streaming attraverso i connettori sorgente Adobe Analytics o Adobe Audience Manager (solo Customer AI), segui la procedura seguente. È comunque consigliabile comprendere lo schema CEE.

1. Rivedere la struttura del [Schema di Consumer ExperienceEvent](#cee-schema) e determinare se i dati possono essere mappati ai relativi campi.
2. Contatta Adobe Consulting Services per facilitare la mappatura dei dati sullo schema e il loro inserimento in [!DNL Intelligent Services]oppure [segui i passaggi descritti in questa guida](#mapping) se desideri mappare i dati da solo.

## Informazioni sullo schema CEE {#cee-schema}

Lo schema Consumer ExperienceEvent descrive il comportamento di un individuo in relazione agli eventi di marketing digitale (web o mobile) nonché alle attività di e-commerce online o offline. L&#39;utilizzo di questo schema è necessario per [!DNL Intelligent Services] a causa dei suoi campi semanticamente ben definiti (colonne), evitando nomi sconosciuti che altrimenti renderebbero i dati meno chiari.

Lo schema CEE, come tutti gli schemi ExperienceEvent XDM, acquisisce lo stato del sistema basato su serie temporali quando si verifica un evento (o un set di eventi), incluso il punto nel tempo e l&#39;identità dell&#39;oggetto coinvolto. Gli eventi di esperienza sono registrazioni di fatti di ciò che è accaduto, e quindi sono immutabili e rappresentano ciò che è accaduto senza aggregazione o interpretazione.

[!DNL Intelligent Services] utilizza diversi campi chiave all’interno di questo schema per generare informazioni dai dati degli eventi di marketing, che possono essere trovati a livello principale ed espansi per mostrare i relativi sottocampi richiesti.

![](./images/data-preparation/schema-expansion.gif)

Come tutti gli schemi XDM, il gruppo di campi dello schema CEE è estensibile. In altre parole, è possibile aggiungere campi aggiuntivi al gruppo di campi CEE e, se necessario, includere varianti diverse in più schemi.

Un esempio completo del gruppo di campi è disponibile nella sezione [archivio XDM pubblico](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Inoltre, puoi visualizzare e copiare quanto segue [File JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) per un esempio di come strutturare i dati in modo da rispettare lo schema CEE. Per determinare come mappare i dati personalizzati sullo schema, fai riferimento a entrambi gli esempi mentre apprendi i campi chiave descritti nella sezione seguente.

## Campi chiave

Ci sono diversi campi chiave all&#39;interno del gruppo di campi CEE che devono essere utilizzati per [!DNL Intelligent Services] per generare informazioni utili. Questa sezione descrive il caso d’uso e i dati previsti per questi campi e fornisce collegamenti alla documentazione di riferimento per ulteriori esempi.

### Campi obbligatori

Sebbene sia vivamente consigliato l’utilizzo di tutti i campi chiave, esistono due campi **obbligatorio** per [!DNL Intelligent Services] per lavorare:

* [Un campo di identità principale](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obbligatorio solo per le Attribution AI)

#### Identità principale {#identity}

Uno dei campi dello schema deve essere impostato come campo di identità principale, che consente [!DNL Intelligent Services] collegare ogni istanza di dati relativi a serie temporali a una singola persona.

È necessario determinare il campo migliore da utilizzare come identità principale in base all’origine e alla natura dei dati. Un campo di identità deve includere un **spazio dei nomi identità** indica il tipo di dati di identità che il campo prevede come valore. Alcuni valori di spazio dei nomi validi includono:

>[!NOTE]
>
>L’ID Experience Cloud (ECID) è noto anche come MCID e continua a essere utilizzato nei namespace.

* &quot;e-mail&quot;
* &quot;telefono&quot;
* &quot;mcid&quot; (per Adobe Audience Manager ID)
* &quot;aaid&quot; (per Adobe Analytics ID)

Se non sei sicuro di quale campo utilizzare come identità principale, contatta Adobe Consulting Services per determinare la soluzione migliore. Se non è impostata un&#39;identità primaria, l&#39;applicazione Intelligent Service utilizza il seguente comportamento predefinito:

| Impostazione predefinita | IA per l’attribuzione | Customer AI |
| --- | --- | --- |
| Colonna identità | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Per impostare un&#39;identità principale, passa allo schema dal **[!UICONTROL Schemi]** e selezionare il collegamento ipertestuale del nome dello schema per aprire **[!DNL Schema Editor]**.

![Passa allo schema](./images/data-preparation/navigate_schema.png)

Quindi, accedi al campo che desideri utilizzare come identità principale e selezionalo. La **[!UICONTROL Proprietà campo]** viene visualizzato il menu corrispondente.

![Selezionare il campo](./images/data-preparation/find_field.png)

In **[!UICONTROL Proprietà campo]** scorri verso il basso fino a trovare il menu **[!UICONTROL Identità]** casella di controllo. Dopo aver selezionato la casella, l&#39;opzione per impostare l&#39;identità selezionata come **[!UICONTROL Identità principale]** appare. Seleziona anche questa casella.

![Seleziona casella di controllo](./images/data-preparation/set_primary_identity.png)

Successivamente, devi fornire un **[!UICONTROL Spazio dei nomi identità]** dall’elenco dei namespace predefiniti nel menu a discesa. In questo esempio, lo spazio dei nomi ECID viene selezionato a partire da un Adobe Audience Manager ID `mcid.id` viene utilizzato. Seleziona **[!UICONTROL Applica]** per confermare gli aggiornamenti, seleziona **[!UICONTROL Salva]** nell’angolo in alto a destra per salvare le modifiche allo schema.

![Salva le modifiche](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Questo campo rappresenta il datetime in cui si è verificato l&#39;evento. Questo valore deve essere fornito come stringa, secondo lo standard ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Questo campo è obbligatorio solo quando si utilizza Attribution AI.

Questo campo rappresenta il canale di marketing correlato all’ExperienceEvent. Il campo include informazioni sul tipo di canale, il tipo di supporto e il tipo di posizione.

![](./images/data-preparation/channel.png)

**Esempio di schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:channel`, si prega di fare riferimento al [schema del canale esperienza](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) specifiche Per alcuni esempi di mappature, consulta la sezione [tabella seguente](#example-channels).

#### Esempio di mappature dei canali {#example-channels}

Nella tabella seguente sono riportati alcuni esempi di canali di marketing mappati a `xdm:channel` schema:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Ricerca pagata | https:/<span>/ns.adobe.com/xdm/channel-types/search | pagato | click |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | guadagnato | click |
| Visualizzazione | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagato | click |
| E-mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | pagato | click |
| Referrer interno | https:/<span>/ns.adobe.com/xdm/channel-types/direct | di proprietà | click |
| Visualizza visualizzazione passante | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagato | impression |
| Reindirizzamento del codice QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | di proprietà | click |
| Dispositivi mobili | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | di proprietà | click |

### Campi consigliati

Il resto dei campi chiave è descritto in questa sezione. Anche se questi campi non sono necessariamente necessari per [!DNL Intelligent Services] per lavorare, si consiglia vivamente di utilizzarne il maggior numero possibile per ottenere informazioni più approfondite.

#### xdm:productListItems

Questo campo è un array di articoli che rappresentano i prodotti selezionati da un cliente, inclusi SKU del prodotto, nome, prezzo e quantità.

![](./images/data-preparation/productListItems.png)

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

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, si prega di fare riferimento al [schema dettagli commercio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) specifiche

#### xdm:commerce

Questo campo contiene informazioni specifiche sull&#39;ExperienceEvent per l&#39;e-commerce, tra cui il numero dell&#39;ordine di acquisto e le informazioni sul pagamento.

![](./images/data-preparation/commerce.png)

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

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:commerce`, si prega di fare riferimento al [schema dettagli commercio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) specifiche

#### xdm:web

Questo campo rappresenta i dettagli web relativi all’ExperienceEvent, ad esempio l’interazione, i dettagli della pagina e il referente.

![](./images/data-preparation/web.png)

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

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, si prega di fare riferimento al [Schema dei dettagli web di ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) specifiche

#### xdm:marketing

Questo campo contiene informazioni relative alle attività di marketing attive con il punto di contatto.

![](./images/data-preparation/marketing.png)

**Esempio di schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, si prega di fare riferimento al [sechma di marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) specifiche

## Mappatura e acquisizione dei dati {#mapping}

Una volta determinato se i dati degli eventi di marketing possono essere mappati sullo schema CEE, il passaggio successivo consiste nel determinare in quali dati portare [!DNL Intelligent Services]. Tutti i dati storici utilizzati in [!DNL Intelligent Services] devono rientrare nell’intervallo di tempo minimo di quattro mesi di dati, più il numero di giorni previsti come periodo di lookback.

Dopo aver deciso l’intervallo di dati da inviare, contatta Adobe Consulting Services per facilitare la mappatura dei dati sullo schema e il loro inserimento nel servizio.

Se hai un [!DNL Adobe Experience Platform] l’abbonamento e desideri mappare e acquisire i dati da solo, segui i passaggi descritti nella sezione seguente.

### Utilizzo di Adobe Experience Platform

>[!NOTE]
>
>I passaggi seguenti richiedono un abbonamento ad Experience Platform. Se non hai accesso a Platform, passa alla [passaggi successivi](#next-steps) sezione .

Questa sezione delinea il flusso di lavoro per la mappatura e l’acquisizione dei dati in Experience Platform da utilizzare in [!DNL Intelligent Services], compresi collegamenti a esercitazioni per passaggi dettagliati.

#### Creare uno schema e un set di dati CEE

Quando sei pronto a preparare i dati per l’acquisizione, il primo passo è creare un nuovo schema XDM che utilizzi il gruppo di campi CEE. Le seguenti esercitazioni illustrano il processo di creazione di un nuovo schema nell’interfaccia utente o nell’API:

* [Creare uno schema nell’interfaccia utente](../xdm/tutorials/create-schema-ui.md)
* [Creare uno schema nell’API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Le esercitazioni di cui sopra seguono un flusso di lavoro generico per la creazione di uno schema. Quando si sceglie una classe per lo schema, è necessario utilizzare il **Classe ExperienceEvent XDM**. Una volta selezionata questa classe, è possibile aggiungere il gruppo di campi CEE allo schema.

Dopo aver aggiunto il gruppo di campi CEE allo schema, è possibile aggiungere altri gruppi di campi come necessario per ulteriori campi all’interno dei dati.

Dopo aver creato e salvato lo schema, puoi creare un nuovo set di dati basato su tale schema. Le seguenti esercitazioni illustrano il processo di creazione di un nuovo set di dati nell’interfaccia utente o nell’API:

* [Creare un set di dati nell’interfaccia utente](../catalog/datasets/user-guide.md#create) (Segui il flusso di lavoro per utilizzare uno schema esistente)
* [Creare un set di dati nell’API](../catalog/datasets/create.md)

Dopo la creazione del set di dati, puoi trovarlo nell’interfaccia utente di Platform all’interno della **[!UICONTROL Set di dati]** workspace.

![](images/data-preparation/dataset-location.png)

#### Aggiungere campi di identità al set di dati

Se inserisci dati da [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]oppure un&#39;altra origine esterna, puoi impostare un campo schema come campo di identità. Per impostare un campo schema come campo di identità, visualizzare la sezione relativa all’impostazione dei campi di identità all’interno di [Esercitazione sull’interfaccia utente](../xdm/tutorials/create-schema-ui.md#identity-field) o [Esercitazione API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) per la creazione di uno schema.

Se acquisisci dati da un file CSV locale, puoi passare alla sezione successiva in [mappatura e acquisizione dei dati](#ingest).

#### Mappare e acquisire dati {#ingest}

Dopo aver creato uno schema e un set di dati CEE, puoi iniziare a mappare le tabelle di dati sullo schema e a trasferirli in Platform. Guarda l’esercitazione su [mappatura di un file CSV su uno schema XDM](../ingestion/tutorials/map-a-csv-file.md) per informazioni su come eseguire questa operazione nell’interfaccia utente di . Puoi utilizzare i seguenti [file JSON di esempio](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) per testare il processo di acquisizione prima di utilizzare i tuoi dati.

Una volta compilato un set di dati, lo stesso set di dati può essere utilizzato per acquisire file di dati aggiuntivi.

Se i dati vengono memorizzati in un’applicazione di terze parti supportata, puoi anche scegliere di creare un [connettore di origine](../sources/home.md) per immettere i dati degli eventi di marketing in [!DNL Platform] in tempo reale.

## Passaggi successivi {#next-steps}

Questo documento fornisce indicazioni generali sulla preparazione dei dati da utilizzare in [!DNL Intelligent Services]. Se hai bisogno di consulenza aggiuntiva in base al tuo caso d’uso, contatta l’Assistenza Consultiva Adobe.

Dopo aver popolato correttamente un set di dati con i dati sulla customer experience, puoi utilizzare [!DNL Intelligent Services] per generare informazioni. Per iniziare, consulta i seguenti documenti:

* [Panoramica di Attribution AI](./attribution-ai/overview.md)
* [Panoramica di Customer AI](./customer-ai/overview.md)
