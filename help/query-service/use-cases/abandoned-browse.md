---
keywords: Experience Platform;servizio query;servizio query;query service;query service;query service;query service;query service;query service;query service;query service;query service;query service;query service;query service;query service;query
title: Caso di utilizzo di esempio per Adobe Experience Platform Query Service
description: Un esempio end-to-end per dimostrare la versatilità e i vantaggi di Adobe Experience Platform Query Service.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Caso d&#39;uso di esempio per Adobe Experience Platform [!DNL Query Service]

Questo documento e la relativa presentazione video forniscono un flusso di lavoro end-to-end di alto livello che illustra i vantaggi di Adobe Experience Platform [!DNL Query Service] per le informazioni aziendali strategiche della tua organizzazione. Utilizzando un caso di utilizzo di abbandono navigazione come esempio, questa guida illustra i seguenti concetti chiave:

* L’importanza chiave dell’elaborazione dei dati per massimizzare il potenziale di Adobe Experience Platform.
* Modi per creare la query in base all’architettura dati esistente.
* Assicurati una qualità dei dati che soddisfi le tue esigenze e metodi per ridurre le carenze.
* Processo per pianificare l’esecuzione di una query a una frequenza impostata per l’utilizzo a valle nella segmentazione e nelle destinazioni per la personalizzazione.
* Facilità per gli addetti al marketing di includere set di dati derivati nei propri tipi di pubblico grazie alla potenza di [!DNL Query Service].

## Obiettivi {#objectives}

Questa dimostrazione di flusso di lavoro si basa su diversi servizi di Adobe Experience Platform. Se desideri procedere, ti consigliamo di comprendere bene le funzioni e i servizi seguenti:

* Le [nozioni di base sulla composizione dello schema Experience Data Model (XDM)](../../xdm/schema/composition.md)
* Come [creare set di dati e acquisire dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=it)
* Come [acquisire dati utilizzando il connettore di origine di Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=it)
* [Segmentazione](../../segmentation/home.md)
* [Destinazioni](../../destinations/home.md)

L&#39;esempio dell&#39;abbandono della navigazione è incentrato sull&#39;utilizzo dei dati di Adobe [!DNL Analytics] per creare un pubblico specifico utilizzabile. Il pubblico viene perfezionato per includere tutti i clienti che hanno navigato nel sito web negli ultimi quattro giorni ma non hanno effettuato un acquisto. A ogni profilo del pubblico viene quindi assegnato lo SKU più costoso risultante dal modello di comportamento del cliente.

La query stessa è molto prescrittiva e include solo dati che soddisfano i criteri del caso d’uso per la definizione del segmento. Questo migliora le prestazioni riducendo al minimo la quantità di [!DNL Analytics] dati in fase di elaborazione. Inoltre, ordina i dati in base al prezzo dal più alto al più basso e sceglie lo SKU più costoso che l’utente stava navigando.

Di seguito è riportata la query utilizzata nella presentazione:

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] esempio di abbandono navigazione con adobe analytics {#video-example}

La presentazione video riportata di seguito fornisce un caso d&#39;uso olistico e reale per i dati di Experience Platform incentrati sulle integrazioni di [!DNL Query Service] e Adobe Analytics.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Vantaggi di [!DNL Query Service] {#benefits}

Le funzionalità fornite da [!DNL Query Service] hanno molti scopi. Puoi utilizzarlo per adattarsi a logiche complesse per la segmentazione, per calcolare vari attributi personalizzati da utilizzare a valle o per semplificare notevolmente la modalità di creazione dei tipi di pubblico.

[!DNL Query Service] consente di includere vincoli nelle query per semplificare il processo di creazione del pubblico. Ciò migliora la qualità dei dati garantendo che i dati giusti siano idonei per i tipi di pubblico. Mantenere la qualità dei risultati delle query in un pubblico accurato e aiuta con l’affidabilità dei dati. Puoi anche salvare il pubblico creando schemi e tabelle personalizzate in base agli attributi derivati dalla query. È possibile abilitare una tabella personalizzata per Profilo e utilizzare questi punti dati per la segmentazione e la personalizzazione. Questa funzione aiuta gli esperti di marketing che desiderano creare un pubblico di persone chiaro.

Inoltre, includendo nella query una logica che soddisfi condizioni ricorrenti o statiche, [!DNL Query Service] estrae il carico di una segmentazione complessa.

Adobe Experience Platform fornisce un archivio di dati e gli strumenti necessari per attivare i dati in modo efficiente e affidabile. Mantenendo i dati all’interno di Experience Platform, consente di derivare gli attributi durante l’esecuzione di altri processi ed elimina la necessità di esportare i dati in strumenti di terze parti per la manipolazione e l’elaborazione. Tali costi generali di elaborazione possono influire notevolmente sulla timeline di un progetto quando si tratta di centinaia di attributi o campagne. Questo offre agli addetti al marketing un’unica posizione per accedere ai dati e creare campagne, nonché un mezzo molto dinamico per segmentare e personalizzare i messaggi.

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di capire in che modo [!DNL Query Service] influisce non solo sulla qualità dei tuoi dati e sulla facilità di segmentazione, ma anche sulla sua importanza all&#39;interno dell&#39;architettura dei dati per l&#39;intero flusso di lavoro end-to-end. Per esempi SQL più applicabili che utilizzano Adobe Analytics con [!DNL Query Service], vedere il caso d&#39;uso [Variabili di merchandising di Adobe Analytics](./merchandising-variables.md).

Altri documenti che dimostrano i vantaggi di [!DNL Query Service] per le informazioni aziendali strategiche della tua organizzazione sono l&#39;esempio del [caso di utilizzo del filtro bot](./bot-filtering.md).

In alternativa, questi documenti possono essere utili per comprendere le funzionalità di [!DNL Query Service]:

* [Linee guida per l’esecuzione delle query](../best-practices/writing-queries.md)
* [Guida per l&#39;organizzazione delle risorse dati](../best-practices/organize-data-assets.md).


