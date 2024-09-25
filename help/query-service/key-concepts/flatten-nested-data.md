---
keywords: Experience Platform;servizio query;servizio query;strutture dati nidificate;dati nidificati;appiattire;appiattire dati nidificati;
title: Appiattire le strutture di dati nidificati da utilizzare con gli strumenti di business intelligence
description: Questo documento spiega come appiattire gli schemi XDM per tutte le tabelle e le viste durante una sessione quando si utilizzano strumenti BI di terze parti con Query Service.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 5f2b44c364183b7becf69f491b41e9d5558accc2
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Flatten delle strutture di dati nidificate da utilizzare con strumenti BI di terze parti

Adobe Experience Platform Query Service supporta l&#39;impostazione `FLATTEN` per la connessione a un database tramite strumenti BI di terze parti. Questa funzione appiattisce le strutture di dati nidificate negli strumenti di business intelligence di terze parti per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e creare rapporti sui dati.

Molti strumenti di business intelligence come [!DNL Tableau] e [!DNL Power BI] non supportano in modo nativo strutture di dati nidificate. L&#39;impostazione `FLATTEN` elimina la necessità di creare visualizzazioni SQL sui dati per fornire una versione flat o di utilizzare i processi di Query Service `CTAS` o `INSERT INTO` per duplicare i set di dati in versioni flat quando si utilizzano schemi ad hoc.

L&#39;impostazione `FLATTEN` richiama la struttura di ciascun campo foglia nella radice della tabella e assegna al campo un nome che segue quello dello spazio dei nomi originale. Questo consente di utilizzare la notazione del punto per far corrispondere un campo al relativo percorso Experience Data Model (XDM), mantenendo al contempo il contesto del campo.

## Prerequisiti

L&#39;utilizzo dell&#39;impostazione `FLATTEN` richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): una panoramica di alto livello di XDM e della relativa implementazione in Experience Platform.

   * [Creare uno schema ad hoc](../../xdm/tutorials/ad-hoc.md): uno schema XDM con campi a cui viene assegnato un namespace per l&#39;utilizzo solo da un singolo set di dati, viene definito schema ad hoc. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dati, ad Experience Platform per la creazione di alcuni tipi di connessioni sorgente.

* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

* [Strutture di dati nidificate](./nested-data-structures.md): questo documento fornisce esempi di come creare, elaborare o trasformare set di dati con tipi di dati complessi, incluse strutture di dati nidificate.

## Connettersi a un database utilizzando l&#39;impostazione FLATTEN {#connect-with-flatten}

L&#39;impostazione `FLATTEN` appiattisce le strutture di dati nidificate in colonne separate in cui il nome dell&#39;attributo diventa il nome della colonna che contiene i valori di riga. Quando si utilizzano dati in strumenti BI che non supportano strutture di dati nidificate, questa impostazione migliora l’usabilità degli schemi ad hoc e riduce il carico di lavoro necessario.

Quando ci si connette a Query Service con il client di terze parti scelto, aggiungere l&#39;impostazione `FLATTEN` al nome del database. Per informazioni su come connettere uno strumento BI specifico, consultare la relativa documentazione nella [panoramica sulla connessione dei client a Query Service](../clients/overview.md). La stringa di connessione deve contenere:

* Il nome della sandbox.
* Due punti seguiti da `all` o un ID set di dati, un ID visualizzazione o un nome database specifico.
* Un punto interrogativo (?) seguito dalla parola chiave `FLATTEN`.

L’input deve avere il seguente formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Di seguito è riportato un esempio di stringa di connessione:

```terminal
prod:all?FLATTEN
```

## Esempio {#example}

Lo schema di esempio utilizzato in questa guida utilizza il gruppo di campi standard [!UICONTROL Dettagli Commerce], che utilizza la struttura di oggetti `commerce` e l&#39;array `productListItems`. Consulta la documentazione XDM per [ulteriori informazioni sul gruppo di campi [!UICONTROL Dettagli Commerce]](../../xdm/field-groups/event/commerce-details.md). Una rappresentazione della struttura dello schema è visibile nell’immagine seguente.

![Diagramma di schema del gruppo di campi Dettagli di Commerce che include le strutture `commerce` e `productListItems`.](../images/key-concepts/commerce-details.png)

Se lo strumento BI non supporta strutture di dati nidificate, può essere difficile fare riferimento ai campi nidificati se contengono valori serializzati, ad esempio `commerce` e `productListItems` nello schema di esempio. Questi valori possono essere visualizzati come parti di un singolo campo stringa `commerce` codificato e non sono realisticamente inutilizzabili.

I valori seguenti rappresentano `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) e `commerce.purchases.value`(1.0) in campi nidificati con formattazione errata.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Utilizzando l&#39;impostazione `FLATTEN`, è possibile accedere a campi separati all&#39;interno dello schema o a sezioni intere della struttura dati nidificata utilizzando la notazione del punto e il nome del percorso originale. Di seguito è riportato un esempio di questo formato che utilizza il gruppo di campi `commerce`.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

L&#39;impostazione `FLATTEN` presenta alcune limitazioni quando si tratta di altre strutture di dati. I dettagli completi sono forniti nella [sezione limitazioni](#limitations).

### Utilizzare le virgolette per i campi nelle query {#quotation-marks}

I campi radice appiattiti ora utilizzano la notazione del punto per corrispondere ai relativi percorsi XDM. Quando vengono utilizzati in una query, i campi devono essere racchiusi tra virgolette (&quot;&quot;).

L&#39;esempio SQL seguente visualizza lo stato originale della query nidificata:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Quando si utilizzano i campi di dati appiattiti, la query viene scritta utilizzando la notazione del punto e racchiusa tra virgolette, come illustrato di seguito:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limitazioni {#limitations}

L&#39;impostazione `FLATTEN` non appiattisce le seguenti strutture di dati:

| Struttura dei dati | Limitazione |
|---|---|
| Array | Utilizzare un indice di matrice esplicito o la funzione `EXPLODE` per accedere agli array. |
| Mappe | Utilizza la chiave stringa per accedere a un valore sotto una mappa per accedere alle mappe. |

Per risolvere le limitazioni di Map e Array, è necessario utilizzare gli strumenti di BI per la modifica delle istruzioni SQL raw, ad esempio Opzioni avanzate -> Istruzione SQL in Power BI.

Per risolvere le limitazioni relative a mappe e array sono necessari strumenti di business intelligence, ad esempio la modifica delle istruzioni SQL non elaborate. Consulta la guida su come [utilizzare le opzioni avanzate di Power BI per immettere una query SQL personalizzata](../clients/power-bi.md#import-tables-using-custom-sql) nella sezione istruzione SQL.

## Passaggi successivi

Questo documento illustra come appiattire le strutture di dati nidificate da utilizzare con strumenti di business intelligence di terze parti. Se non hai già connesso il client, consulta [la panoramica della connessione client](../clients/overview.md) per un elenco dei client di terze parti supportati.
