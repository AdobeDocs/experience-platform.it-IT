---
keywords: Experience Platform;servizio query;servizio query;strutture dati nidificate;dati nidificati;appiattire;appiattire dati nidificati;
title: Appiattire le strutture di dati nidificati da utilizzare con gli strumenti di business intelligence
description: Questo documento spiega come appiattire gli schemi XDM per tutte le tabelle e le viste durante una sessione quando si utilizzano strumenti BI di terze parti con Query Service.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Flatten delle strutture di dati nidificate da utilizzare con strumenti BI di terze parti

Adobe Experience Platform Query Service supporta `FLATTEN` impostazione per la connessione a un database tramite strumenti BI di terze parti. Questa funzione appiattisce le strutture di dati nidificate negli strumenti di business intelligence di terze parti per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e creare rapporti sui dati.

Molti strumenti BI come [!DNL Tableau] e [!DNL Power BI] non supportano in modo nativo le strutture di dati nidificate. Il `FLATTEN` L&#39;impostazione elimina la necessità di creare viste SQL sopra i dati per fornire una versione semplice o per utilizzare Query Service `CTAS` o `INSERT INTO` processi per duplicare i set di dati in versioni flat quando si utilizzano schemi ad hoc.

Il `FLATTEN` l&#39;impostazione richiama la struttura di ciascun campo foglia nella radice della tabella e assegna al campo un nome successivo a quello dello spazio dei nomi originale. Questo consente di utilizzare la notazione del punto per far corrispondere un campo al relativo percorso Experience Data Model (XDM), mantenendo al contempo il contesto del campo.

## Prerequisiti

Utilizzo di `FLATTEN` L&#39;impostazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): panoramica di alto livello di XDM e della relativa implementazione in Experienci Platform.

   * [Creare uno schema ad hoc](../../xdm/tutorials/ad-hoc.md): schema XDM con campi a cui viene assegnato un nome da utilizzare solo per un singolo set di dati, viene definito schema ad hoc. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dati, ad Experience Platform per la creazione di alcuni tipi di connessioni sorgente.

* [Sandbox](../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

* [Strutture di dati nidificate](./nested-data-structures.md): questo documento fornisce esempi su come creare, elaborare o trasformare set di dati con tipi di dati complessi, comprese le strutture di dati nidificate.

## Connettersi a un database utilizzando l&#39;impostazione FLATTEN {#connect-with-flatten}

Il `FLATTEN` l&#39;impostazione consente di unire le strutture di dati nidificate in colonne separate in cui il nome dell&#39;attributo diventa il nome della colonna che contiene i valori di riga. Quando si utilizzano dati in strumenti BI che non supportano strutture di dati nidificate, questa impostazione migliora l’usabilità degli schemi ad hoc e riduce il carico di lavoro necessario.

Quando ti connetti a Query Service con il client di terze parti scelto, aggiungi `FLATTEN` al nome del database. Per informazioni su come collegare uno specifico strumento BI, consulta la relativa documentazione nel [panoramica sulla connessione dei client a Query Service](../clients/overview.md). La stringa di connessione deve contenere:

* Il nome della sandbox.
* Due punti seguiti da `all` o un ID di set di dati, un ID di visualizzazione o un nome di database specifico.
* Un punto interrogativo (?) seguito da `FLATTEN` parola chiave.

L’input deve avere il seguente formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Di seguito è riportato un esempio di stringa di connessione:

```terminal
prod:all?FLATTEN
```

## Esempio {#example}

Lo schema di esempio utilizzato in questa guida utilizza il gruppo di campi standard [!UICONTROL Dettagli Commerce], che utilizza `commerce` struttura dell&#39;oggetto e `productListItems` array. Consulta la documentazione di XDM per [ulteriori informazioni su [!UICONTROL Dettagli Commerce] gruppo di campi](../../xdm/field-groups/event/commerce-details.md). Una rappresentazione della struttura dello schema è visibile nell’immagine seguente.

![Un diagramma di schema del gruppo di campi Dettagli Commerce che include `commerce` e `productListItems` strutture.](../images/essential-concepts/commerce-details.png)

Se lo strumento BI non supporta strutture di dati nidificate, può essere difficile fare riferimento ai campi nidificati che contengono valori serializzati, ad esempio `commerce` e `productListItems` nello schema di esempio). Questi valori possono essere visualizzati come parti di un&#39;unica codifica `commerce` e non sono realisticamente inutilizzabili.

I seguenti valori rappresentano `commerce.order.priceTotal` (3018.0) `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), e `commerce.purchases.value`(1.0) in campi nidificati in formato non corretto.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Utilizzando il `FLATTEN` impostazione, puoi accedere a campi separati all’interno dello schema o a sezioni intere della struttura dati nidificata utilizzando la notazione del punto e il nome del percorso originale. Un esempio di questo formato utilizzando `commerce` gruppo di campi è riportato di seguito.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

Il `FLATTEN` L&#39;impostazione presenta alcune limitazioni quando si tratta di altre strutture di dati. Per informazioni dettagliate, consulta [sezione limitazioni](#limitations).

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

Il `FLATTEN` L&#39;impostazione non appiattisce le seguenti strutture di dati:

| Struttura dei dati | Limitazione |
|---|---|
| Matrici | Utilizza un indice di array esplicito o `EXPLODE` per accedere agli array. |
| Mappe | Utilizza la chiave stringa per accedere a un valore sotto una mappa per accedere alle mappe. |

Per risolvere le limitazioni di Map e Array, è necessario utilizzare gli strumenti di BI per la modifica delle istruzioni SQL raw, ad esempio Opzioni avanzate -> Istruzione SQL in Power BI.

Per risolvere le limitazioni relative a mappe e array sono necessari strumenti di business intelligence, ad esempio la modifica delle istruzioni SQL non elaborate. Consulta la guida su come [utilizzare le opzioni avanzate Power BI per immettere una query SQL personalizzata](../clients/power-bi.md#import-tables-using-custom-sql) nella sezione istruzione SQL.

## Passaggi successivi

Questo documento illustra come appiattire le strutture di dati nidificate da utilizzare con strumenti di business intelligence di terze parti. Se il client non è già stato connesso, vedere [panoramica della connessione client](../clients/overview.md) per un elenco dei client di terze parti supportati.
