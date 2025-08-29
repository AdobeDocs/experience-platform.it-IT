---
title: Gruppo di campi schema estensione completa Adobe Advertising Cloud ExperienceEvent
description: Scopri il gruppo di campi dello schema Estensione completa Adobe Advertising Cloud ExperienceEvent.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---

# [!UICONTROL Estensione completa Adobe Advertising Cloud ExperienceEvent] gruppo di campi schema

>[!AVAILABILITY]
>
>Il gruppo di campi [!UICONTROL Estensione completa Adobe Advertising Cloud ExperienceEvent] è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!UICONTROL Estensione completa Adobe Advertising Cloud ExperienceEvent] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), che acquisisce le metriche comuni raccolte da Adobe Advertising (precedentemente denominato &quot;[!DNL Advertising Cloud]&quot;).

Questo documento descrive la struttura e il caso d&#39;uso del gruppo di campi dell&#39;estensione [!DNL Advertising Cloud].

>[!NOTE]
>
>Puoi anche cercare questo gruppo di campi [ nell&#39;interfaccia utente di Experience Platform](../../ui/explore.md) o visualizzare lo schema completo nel [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Struttura del gruppo di campi

Il gruppo di campi fornisce un singolo oggetto `_experience` a uno schema, che contiene un singolo oggetto `adcloud`.

![Campi di primo livello per il [!DNL Advertising Cloud] gruppo di campi](../../images/field-groups/advertising-full-extension/full-schema.png "Campi di primo livello per il [!DNL Advertising Cloud] gruppo di campi")

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `adDeliveryDetails` | Oggetto | Dettagli della consegna dell’annuncio. Per ulteriori informazioni sul contenuto dell&#39;oggetto, vedere la [sottosezione seguente sull&#39;oggetto `adDeliveryDetails`](#adDeliveryDetails). |
| `advertisement` | Oggetto | Dettagli pubblicitari digitali. Per ulteriori informazioni sul contenuto di questo oggetto, vedere la [sottosezione seguente sull&#39;oggetto pubblicitario](#advertisement). |
| `campaign` | Oggetto | Dettagli gerarchia campagna. Per ulteriori informazioni sul contenuto dell&#39;oggetto, vedere la [sottosezione seguente sull&#39;oggetto della campagna](#campaign-campaign). |
| `conversionDetails` | Oggetto | Dettagli della conversione per un annuncio. Per ulteriori informazioni sul contenuto dell&#39;oggetto, vedere la [sottosezione seguente](#conversionDetails). |
| `eventType` | Stringa | Il tipo di evento Adobe Advertising. |
| `fees` | Oggetto | Dettagli sulle tariffe di Advertising. Per ulteriori informazioni sul contenuto di questo oggetto, vedere la [sottosezione seguente sull&#39;oggetto tariffe](#fees). |
| `inventory` | Oggetto | Dettagli inventario. Per ulteriori informazioni sul contenuto dell&#39;oggetto, vedere la [sottosezione seguente](#inventory). |
| `productDetails` | Oggetto | Dettagli dell’annuncio del prodotto. Per ulteriori informazioni sul contenuto dell&#39;oggetto, vedere la [sottosezione seguente sull&#39;oggetto productDetails](#productDetails). |
| `stitchId` | Stringa | ID dai server di annunci Adobe Advertising per tenere traccia delle conversioni click-through nei browser che bloccano i cookie di terze parti. |

## `adDeliveryDetails` {#adDeliveryDetails}

L&#39;oggetto adDeliveryDetails fornisce informazioni su dove e come è stato distribuito l&#39;annuncio, inclusi i siti Web di posizionamento e gli identificatori di posizione.

![Diagramma di schema che mostra l&#39;oggetto `adDeliveryDetails` e i relativi campi.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `placementWebsite` | Stringa | Il sito web in cui è stato mostrato l’annuncio pubblicitario. |
| `siteLinkText` | Stringa | Il link effettivo del sito selezionato nell’annuncio. |
| `interestLocationID` | Stringa | Posizione dedotta dalla query di ricerca. Ad esempio, una query per &quot;Hotel in Goa&quot; restituisce l’ID per Goa, indipendentemente dalla posizione di navigazione effettiva dell’utente. |
| `physicalLocationID` | Stringa | Il percorso di navigazione dell’utente, rappresentato da un ID di riferimento proveniente dalla rete di annunci. Questo ID non è un nome di posizione leggibile (come una città o un paese), ma un codice assegnato dalla rete di annunci per identificare un target geografico. |

## `advertisement` {#advertisement}

L&#39;oggetto pubblicitario descrive i dettagli dell&#39;annuncio digitale, quali identificatori, tipo, contenuto creativo, targeting e parole chiave associate.

![Diagramma di schema che mostra l&#39;oggetto `advertisement` e i relativi campi.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `adId` | Stringa | L’identificatore dell’annuncio associato a questo evento. Questo ID non è correlato allo standard di settore Ad-ID. |
| `runtime` | Stringa | Il runtime dell’unità dell’annuncio, distinto dal runtime del browser o del sistema operativo. I valori possibili includono: `unknown` e `HTML5`. |
| `adClass` | Stringa | La classe dell&#39;annuncio dell&#39;evento guida: `display`, `video` o `social`. |
| `adUnitType` | Stringa | Identificatore del codice che esegue il rendering dell’annuncio in un browser o in un dispositivo. Possibili valori:<ul><li>`linearVideo`: video lineare</li><li>`interactiveVideo`: video interattivo</li><li>`banner`: banner,</li><li>`richMediaBanner`: banner rich media,</li><li>`newsFeedVideo`: video feed notizie,</li><li>`newsFeedDisplay`: visualizzazione feed notizie,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: nel video della pagina,</li><li>`inPageDisplay`: nella visualizzazione delle pagine,</li><li>`facebook`: Facebook,</li><li>`twitter`: Twitter,</li><li>`linearTv`: TV lineare,</li><li>`vod`: video on demand</li></ul> |
| `promotedAssetId` | Stringa | Identificatore della risorsa promossa nell’annuncio associato a questo evento. |
| `creativeID` | Stringa | L’identificatore del contenuto creativo dell’annuncio pubblicitario (ad esempio un banner, un video o un annuncio social) associato a questo evento. |
| `keywordID` | Stringa | Identificatore della parola chiave immessa dall&#39;utente in una query di ricerca che ha attivato l&#39;evento. |
| `keyword` | Stringa | La parola chiave dell&#39;inserzione su cui il cliente ha fatto un&#39;offerta. |
| `isDynamicSearchAd` | Booleano | Indica se l’evento proviene da un annuncio di ricerca dinamica. |
| `audienceID` | Stringa | Identificatore del segmento di pubblico di destinazione dell’annuncio. |
| `adGroupID` | Stringa | Identificatore del gruppo di annunci associato all’annuncio che ha attivato questo evento. |
| `campaignID` | Stringa | Identificatore della campagna associata all’annuncio che ha attivato questo evento. |
| `networkType` | Stringa | Tipo di rete in cui si è verificato l&#39;evento. Possibili valori: <ul><li>`search`: l&#39;annuncio è stato visualizzato nella rete di ricerca.</li><li>`content`: l&#39;annuncio è stato visualizzato nella rete dei contenuti.</li></ul> |
| `matchType` | Stringa | Tipo di corrispondenza della parola chiave. Possibili valori: <ul><li>`exact`: Corrispondenza esatta della parola chiave</li><li>`broad`: Corrispondenza ampia della parola chiave</li><li>`phrase`: Corrispondenza frase della parola chiave</li></ul> |

## `campaign` {#campaign}

L’oggetto campagna definisce la gerarchia della campagna pubblicitaria, inclusi gli identificatori di account, inserzionista, posizionamento e pacchetto, insieme ai dettagli della valuta.

![Diagramma di schema che mostra l&#39;oggetto `campaign` e i relativi campi.](../../images/field-groups/advertising-full-extension/campaign.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountId` | Stringa | Identificatore dell’account. |
| `dspId` | Stringa | L’identificatore del Demand Side Platform (DSP) in cui è definita la campagna. Di solito, questo identificatore è l’ID di Adobe Advertising Cloud DSP. |
| `campaignId` | Stringa | Identificatore della campagna. |
| `placementId` | Stringa | L’identificatore del posizionamento. |
| `packageId` | Stringa | Identificatore del pacchetto Advertising DSP. |
| `advertiserId` | Stringa | Identificatore dell&#39;inserzionista. |
| `experimentId` | Stringa | Identificatore dell’esperimento. |
| `sampleGroupId` | Stringa | Identificatore del gruppo di esempio. |
| `currency` | Stringa | Il codice valuta di fatturazione ISO 4217 per il conto. Utilizza il pattern di espressione regolare ^[A-Z]{3}$ (tre lettere maiuscole). Ad esempio: USD, EUR. |

## `conversionDetails` {#conversionDetails}

L&#39;oggetto conversionDetails acquisisce informazioni di tracciamento per le conversioni di annunci, inclusi codici di tracciamento, identità e proprietà di conversione.

![Diagramma di schema che mostra l&#39;oggetto `conversionDetails` e i relativi campi.](../../images/field-groups/advertising-full-extension/conversionDetails.png "campo conversionDetails")

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `trackingCode` | Stringa | Il codice di tracciamento della conversione per l’evento. Per un elenco dei possibili formati, consulta [Formati AMO ID](https://experienceleague.adobe.com/it/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats). |
| `trackingIdentities` | Stringa | ID EF o dettagli dell’identità di tracciamento di un evento. Per un elenco dei formati possibili, vedere [Formati ID EF](https://experienceleague.adobe.com/it/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Oggetto | Mappa delle proprietà di conversione, rappresentata come matrice di stringhe di coppie chiave-valore (ad esempio `subscriptions=253`). |

## `fees` {#fees}

L’oggetto tariffe acquisisce i costi relativi a contenuti multimediali, dati e altri costi pubblicitari, suddivisi per Advertising DSP, account e inserzionista.

![Diagramma di schema che mostra l&#39;oggetto `fees` e i relativi campi.](../../images/field-groups/advertising-full-extension/fees.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `DSPMediaFees` | Numero | Le tariffe dei media fatturabili da Advertising DSP. |
| `DSPDataFees` | Numero | Tariffe dei dati fatturabili da Advertising DSP. |
| `DSPOtherFees` | Numero | Altre tariffe fatturabili da Advertising DSP. |
| `accountMediaFees` | Numero | Tariffe dei media per l’account ma non fatturabili da Advertising DSP. |
| `accountDataFees` | Numero | Tariffe per i dati dell’account ma non fatturabili da Advertising DSP. |
| `accountOtherFees` | Numero | Altre tariffe per l’account ma non fatturabili da Advertising DSP. |
| `advertiserMediaFees` | Numero | Le tariffe applicate dall’inserzionista multimediale all’inserzionista dall’account. |
| `advertiserDataFees` | Numero | Altre tariffe dell&#39;inserzionista addebitate all&#39;inserzionista dall&#39;account. |
| `advertiserOtherFees` | Numero | Altre tariffe dell&#39;inserzionista addebitate all&#39;inserzionista dall&#39;account. |
| `billableMediaNetSpend` | Numero | La spesa netta fatturabile per la pubblicità mediatica. |
| `totalMediaNetSpend` | Numero | Spesa netta totale per la pubblicità multimediale. |
| `billableDataNetSpend` | Numero | La spesa netta fatturabile per la pubblicità dei dati. |
| `billableOtherNetSpend` | Numero | La spesa netta fatturabile per altri tipi di pubblicità. |
| `totalBillableNetSpend` | Numero | Spesa netta totale fatturabile. |
| `totalNonBillableNetSpend` | Numero | Spesa netta totale non fatturabile. |
| `totalNetSpend` | Numero | Spesa netta totale. |

## `inventory` {#inventory}

L’oggetto inventario registra i dettagli sull’opportunità di inventario dell’annuncio, inclusi i dati della sessione, i codici partner, gli ID sito, la valuta dei costi e le regole di segmentazione.

![Diagramma di schema che mostra l&#39;oggetto `inventory` e i relativi campi.](../../images/field-groups/advertising-full-extension/inventory.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `sessionId` | Stringa | L’ID sessione associato a un evento esperienza, utilizzato per collegare eventi indipendenti che si sono verificati nella stessa sessione. |
| `feedID` | Stringa | ID composito dell’editore, dello scambio di annunci e di altre funzioni. |
| `sspPartnerCode` | Stringa | Il partner (Exchange) tramite il quale Adobe Advertising Cloud riceve l’opportunità di inventario. |
| `siteID` | Stringa | Identificatore del sito Web in cui è stata distribuita l’ad impression. |
| `costCurrency` | Stringa | Il codice valuta ISO 4217 utilizzato per pagare un partner per un’opportunità pubblicitaria. Il valore deve seguire il pattern di espressione regolare ^[A-Z]{3}$ (tre lettere maiuscole). Ad esempio: USD, EUR. |
| `inventorySourceId` | Stringa | ID dell’origine dell’inventario di Adobe Advertising Cloud su cui è stata consegnata questa opportunità. |
| `segment` | Oggetto | Dettagli associati alle regole di segmentazione degli utenti. Le sue proprietà includono:<ul><li>`attributablePartnerId` (stringa): identificatore per il provider di segmenti proprietario dell&#39;attributableSegmentId.</li><li>`attributableSegmentId` (stringa): segmento accreditato per il targeting utente nella regola di targeting del posizionamento. Questo viene utilizzato per tenere traccia dei costi e pagare i partner.</li><li>`segments` (stringa): l&#39;intersezione dei segmenti utente a\) a cui apparteneva l&#39;utente e b\) a cui l&#39;annuncio era destinato. Non è l&#39;elenco completo dei segmenti a cui l&#39;utente apparteneva al momento dell&#39;asta.</li></ul> |
| `optimizationTag` | Stringa | Tag relativo all’ottimizzazione. |
| `attributableDeviceGraphId` | Stringa | Identificatore del grafico dei dispositivi attribuito a un evento di conversione. |

## `productDetails` {#productDetails}

L&#39;oggetto `productDetails` contiene informazioni sui prodotti presenti negli annunci per acquisti per [!DNL Adobe Advertising Search, Social, & Commerce], inclusi identificatori di prodotto, paese, lingua, partizione, titolo e tipo di annuncio.

![Diagramma di schema che mostra l&#39;oggetto `productDetails` e i relativi campi.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productID` | Stringa | L’identificatore del prodotto presente nell’annuncio associato a questo evento. |
| `country` | Stringa | Il paese di vendita del prodotto presente nell’annuncio associato all’evento. |
| `language` | Stringa | La lingua delle informazioni sul prodotto, come indicato nel feed dati del Merchant Center del cliente. |
| `partitionID` | Stringa | L’identificatore del gruppo di prodotti associato all’annuncio in questo evento. |
| `title` | Stringa | Il titolo del prodotto mostrato nell’annuncio pubblicitario. |
| `adType` | Stringa | Tipo di annuncio per il prodotto utilizzato nelle campagne acquisti [!DNL Google]. Possibili valori:<ul><li>`pla_with_pog`: quando l&#39;evento proviene da un acquisto tramite un annuncio</li><li>`pla`: quando l&#39;evento proviene da un annuncio di acquisto.</li><li>`pla_multichannel`: quando l&#39;evento da un annuncio di acquisto includeva opzioni per i canali di acquisto &quot;online&quot; e &quot;locali&quot;.</li><li>`pla_with_promotion`: quando l&#39;evento di un annuncio di acquisto ha mostrato una promozione per esercenti.</li></ul> |

## Passaggi successivi

Questo documento descrive la struttura e il caso d&#39;uso per il gruppo di campi dell&#39;estensione [!DNL Advertising Cloud]. Per ulteriori dettagli sul gruppo di campi stesso, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Se si utilizza questo gruppo di campi per raccogliere i dati di [!DNL Advertising] tramite Adobe Experience Platform Web SDK, vedere la guida alla [configurazione di uno stream di dati](../../../datastreams/overview.md) per informazioni su come mappare i dati a XDM sul lato server.
