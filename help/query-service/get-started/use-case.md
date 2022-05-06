---
keywords: Experience Platform;servizio query;servizio query;query
title: Esempio di caso d’uso per il servizio query Adobe Experience Platform
topic-legacy: tutorial
description: Un esempio end-to-end per dimostrare la versatilità e i vantaggi di Adobe Experience Platform Query Service.
source-git-commit: 00039961bcda8e77bcff3cee36da422b3e466f52
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 1%

---

# Esempio di utilizzo per Adobe Experience Platform [!DNL Query Service]

Questo documento e la relativa presentazione video forniscono un flusso di lavoro end-to-end di alto livello che illustra come Adobe Experience Platform [!DNL Query Service] offre vantaggi per le informazioni strategiche di business della tua organizzazione. Utilizzando come esempio un caso di utilizzo di abbandono navigazione, questa guida illustra i seguenti concetti chiave:

* L&#39;importanza fondamentale del trattamento dei dati per massimizzare il potenziale di Adobe Experience Platform
* Modi per creare la query in base all’architettura dati esistente.
* Assicurati la qualità dei dati che soddisfi le tue esigenze e i metodi per attenuare eventuali carenze.
* Il processo per pianificare l’esecuzione di una query a una frequenza impostata da utilizzare a valle nella segmentazione e nelle destinazioni per la personalizzazione.
* La facilità con cui gli esperti di marketing possono includere attributi derivati nei loro segmenti attraverso la potenza di [!DNL Query Service].

## Obiettivi {#objectives}

Questa dimostrazione del flusso di lavoro si basa su diversi servizi Adobe Experience Platform. Se desideri seguire questa procedura, è consigliabile avere una buona comprensione delle seguenti funzioni e servizi:

* La [nozioni di base sulla composizione dello schema di Experience Data Model (XDM)](../../xdm/schema/composition.md)
* Come fare per [creare set di dati e acquisire dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* Come fare per [Acquisizione di dati tramite il connettore di origine Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=it)
* [Segmentazione](../../segmentation/home.md)
* [Destinazioni](../../destinations/home.md)

L’esempio di abbandono ricerca si concentra sull’utilizzo dell’Adobe [!DNL Analytics] per creare un pubblico actionable specifico. Il pubblico è perfezionato per includere tutti i clienti che hanno visitato il sito web negli ultimi quattro giorni ma non hanno effettuato un acquisto. Ogni profilo nel pubblico viene quindi indirizzato con lo SKU del prezzo più alto risultante dal modello di comportamento del cliente.

La query stessa è molto prescrittiva e include solo i dati che soddisfano i criteri del caso d’uso per la definizione del segmento. Ciò migliora le prestazioni riducendo al minimo la quantità di [!DNL Analytics] dati in fase di elaborazione. Inoltre, ordina i dati in base al prezzo da più alto a più basso e sceglie la SKU più costosa che l&#39;utente stava navigando.

La query utilizzata nella presentazione può essere visualizzata di seguito:

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

## [!DNL Query Service] esempio di abbandono navigazione tramite adobe analytics {#video-example}

La presentazione video riportata di seguito fornisce un caso d’uso olistico e reale per i dati di Experience Platform incentrati su [!DNL Query Service] e integrazioni Adobe analytics.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Vantaggi [!DNL Query Service] {#benefits}

Le caratteristiche fornite da [!DNL Query Service] ha molti scopi. Puoi utilizzarla per adattarla a logiche complesse per la segmentazione, per calcolare vari attributi personalizzati da utilizzare a valle o per semplificare notevolmente la creazione dei segmenti.

[!DNL Query Service] consente di includere vincoli nelle query per semplificare il processo di creazione dei segmenti. Ciò migliora la qualità dei dati garantendo che i dati giusti siano idonei per i segmenti e crea un pubblico più preciso. Mantenere la qualità della query consente di ottenere un pubblico accurato e contribuisce all’affidabilità dei dati. Puoi anche salvare il pubblico creando schemi e tabelle personalizzate in base agli attributi derivati dalla query. Puoi abilitare una tabella personalizzata per Profilo e utilizzare questi punti dati per la segmentazione e la personalizzazione. Questa funzione aiuta gli esperti di marketing che desiderano creare un pubblico di tipo &quot;clear&quot; tra le persone.

Inoltre, includendo la logica nella query che soddisfa condizioni ricorrenti o statiche, [!DNL Query Service] estrae il peso di una segmentazione elaborata.

Adobe Experience Platform fornisce un archivio dati e gli strumenti necessari per attivare i tuoi dati in modo efficiente e affidabile. Mantenendo i dati all’interno di Platform, consente di derivare gli attributi durante l’esecuzione di altri processi e elimina la necessità di esportare i dati in strumenti di terze parti per la manipolazione e l’elaborazione. Tali costi comuni di elaborazione possono avere un impatto notevole sulla cronologia di un progetto quando si utilizzano centinaia di attributi o campagne. Questo offre agli addetti al marketing un’unica posizione per accedere ai loro dati e creare campagne, nonché un mezzo molto dinamico per segmentare e personalizzare i loro messaggi.

## Passaggi successivi

Leggendo questo documento, è ora necessario comprendere come [!DNL Query Service] influisce non solo sulla qualità dei dati e sulla facilità di segmentazione, ma anche sulla loro importanza nell’architettura dei dati per l’intero flusso di lavoro end-to-end.

Altri documenti che ti aiuteranno a comprendere [!DNL Query Service] funzioni e utilizzi includono [guida per l’esecuzione delle query](../best-practices/writing-queries.md) e [guida per l’organizzazione delle risorse dati](../best-practices/organize-data-assets.md).

Per esempi SQL più applicabili che utilizzano Adobe Analytics con [!DNL Query Service], vedi [Documentazione sulle query di esempio di Adobe Analytics](../sample-queries/adobe-analytics.md).
