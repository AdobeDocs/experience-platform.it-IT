---
keywords: Experience Platform;guida introduttiva;Attribution ai;argomenti comuni;Attribution ai input;Attribution ai output;
feature: Attribution AI
title: Input e output in Attribution AI
description: Il documento seguente illustra i diversi input e output utilizzati in Attribution AI.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2467'
ht-degree: 2%

---

# Input e output in [!DNL Attribution AI]

Il documento seguente illustra i diversi input e output utilizzati in [!DNL Attribution AI].

## [!DNL Attribution AI] dati di input

Attribution AI funziona analizzando i seguenti set di dati per calcolare i punteggi algoritmici:

- Set di dati di Adobe Analytics che utilizzano il [connettore di origine di Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Set di dati di Experience Event (EE) in generale dallo schema di Adobe Experience Platform
- Set di dati di Consumer Experience Event (CEE)

Ora puoi aggiungere più set di dati da origini diverse in base al **mapping delle identità** (campo) se ciascuno dei set di dati condivide lo stesso tipo di identità (spazio dei nomi), ad esempio un ECID. Dopo aver selezionato un’identità e uno spazio dei nomi, vengono visualizzate le metriche di completezza della colonna ID che indicano il volume di dati uniti. Per ulteriori informazioni sull&#39;aggiunta di più set di dati, visitare la [guida utente di Attribution AI](./user-guide.md#identity).

Per impostazione predefinita, le informazioni sul canale non vengono sempre mappate. In alcuni casi, se mediaChannel (campo) è vuoto, non sarà possibile &quot;continuare&quot; finché non si mappa un campo su mediaChannel in quanto si tratta di una colonna obbligatoria. Se il canale viene rilevato nel set di dati, viene mappato su mediaChannel per impostazione predefinita. Le altre colonne, ad esempio **tipo di supporto** e **azione supporto**, sono ancora facoltative.

Dopo aver mappato il campo del canale, continua con il passaggio &quot;Definisci eventi&quot; in cui puoi selezionare gli eventi di conversione e gli eventi dei punti di contatto e scegliere campi specifici dai singoli set di dati.

>[!IMPORTANT]
>
>Il connettore di origine di Adobe Analytics può richiedere fino a quattro settimane per la retrocompilazione dei dati. Se hai impostato di recente un connettore, devi verificare che il set di dati abbia la lunghezza minima dei dati richiesta per l’Attribution AI. Rivedi la sezione [dati storici](#data-requirements) per verificare di disporre di dati sufficienti per calcolare punteggi algoritmici accurati.

Per ulteriori dettagli sulla configurazione dello schema [!DNL Consumer Experience Event] (CEE), fare riferimento alla [Guida alla preparazione dei dati di Intelligent Services](../data-preparation.md). Per ulteriori informazioni sulla mappatura dei dati di Adobe Analytics, consulta la documentazione sulle [mappature dei campi di Analytics](../../sources/connectors/adobe-applications/analytics.md).

Non tutte le colonne dello schema [!DNL Consumer Experience Event] (CEE) sono obbligatorie per l&#39;Attribution AI.

Puoi configurare i punti di contatto utilizzando qualsiasi campo consigliato di seguito nello schema o nel set di dati selezionato.

| Colonne consigliate | Necessario per |
| --- | --- |
| Campo di identità primaria | Punto di contatto/conversione |
| Timestamp | Punto di contatto/conversione |
| Canale._type | Punto di contatto |
| Channel.mediaAction | Punto di contatto |
| Channel.mediaType | Punto di contatto |
| Marketing.trackingCode | Punto di contatto |
| Marketing.campaignname | Punto di contatto |
| Marketing.campaigngroup | Punto di contatto |
| Commerce | Conversione |

In genere, l’attribuzione viene eseguita su colonne di conversione come ordine, acquisti e pagamenti in &quot;commerce&quot;. Le colonne per &quot;canale&quot; e &quot;marketing&quot; vengono utilizzate per definire i punti di contatto per le Attribution AI (ad esempio, `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Per risultati e informazioni ottimali, si consiglia vivamente di includere il maggior numero possibile di colonne di conversione e di punti di contatto. Inoltre, non sei limitato alle sole colonne di cui sopra. Puoi includere qualsiasi altra colonna consigliata o personalizzata come definizione di conversione o punto di contatto.

I set di dati dell’evento esperienza (EE) non devono disporre esplicitamente di mixin di canale e marketing, purché le informazioni sul canale o sulla campagna rilevanti per la configurazione di un punto di contatto siano presenti in uno dei campi mixin o pass-through.

>[!TIP]
>
>Se si utilizzano dati di Adobe Analytics nello schema CEE, le informazioni sui punti di contatto per Analytics vengono in genere memorizzate in `channel.typeAtSource` (ad esempio, `channel.typeAtSource = 'email'`).

## Dati storici {#data-requirements}

>[!IMPORTANT]
>
> La quantità minima di dati necessaria per il funzionamento di Attribution AI è la seguente:
> - Devi fornire almeno 3 mesi (90 giorni) di dati per eseguire un buon modello.
> - Sono necessarie almeno 1000 conversioni.

Attribution AI richiede dati storici come input per l’apprendimento dei modelli. La durata dei dati richiesta è determinata principalmente da due fattori chiave: l’intervallo di formazione e l’intervallo di lookback. Gli input con finestre di formazione più brevi sono più sensibili alle tendenze recenti, mentre finestre di formazione più lunghe contribuiscono a produrre modelli più stabili e precisi. È importante modellare l’obiettivo con dati storici che rappresentino al meglio i tuoi obiettivi aziendali.

La [configurazione della finestra di formazione](./user-guide.md#training-window) filtra gli eventi di conversione impostati per essere inclusi nell&#39;apprendimento del modello in base al tempo di occorrenza. Attualmente, la finestra di formazione minima è di 1 trimestre (90 giorni). L&#39;[intervallo di lookback](./user-guide.md#lookback-window) fornisce un intervallo di tempo che indica quanti giorni prima devono essere inclusi i punti di contatto dell&#39;evento di conversione correlati a questo evento di conversione. Questi due concetti determinano insieme la quantità di dati di input (misurati in giorni) necessari per un&#39;applicazione.

Per impostazione predefinita, Attribution AI definisce l’intervallo di formazione come i 2 trimestri (6 mesi) più recenti e l’intervallo di lookback come 56 giorni. In altre parole, il modello prenderà in considerazione tutti gli eventi di conversione definiti che si sono verificati negli ultimi 2 trimestri e cercherà tutti i punti di contatto che si sono verificati entro 56 giorni prima degli eventi di conversione associati.

**Formula**:

Lunghezza minima dei dati richiesti = intervallo di formazione + intervallo di lookback

>[!TIP]
>
> La lunghezza minima dei dati richiesta per un&#39;applicazione con configurazioni predefinite è: 2 trimestri (180 giorni) + 56 giorni = 236 giorni.

Esempio:

- Desideri attribuire gli eventi di conversione che si sono verificati negli ultimi 90 giorni (3 mesi) e tenere traccia di tutti i punti di contatto che si sono verificati nelle 4 settimane precedenti l’evento di conversione. La durata dei dati di input deve essere compresa negli ultimi 90 giorni + 28 giorni (4 settimane). L’intervallo di formazione è di 90 giorni e l’intervallo di lookback è di 28 giorni, per un totale di 118 giorni.

## Attribution AI dati di output

Attribution AI produce i seguenti risultati:

- [Punteggi granulari non elaborati](#raw-granular-scores)
- [Punteggi aggregati](#aggregated-attribution-scores)

**Esempio di schema di output:**

![](./images/input-output/schema_output.gif)

### Punteggi granulari non elaborati {#raw-granular-scores}

Attribution AI restituisce i punteggi di attribuzione nel livello più granulare possibile, in modo da poter suddividere i punteggi in base a qualsiasi colonna di punteggio. Per visualizzare questi punteggi nell&#39;interfaccia utente, leggi la sezione su [visualizzazione dei percorsi di punteggio non elaborati](#raw-score-path). Per scaricare i punteggi utilizzando l&#39;API, visita il documento [download dei punteggi in Attribution AI](./download-scores.md).

>[!NOTE]
>
> Puoi visualizzare qualsiasi colonna di reporting desiderata dal set di dati di input nel set di dati di output del punteggio solo se si verifica una delle seguenti condizioni:
> - La colonna per la generazione di rapporti è inclusa nella pagina di configurazione come parte della configurazione del punto di contatto o della definizione di conversione.
> - La colonna di reporting è inclusa in colonne aggiuntive di set di dati di punteggio.

La tabella seguente illustra i campi dello schema nell’output dell’esempio di punteggi non elaborati:

| Nome colonna (DataType) | Nullable | Descrizione |
| --- | --- | --- |
| timestamp (DateTime) | False | Il momento in cui si è verificato un evento di conversione o un’osservazione. <br> **Esempio:** 2020-06-09T00:01:51.000Z |
| identityMap (mappa) | True | identityMap dell’utente simile al formato XDM CEE. |
| eventType (String) | True | Il tipo di evento principale per questo record di serie temporali. <br> **Esempio:** &quot;Ordine&quot;, &quot;Acquisto&quot;, &quot;Visita&quot; |
| eventMergeId (Stringa) | True | ID per correlare o unire più [!DNL Experience Events] che sono essenzialmente lo stesso evento o che devono essere uniti. Questo deve essere compilato dal produttore dei dati prima dell’acquisizione. <br> **Esempio:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (stringa) | False | Un identificatore univoco dell’evento della serie temporale. <br> **Esempio:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (oggetto) | False | Contenitore di oggetti di primo livello corrispondente all&#39;ID tentante. <br> **Esempio:** _atsdsnrmmsv2 |
| your_schema_name (Oggetto) | False | Riga di punteggio con evento di conversione tutti gli eventi punto di contatto associati a esso e i relativi metadati. <br> **Esempio:** Punteggi Attribution AI - Nome modello__2020 |
| segmentazione (stringa) | True | Segmento di conversione come la segmentazione geografica rispetto alla quale viene generato il modello. In caso di assenza di segmenti, il segmento è uguale a conversionName. <br> **Esempio:** ORDER_US |
| conversionName (String) | True | Nome della conversione configurata durante la configurazione. <br> **Esempio:** Ordine, lead, visita |
| Conversione (oggetto) | False | Colonne di metadati di conversione. |
| dataSource (String) | True | Identificazione univoca globale di un&#39;origine dati. <br> **Esempio:** Adobe Analytics |
| eventSource (Stringa) | True | La sorgente in cui si è verificato l’evento effettivo. <br> **Esempio:** Adobe.com |
| eventType (String) | True | Il tipo di evento principale per questo record di serie temporali. <br> **Esempio:** ordine |
| geo (Stringa) | True | La posizione geografica in cui è stata consegnata la conversione `placeContext.geo.countryCode`. <br> **Esempio:** US |
| priceTotal (Doppio) | True | Ricavi ottenuti tramite la conversione <br> **Esempio:** 99.9 |
| product (String) | True | L’identificatore XDM del prodotto stesso. <br> **Esempio:** RX 1080 ti |
| productType (String) | True | Il nome visualizzato del prodotto presentato all’utente per questa visualizzazione prodotto. <br> **Esempio:** Gpu |
| quantità (numero intero) | True | Quantità acquistata durante la conversione. <br> **Esempio:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Timestamp ricevuto della conversione. <br> **Esempio:** 2020-06-09T00:01:51.000Z |
| skuId (stringa) | True | Stock Keeping Unit (SKU), l’identificatore univoco di un prodotto definito dal fornitore. <br> **Esempio:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Timestamp della conversione. <br> **Esempio:** 2020-06-09T00:01:51.000Z |
| passThrough (oggetto) | True | Colonne aggiuntive del set di dati di punteggio specificate dall’utente durante la configurazione del modello. |
| commerce_order_purchaseCity (Stringa) | True | Colonna aggiuntiva del set di dati di punteggio. <br> **Esempio:** città: San Jose |
| customerProfile (oggetto) | False | Dettagli di identità dell’utente utilizzato per generare il modello. |
| identità (oggetto) | False | Contiene i dettagli dell&#39;utente utilizzato per generare il modello, ad esempio `id` e `namespace`. |
| id (Stringa) | True | ID identità dell&#39;utente come ID cookie, Adobe Analytics ID (AAID) o ID Experience Cloud (ECID, noto anche come MCID o come ID visitatore) ecc. <br> **Esempio:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Spazio dei nomi identità utilizzato per creare i percorsi e quindi il modello. <br> **Esempio:** aaid |
| touchpointsDetail (array di oggetti) | True | L’elenco dei dettagli del punto di contatto che conducono alla conversione ordinata da | occorrenza del punto di contatto o marca temporale. |
| touchpointName (stringa) | True | Nome del punto di contatto configurato durante la configurazione. <br> **Esempio:** PAID_SEARCH_CLICK |
| punteggi (oggetto) | True | Contributo del punto di contatto a questa conversione come punteggio. Per ulteriori informazioni sui punteggi prodotti in questo oggetto, consulta la sezione [punteggi di attribuzione aggregati](#aggregated-attribution-scores). |
| touchPoint (oggetto) | True | Metadati punto di contatto. Per ulteriori informazioni sui punteggi prodotti in questo oggetto, vedere la sezione [punteggi aggregati](#aggregated-scores). |

### Visualizzazione dei percorsi di punteggio non elaborati (UI) {#raw-score-path}

Puoi visualizzare il percorso dei punteggi non elaborati nell’interfaccia utente. Inizia selezionando **[!UICONTROL Schemi]** nell&#39;interfaccia utente di Platform, quindi cerca e seleziona lo schema dei punteggi di IA per l&#39;attribuzione dalla scheda **[!UICONTROL Sfoglia]**.

![Scegli lo schema](./images/input-output/schemas_browse.png)

Quindi, seleziona un campo nella finestra **[!UICONTROL Struttura]** dell&#39;interfaccia utente. Verrà aperta la scheda **[!UICONTROL Proprietà campo]**. All&#39;interno di **[!UICONTROL Proprietà campo]** è il campo percorso mappato ai punteggi non elaborati.

![Scegli uno schema](./images/input-output/field_properties.png)

### Punteggi di attribuzione aggregati {#aggregated-attribution-scores}

I punteggi aggregati possono essere scaricati in formato CSV dall’interfaccia utente di Platform se l’intervallo di date è inferiore a 30 giorni.

Attribution AI supporta due categorie di punteggi di attribuzione, algoritmici e basati su regole.

Attribution AI produce due diversi tipi di punteggi algoritmici, incrementali e influenzati. Un punteggio influenzato è la frazione della conversione di cui è responsabile ogni punto di contatto di marketing. Un punteggio incrementale è la quantità di impatto marginale causato direttamente dal punto di contatto di marketing. La differenza principale tra il punteggio incrementale e il punteggio influenzato è che il punteggio incrementale tiene conto dell’effetto al basale. Non presuppone che una conversione sia causata esclusivamente dai precedenti punti di contatto di marketing.

Ecco un esempio di output con schema di Attribution AI dall’interfaccia utente di Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Per ulteriori dettagli su ciascuno di questi punteggi di attribuzione, consulta la tabella seguente:

| Punteggi di attribuzione | Descrizione |
| ----- | ----------- |
| Influenzato (algoritmico) | Il punteggio influenzato è la frazione della conversione di cui è responsabile ogni punto di contatto di marketing. |
| Incrementale (algoritmico) | Il punteggio incrementale è la quantità di impatto marginale causato direttamente da un punto di contatto di marketing. |
| Primo contatto | Punteggio di attribuzione basato su regole che assegna tutti i crediti al punto di contatto iniziale in un percorso di conversione. |
| Ultimo contatto | Punteggio di attribuzione basato su regole che assegna tutto il credito al punto di contatto più vicino alla conversione. |
| Lineare | Punteggio di attribuzione basato su regole che assegna lo stesso credito a ciascun punto di contatto in un percorso di conversione. |
| A forma di U | Punteggio di attribuzione basato su regole che assegna il 40% del credito al primo punto di contatto e il 40% del credito all’ultimo punto di contatto, con gli altri punti di contatto che dividono il restante 20% in parti uguali. |
| Decadimento nel tempo | Punteggio di attribuzione basato su regole in cui i punti di contatto più vicini alla conversione ricevono più credito rispetto ai punti di contatto più lontani nel tempo dalla conversione. |

**Riferimento punteggio non elaborato (punteggi di attribuzione)**

La tabella seguente mappa i punteggi di attribuzione in base ai punteggi non elaborati. Se desideri scaricare i tuoi punteggi non elaborati, visita la sezione [download dei punteggi nella documentazione di Attribution AI](./download-scores.md).

| Punteggi di attribuzione | Colonna di riferimento punteggio non elaborato |
| --- | --- |
| Influenzato (algoritmico) | _tenantID.nome_schema.elemento.punto.algoritmoInfluenzato |
| Incrementale (algoritmico) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluenzato |
| Primo contatto | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Ultimo contatto | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Lineare | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| A forma di U | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Decadimento nel tempo | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Punteggi aggregati {#aggregated-scores}

I punteggi aggregati possono essere scaricati in formato CSV dall’interfaccia utente di Platform se l’intervallo di date è inferiore a 30 giorni. Per ulteriori dettagli su ciascuna di queste colonne aggregate, consulta la tabella seguente.

| Nome colonna | Vincolo | Nullable | Descrizione |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Definito dall&#39;utente e formato fisso | False | Data evento cliente in formato AAAA-MM-GG. <br> **Esempio**: 02/05/2016 |
| mediatouchpoints_date (DateTime) | Definito dall&#39;utente e formato fisso | True | Data punto di contatto multimediale in formato AAAA-MM-GG <br> **Esempio**: 21/04/2017 |
| segmento (stringa) | Calcolato | False | Segmento di conversione, ad esempio segmentazione geografica, in base alla quale viene generato il modello. In caso di assenza di segmenti, il segmento è uguale a conversion_scope. <br> **Esempio**: ORDER_AMER |
| conversion_scope (Stringa) | Definita dall’utente | False | Nome della conversione configurato dall’utente. <br> **Esempio**: ORDINE |
| touchpoint_scope (Stringa) | Definita dall’utente | True | Nome del punto di contatto configurato dall&#39;utente <br> **Esempio**: PAID_SEARCH_CLICK |
| product (String) | Definita dall’utente | True | L’identificatore XDM del prodotto. <br> **Esempio**: CC |
| product_type (String) | Definita dall’utente | True | Il nome visualizzato del prodotto presentato all’utente per questa visualizzazione prodotto. <br> **Esempio**: gpu, laptop |
| geo (Stringa) | Definita dall’utente | True | La posizione geografica in cui è stata consegnata la conversione (placeContext.geo.countryCode) <br> **Esempio**: Stati Uniti |
| event_type (Stringa) | Definita dall’utente | True | Il tipo di evento primario per questo record di serie temporali <br> **Esempio**: conversione a pagamento |
| media_type (String) | ENUM | False | Descrive se il tipo di file multimediale è pagato, di proprietà o guadagnato. <br> **Esempio**: PAID, OWNED |
| channel (String) | ENUM | False | La proprietà `channel._type` utilizzata per fornire una classificazione approssimativa dei canali con proprietà simili in [!DNL Consumer Experience Event] XDM. <br> **Esempio**: RICERCA |
| action (String) | ENUM | False | La proprietà `mediaAction` viene utilizzata per fornire un tipo di azione multimediale evento esperienza. <br> **Esempio**: CLIC |
| campaign_group (Stringa) | Definita dall’utente | True | Nome del gruppo di campagne in cui sono raggruppate più campagne, ad esempio &quot;SCONTO_50%&quot;. <br> **Esempio**: COMMERCIAL |
| campaign_name (Stringa) | Definita dall’utente | True | Nome della campagna utilizzato per identificare la campagna di marketing, ad esempio &quot;SCONTO_50%_STATI_UNITI&quot; o &quot;SCONTO_50%_ASIA&quot;. <br> **Esempio**: vendita del ringraziamento |

**Riferimento punteggio non elaborato (aggregato)**

La tabella seguente mappa i punteggi aggregati sui punteggi non elaborati. Se desideri scaricare i tuoi punteggi non elaborati, visita la sezione [download dei punteggi nella documentazione di Attribution AI](./download-scores.md). Per visualizzare i percorsi di punteggio non elaborati dall&#39;interfaccia utente, visitare la sezione [visualizzazione dei percorsi di punteggio non elaborati](#raw-score-path) in questo documento.

| Nome colonna | Colonna di riferimento Punteggio non elaborato |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmento | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| ambito_punto_contatto | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| prodotto | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.nome_schema.conversione.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| action | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| nome_campagna | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI utilizza solo dati aggiornati per l’ulteriore formazione e il punteggio. Allo stesso modo, quando richiedi di eliminare i dati, IA per l’analisi dei clienti si astiene dall’utilizzare i dati eliminati.
> - Attribution AI sfrutta i set di dati di Platform. Per supportare le richieste di diritti dei consumatori che un brand può ricevere, i brand devono utilizzare Platform Privacy Service per inviare ai consumatori le richieste di accesso e cancellazione per rimuovere i propri dati attraverso il data lake, il servizio Identity e il profilo cliente in tempo reale.
> - Tutti i set di dati utilizzati per l’input/output dei modelli seguiranno le linee guida di Platform. Platform Data Encryption si applica ai dati in transito e a riposo. Per ulteriori informazioni sulla [crittografia dei dati](../../../help/landing/governance-privacy-security/encryption.md), consulta la documentazione

## Passaggi successivi {#next-steps}

Dopo aver preparato i dati e aver impostato tutte le credenziali e gli schemi, inizia seguendo la [guida utente di Attribution AI](./user-guide.md). Questa guida illustra come creare un’istanza per Attribution AI.
