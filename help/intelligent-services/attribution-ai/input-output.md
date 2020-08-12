---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform
title: ' ingresso e uscita Attribution AI'
topic: Input and Output data for Attribution AI
description: Il seguente documento illustra i diversi input e output utilizzati nelle Attribution AI .
translation-type: tm+mt
source-git-commit: 2b51569a4c3dd9863edb6831bd182a7fa9d1d891
workflow-type: tm+mt
source-wordcount: '2067'
ht-degree: 3%

---


# [!DNL Attribution AI] ingresso e uscita

Il documento seguente illustra i diversi input e output utilizzati in [!DNL Attribution AI].

## [!DNL Attribution AI] dati di input

[!DNL Attribution AI] utilizza [!DNL Consumer Experience Event] i dati per calcolare i punteggi algoritmici. Per ulteriori informazioni su [!DNL Consumer Experience Event], consulta la sezione [Preparare i dati per l&#39;utilizzo nella documentazione](../data-preparation.md)dei servizi intelligenti.

Non tutte le colonne dello schema [!DNL Consumer Experience Event] (CEE) sono obbligatorie per  Attribution AI.

>[!NOTE]
>
> Le seguenti 9 colonne sono obbligatorie. Le colonne aggiuntive sono facoltative ma consigliate/necessarie se si desidera utilizzare gli stessi dati per altre soluzioni di Adobe  come [!DNL Customer AI] e [!DNL Journey AI].

| Colonne obbligatorie | Necessario per |
| --- | --- |
| Campo identità principale | Punto di contatto / Conversione |
| Timestamp | Punto di contatto / Conversione |
| Channel._type | Punto di contatto |
| Channel.mediaAction | Punto di contatto |
| Channel.mediaType | Punto di contatto |
| Marketing.trackingCode | Punto di contatto |
| Marketing.campaignname | Punto di contatto |
| Marketing.campaigngroup | Punto di contatto |
| Commercio | Conversione |

In genere, l&#39;attribuzione viene eseguita su colonne di conversione quali ordine, acquisti e pagamenti in &quot;commerce&quot;. Le colonne &quot;canale&quot; e &quot;marketing&quot; sono consigliate per definire punti di contatto per una buona conoscenza. Tuttavia, puoi includere qualsiasi altra colonna aggiuntiva insieme alle colonne precedenti da configurare come definizione di conversione o punto di contatto.

Le colonne riportate di seguito non sono obbligatorie, ma si consiglia di includerle nello schema CEE se si dispone delle informazioni disponibili.

**Altre colonne consigliate:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Dati storici

>[!IMPORTANT]
>
> La quantità minima di dati necessaria per il funzionamento  Attribution AI è la seguente:
> - È necessario fornire almeno 3 mesi (90 giorni) di dati per eseguire un buon modello.
> - Hai bisogno di almeno 1000 conversioni.


 Attribution AI richiede dati storici come input per la formazione dei modelli. La durata dei dati richiesti è determinata principalmente da due fattori chiave: finestra di formazione e finestra di look-back. L&#39;input con finestre di formazione più brevi è più sensibile alle tendenze recenti, mentre le finestre di formazione più lunghe consentono di produrre modelli più stabili e precisi. È importante modellare l&#39;obiettivo con dati storici che meglio rappresentano gli obiettivi aziendali.

La configurazione della finestra di [formazione](./user-guide.md#training-window) filtra gli eventi di conversione impostati per essere inclusi nella formazione del modello in base al tempo di occorrenza. Attualmente, la finestra di formazione minima è di 1 quarto (90 giorni). La finestra [di](./user-guide.md#lookback-window) lookback fornisce un intervallo di tempo che indica quanti giorni prima dei punti di contatto dell&#39;evento di conversione relativi a questo evento di conversione devono essere inclusi. Questi due concetti insieme determinano la quantità di dati di input (misurati in giorni) necessaria per un&#39;applicazione.

Per impostazione predefinita,  Attribution AI definisce la finestra di formazione come l’ultima finestra di 2 trimestri (6 mesi) e la finestra di lookback come 56 giorni. In altre parole, il modello terrà conto di tutti gli eventi di conversione definiti che si sono verificati negli ultimi 2 trimestri e cercherà tutti i punti di contatto che si sono verificati entro 56 giorni prima degli eventi di conversione associati.

**Formula**:

Lunghezza minima dei dati richiesti = finestra di formazione + finestra di lookback

>[!TIP]
> La lunghezza minima dei dati richiesti per un&#39;applicazione con configurazioni predefinite è: 2 trimestri (180 giorni) + 56 giorni = 236 giorni.

Esempio :

- Si desidera attribuire gli eventi di conversione che si sono verificati negli ultimi 90 giorni (3 mesi) e tenere traccia di tutti i punti di contatto che si sono verificati entro 4 settimane prima dell&#39;evento di conversione. La durata dei dati di input dovrebbe estendersi negli ultimi 90 giorni + 28 giorni (4 settimane). La finestra di formazione è di 90 giorni e la finestra di lookback è di 28 giorni per un totale di 118 giorni.

## Dati di output Attribution AI 

 Attribution AI produce i seguenti output:

- [Punteggi granulari grezzi](#raw-granular-scores)
- [Punteggi aggregati](#aggregated-attribution-scores)

**Esempio di schema di output:**

![](./images/input-output/schema_output.gif)

### Punteggi granulari grezzi {#raw-granular-scores}

 Attribution AI produce i punteggi di attribuzione nel livello più granulare possibile, in modo che sia possibile suddividere i punteggi e renderli più dadi per qualsiasi colonna di punteggio. Per visualizzare questi punteggi nell’interfaccia utente, leggi la sezione sulla [visualizzazione dei percorsi](#raw-score-path)di valutazione non elaborati. Per scaricare i punteggi utilizzando l&#39;API, visita i punteggi di [download nel documento  Attribution AI](./download-scores.md) .

>[!NOTE]
>
> Potete visualizzare qualsiasi colonna di reporting desiderata dal dataset di input nel dataset di output del punteggio solo se una delle seguenti colonne è vera:
> - La colonna del rapporto è inclusa nella pagina di configurazione come parte della configurazione del punto di contatto o della definizione di conversione.
> - La colonna di reporting è inclusa in colonne di set di dati con punteggio aggiuntive.


Nella tabella seguente sono delineati i campi dello schema nell’esempio di output dei punteggi non elaborati:

| Nome colonna (DataType) | Nullable | Descrizione |
| --- | --- | --- |
| timestamp (DateTime) | False | L&#39;ora in cui si è verificato un evento o un&#39;osservazione di conversione. <br> **Esempio:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap dell&#39;utente simile al formato CEE XDM. |
| eventType (String) | True | Il tipo di evento principale per il record della serie temporale. <br> **Esempio:** &quot;Order&quot;, &quot;Purchase&quot;, &quot;Visit&quot; |
| eventMergeId (String) | True | Un ID per correlare o unire più [!DNL Experience Events] elementi che sono sostanzialmente lo stesso evento o che devono essere uniti. Questo è destinato a essere compilato dal produttore di dati prima dell’assimilazione. <br> **Esempio:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | False | Un identificatore univoco per l&#39;evento delle serie temporali. <br> **Esempio:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (oggetto) | False | Il contenitore di oggetti di livello superiore che viene associato all&#39;ID tentante. <br> **Esempio:** _atsdsnrmsv2 |
| your_schema_name (Object) | False | Riga di punteggio con evento di conversione tutti gli eventi dei punti di contatto ad esso associati e i relativi metadati. <br> **Esempio:**  Punteggi Attribution AI - Nome Modello__2020 |
| segmentazione (String) | True | Segmento di conversione, ad esempio la segmentazione geografica rispetto alla quale il modello è costruito. In caso di assenza di segmenti, il segmento è uguale a conversionName. <br> **Esempio:** ORDER_US |
| conversionName (String) | True | Nome della conversione configurata durante l&#39;installazione. <br> **Esempio:** Ordine, Lead, Visita |
| conversion (oggetto) | False | Conversione delle colonne di metadati. |
| dataSource (String) | True | Identificazione univoca globale di un&#39;origine dati. <br> **Esempio:**  Adobe Analytics |
| eventSource (String) | True | L&#39;origine dell&#39;evento effettivo. <br> **Esempio:**  Adobe.com |
| eventType (String) | True | Il tipo di evento principale per il record della serie temporale. <br> **Esempio:** Ordine |
| geo (String) | True | Posizione geografica in cui è stata consegnata la conversione `placeContext.geo.countryCode`. <br> **Esempio:** US |
| priceTotal (Double) | True | Entrate ottenute mediante la conversione <br> **Esempio:** 99,9 |
| product (String) | True | Identificatore XDM del prodotto stesso. <br> **Esempio:** RX 1080 ti |
| productType (String) | True | Nome visualizzato per il prodotto presentato all&#39;utente per la visualizzazione del prodotto. <br> **Esempio:** Gpus |
| quantità (numero intero) | True | Quantità acquistata durante la conversione. <br> **Esempio:** 1 1080 ti |
| ReceivedTimestamp (DateTime) | True | È stata ricevuta la marca temporale della conversione. <br> **Esempio:** 2020-06-09T00:01:51.000Z |
| skuId (String) | True | Unità di conservazione delle scorte (SKU), identificatore univoco per un prodotto definito dal fornitore. <br> **Esempio:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Timestamp della conversione. <br> **Esempio:** 2020-06-09T00:01:51.000Z |
| passThrough (oggetto) | True | Colonne di set di dati di punteggio aggiuntive specificate dall&#39;utente durante la configurazione del modello. |
| commerce_order_purchaseCity (String) | True | Colonna dataset Punteggio Aggiuntiva. <br> **Esempio:** città : San Jose |
| customerProfile (Oggetto) | False | Dettagli identità dell&#39;utente utilizzato per creare il modello. |
| identity (Object) | False | Contiene i dettagli dell&#39;utente utilizzato per creare il modello, ad esempio `id` e `namespace`. |
| id (String) | True | ID identità dell’utente, ad esempio ID cookie o AAID o MCID ecc. <br> **Esempio:** 1734876272540865634468320891369597404 |
| namespace (String) | True | Spazio dei nomi identità utilizzato per creare i percorsi e quindi il modello. <br> **Esempio:** aid |
| touchpointsDetail (array di oggetti) | True | L&#39;elenco dei dettagli dei punti di contatto che determinano la conversione ordinata dall&#39;occorrenza del punto di contatto o dalla marca temporale. |
| touchPointName (String) | True | Nome del punto di contatto configurato durante l’installazione. <br> **Esempio:** PAID_SEARCH_CLICK |
| scores (oggetto) | True | Contributo punto di contatto a questa conversione come punteggio. Per ulteriori informazioni sui punteggi prodotti all&#39;interno di questo oggetto, vedere la sezione [punteggi](#aggregated-attribution-scores) di attribuzione aggregati. |
| touchPoint (oggetto) | True | Metadati punto di contatto. Per ulteriori informazioni sui punteggi prodotti all&#39;interno di questo oggetto, vedere la sezione [punteggi](#aggregated-scores) aggregati. |

### Visualizzazione di percorsi di valutazione non elaborati (interfaccia utente) {#raw-score-path}

Puoi visualizzare il percorso dei punteggi non elaborati nell’interfaccia utente. Per iniziare, seleziona **[!UICONTROL Schemas]** nell’interfaccia utente della piattaforma, quindi cerca e seleziona il tuo schema di valutazione AI dell’attribuzione dall’interno della *[!UICONTROL Browse]* scheda.

![Scegli lo schema](./images/input-output/schemas_browse.png)

Quindi, selezionate un campo all’interno della *[!UICONTROL Structure]* finestra dell’interfaccia utente, si apre la *[!UICONTROL Field properties]* scheda. All&#39;interno *[!UICONTROL Field properties]* è il *[!UICONTROL Path]* campo associato ai punteggi non elaborati.

![Selezione di uno schema](./images/input-output/field_properties.png)


### Punteggi di attribuzione aggregati {#aggregated-attribution-scores}

I punteggi aggregati possono essere scaricati in formato CSV dall’interfaccia utente della piattaforma se l’intervallo di date è inferiore a 30 giorni.

 Attribution AI supporta due categorie di punteggi di attribuzione, algoritmi e basati su regole.

 Attribution AI produce due diversi tipi di punteggi algoritmici, incrementali e influenzati. Un punteggio influenzato è la frazione della conversione di cui è responsabile ogni punto di contatto marketing. Un punteggio incrementale è l&#39;importo dell&#39;impatto marginale direttamente causato dal punto di contatto di marketing. La differenza principale tra il punteggio incrementale e il punteggio influenzato è che il punteggio incrementale prende in considerazione l&#39;effetto previsto. Non presuppone che una conversione sia causata esclusivamente dai punti di contatto di marketing precedenti.

Di seguito è riportato un breve esempio di output dello schema di Attribution AI  dall&#39;interfaccia utente di Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Per ulteriori informazioni su ciascuno di questi punteggi di attribuzione, consulta la tabella seguente:

| Punti di attribuzione | Descrizione |
| ----- | ----------- |
| Influenzato (algoritmico) | Il punteggio influenzato è la frazione della conversione di cui è responsabile ogni punto di contatto marketing. |
| Incremental (algoritmico) | Il punteggio incrementale è la quantità di impatto marginale direttamente causato da un punto di contatto di marketing. |
| Primo contatto | Punteggio di attribuzione basato su regole che assegna tutti i crediti al punto di contatto iniziale di un percorso di conversione. |
| Ultimo contatto | Punteggio di attribuzione basato su regole che assegna tutti i crediti al punto di contatto più vicino alla conversione. |
| Lineare | Punteggio di attribuzione basato su regole che assegna lo stesso credito a ogni punto di contatto di un percorso di conversione. |
| A forma di U | Punteggio di attribuzione basato su regole che assegna il 40% del credito al primo punto di contatto e il 40% del credito all&#39;ultimo punto di contatto, con gli altri punti di contatto che dividono il restante 20% in modo uniforme. |
| Decadimento nel tempo | Punteggio di attribuzione basato su regole in cui i punti di contatto più vicini alla conversione ricevono più credito rispetto ai punti di contatto più distanti nel tempo dalla conversione. |

**Riferimento Punteggio non elaborato (punteggi di attribuzione)**

La tabella seguente mappa i punteggi di attribuzione ai punteggi non elaborati. Se desiderate scaricare i punteggi grezzi, visitate i punteggi di [download nella documentazione  Attribution AI](./download-scores.md) .

| Punti di attribuzione | Colonna di riferimento per la valutazione non elaborata |
| --- | --- |
| Influenzato (algoritmico) | _tenantID.your_schema_name.element.touchPoint.algorithmInfluencing |
| Incremental (algoritmico) | _tenantID.your_schema_name.touchDetail.element.touchPoint.algorithmInfluenzated |
| Primo contatto | _tenantID.your_schema_name.touchpointsDetail.element.touchPoint.firstTouch |
| Ultimo contatto | _tenantID.your_schema_name.touchpointsDetail.element.touchPoint.lastTouch |
| Lineare | _tenantID.your_schema_name.touchDetail.element.touchPoint.linear |
| A forma di U | _tenantID.your_schema_name.touchpointsDetail.element.touchPoint.uShape |
| Decadimento nel tempo | _tenantID.your_schema_name.touchDetail.element.touchPoint.decayUnits |

### Punteggi aggregati {#aggregated-scores}

I punteggi aggregati possono essere scaricati in formato CSV dall’interfaccia utente della piattaforma se l’intervallo di date è inferiore a 30 giorni. Per ulteriori informazioni su ciascuna di queste colonne di aggregazione, vedere la tabella seguente.

| Nome colonna | Vincolo | Nullable | Descrizione |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Formato definito dall&#39;utente e fisso | False | Data evento cliente in formato AAAA-MM-GG. <br> **Esempio**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Formato definito dall&#39;utente e fisso | True | Media Touchpoint Date in formato AAAA-MM-GG <br> **Esempio**: 21/04/2017 |
| segment (String) | Calcolato | False | Segmento di conversione, ad esempio la segmentazione geografica rispetto alla quale il modello è costruito. In caso di assenza di segmenti, il segmento è uguale a conversion_scope. <br> **Esempio**: ORDER_AMER |
| conversion_scope (String) | Definito dall&#39;utente | False | Nome della conversione configurata dall&#39;utente. <br> **Esempio**: ORDINE |
| touchpoint_scope (String) | Definito dall&#39;utente | True | Nome del punto di contatto configurato dall’utente <br> **Esempio**: PAID_SEARCH_CLICK |
| product (String) | Definito dall&#39;utente | True | Identificatore XDM del prodotto. <br> **Esempio**: CC |
| product_type (String) | Definito dall&#39;utente | True | Nome visualizzato per il prodotto presentato all&#39;utente per la visualizzazione del prodotto. <br> **Esempio**: gpus, laptop |
| geo (String) | Definito dall&#39;utente | True | Posizione geografica in cui è stata distribuita la conversione (placeContext.geo.countryCode) <br> **Esempio**: US |
| event_type (String) | Definito dall&#39;utente | True | Il tipo di evento principale per questo record della serie temporale <br> **Esempio**: Conversione a pagamento |
| media_type (String) | ENUM | False | Descrive se il tipo di supporto è pagato, posseduto o ottenuto. <br> **Esempio**: PAGATO, PROPRIETARIO |
| channel (String) | ENUM | False | La `channel._type` proprietà utilizzata per fornire una classificazione approssimativa dei canali con proprietà simili in [!DNL Consumer Experience Event] XDM. <br> **Esempio**: CERCA |
| action (String) | ENUM | False | La `mediaAction` proprietà viene utilizzata per fornire un tipo di azione multimediale evento esperienza. <br> **Esempio**: FATE CLIC |
| campaign_group (String) | Definito dall&#39;utente | True | Nome del gruppo di campagne in cui più campagne sono raggruppate come &#39;50%_DISCOUNT&#39;. <br> **Esempio**: COMMERCIALE |
| campaign_name (String) | Definito dall&#39;utente | True | Nome della campagna utilizzata per identificare la campagna di marketing come &#39;50%_DISCOUNT_USA&#39; o &#39;50%_DISCOUNT_ASIA&#39;. <br> **Esempio**: Vendita ringraziamento |

**Riferimento Raw Score (aggregato)**

La tabella seguente mappa i punteggi aggregati sulle valutazioni non elaborate. Se desiderate scaricare i punteggi grezzi, visitate i punteggi di [download nella documentazione  Attribution AI](./download-scores.md) . Per visualizzare i percorsi di valutazione non elaborati dall&#39;interfaccia utente, visita la sezione sulla [visualizzazione dei percorsi](#raw-score-path) di valutazione non elaborati all&#39;interno di questo documento.

| Nome colonna | Colonna di riferimento Punteggio non elaborato |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchDetail.element.touchPoint.timestamp |
| segmento | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchPoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchPointName |
| product | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchPoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchPoint.mediaChannel |
| action | _tenantID.your_schema_name.touchpointsDetail.element.touchPoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchDetail.element.touchPoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchDetail.element.touchPoint.campaignName |


## Passaggi successivi {#next-steps}

Dopo aver preparato i dati e aver inserito tutte le credenziali e gli schemi, iniziare seguendo la guida [utente](./user-guide.md)Attribution AI. Questa guida illustra come creare un’istanza per  Attribution AI.