---
keywords: Experience Platform;servizio query;servizio query;strutture dati nidificate;dati nidificati;appiattito;appiattire dati nidificati;
title: Strutture Di Dati Nidificati Flatten Da Utilizzare Con Gli Strumenti BI
description: Questo documento spiega come appiattire gli schemi XDM per tutte le tabelle e le viste durante una sessione quando si utilizzano strumenti BI di terze parti con Query Service.
source-git-commit: 3c9a1f552760b34bfb2c4246382fcb2d66e563d0
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Strutture di dati nidificate appiattite per l’utilizzo con strumenti BI di terze parti

Adobe Experience Platform Query Service supporta la `FLATTEN` impostazione durante la connessione a un database tramite strumenti BI di terze parti. Questa funzione appiattisce le strutture di dati nidificate in strumenti BI di terze parti per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e creare rapporti sui dati.

Molti strumenti BI come [!DNL Tableau] e [!DNL Power BI] non supportano in modo nativo le strutture dati nidificate. La `FLATTEN` l&#39;impostazione elimina la necessità di creare visualizzazioni SQL sui dati per fornire una versione semplice o per utilizzare Query Service `CTAS` o `INSERT INTO` processi per duplicare i set di dati in versioni piatte quando si utilizzano schemi ad hoc.

La `FLATTEN` richiama la struttura di ciascun campo foglia nella directory principale della tabella e assegna un nome al campo dopo lo spazio dei nomi originale. Questo consente di utilizzare la notazione del punto per far corrispondere un campo al relativo percorso Experience Data Model (XDM) mantenendo il contesto del campo.

## Prerequisiti

Utilizzo della `FLATTEN` l’impostazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): Panoramica di alto livello di XDM e della sua implementazione in Experience Platform.

   * [Creare uno schema ad hoc](../../xdm/tutorials/ad-hoc.md): Uno schema XDM con campi con spazi dei nomi assegnati solo a un singolo set di dati viene definito schema ad hoc. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di inserimento dati, ad Experience Platform per creare determinati tipi di connessioni sorgente.

* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

* [Strutture di dati nidificate](./nested-data-structures.md): Questo documento fornisce esempi su come creare, elaborare o trasformare set di dati con tipi di dati complessi, incluse le strutture di dati nidificate.

## Connettersi a un database utilizzando l&#39;impostazione FLATTEN {#connect-with-flatten}

La `FLATTEN` l’impostazione appiattisce le strutture di dati nidificate in colonne separate in cui il nome dell’attributo diventa il nome della colonna contenente i valori della riga. Quando si utilizzano dati in strumenti BI che non supportano strutture di dati nidificate, questa impostazione migliora l’usabilità degli schemi ad hoc e riduce il carico di lavoro necessario.

Quando ti connetti a Query Service con il client di terze parti scelto, aggiungi la `FLATTEN` impostazione sul nome del database. Per informazioni su come collegare uno specifico strumento BI, consulta la relativa documentazione nella sezione [panoramica di connessione dei client a Query Service](../clients/overview.md). La stringa di connessione deve contenere:

* Nome della sandbox.
* Due punti seguiti da `all` o un ID set di dati specifico, un ID visualizzazione o un nome di database.
* Un punto interrogativo (?) seguito da `FLATTEN` keyword.

L&#39;input deve avere il formato seguente:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Di seguito è riportato un esempio di stringa di connessione:

```terminal
prod:all?FLATTEN
```

## Esempio {#example}

Lo schema di esempio utilizzato in questa guida utilizza il gruppo di campi standard [!UICONTROL Dettagli Commerce], che utilizza `commerce` struttura dell&#39;oggetto e `productListItems` array. Consulta la documentazione XDM per [ulteriori informazioni [!UICONTROL Dettagli Commerce] gruppo di campi](../../xdm/field-groups/event/commerce-details.md). Nell’immagine seguente è possibile vedere una rappresentazione della struttura dello schema.

![Diagramma dello schema del gruppo di campi Dettagli commerciali, tra cui `commerce` e `productListItems` strutture.](../images/best-practices/final-subscription-schema.png)

Se lo strumento BI non supporta le strutture di dati nidificate, può essere difficile fare riferimento ai campi nidificati se contengono valori seriali (ad esempio `commerce` e `productListItems` nello schema di esempio). Questi valori possono apparire come parti di un singolo codificato `commerce` campo stringa e non sono realisticamente inutilizzabili.

I seguenti valori rappresentano `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) e `commerce.purchases.value`(1.0) in campi nidificati in formato non corretto.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Utilizzando `FLATTEN` è possibile accedere a campi separati all’interno dello schema o a intere sezioni della struttura dati nidificata utilizzando la notazione del punto e il relativo percorso originale. Un esempio di questo formato che utilizza `commerce` di seguito è riportato un gruppo di campi.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

La `FLATTEN` l’impostazione presenta alcune limitazioni quando si tratta di altre strutture di dati. I dettagli completi sono forniti nella sezione [sezione sulle limitazioni](#limitations).

### Usa virgolette per i campi nelle query {#quotation-marks}

I campi principali appiattiti ora utilizzano la notazione del punto per corrispondere ai rispettivi percorsi XDM. Se utilizzati in una query, i campi devono essere racchiusi tra virgolette (&quot; &quot;).

Nell&#39;esempio SQL seguente viene visualizzato lo stato originale della query nidificata:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Quando si utilizzano i campi dati appiattiti, la query viene scritta utilizzando la notazione del punto e racchiusa tra virgolette come illustrato di seguito:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limitazioni  {#limitations}

La `FLATTEN` al momento l’impostazione non appiattisce le seguenti strutture di dati:

| Struttura dati | Limitazione |
|---|---|
| Matrici | Utilizzare un indice di matrice esplicito o `EXPLODE` per accedere agli array. |
| Mappe | Utilizza la chiave stringa per accedere a un valore sotto una mappa per accedere alle mappe. |

Per risolvere i limiti di Mappa e Array è necessario utilizzare la modifica SQL grezza degli strumenti BI, come Opzioni avanzate -> Istruzione SQL in Power BI.

Gli strumenti BI, come la modifica non elaborata di SQL, sono necessari per risolvere i limiti sia della mappa che della matrice. Consulta la guida su come [utilizzare le opzioni avanzate di Power BI per immettere una query SQL personalizzata](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html#import-tables-using-custom-sql) nella sezione Istruzione SQL.

## Passaggi successivi

Questo documento illustra come appiattire le strutture di dati nidificate da utilizzare con strumenti BI di terze parti. Se il client non è già stato connesso, consulta [panoramica della connessione client](../clients/overview.md) per un elenco dei client di terze parti supportati.
