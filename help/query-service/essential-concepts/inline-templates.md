---
title: Modelli in linea
description: Scopri come riutilizzare più condizioni in numerose query con modelli in linea.
source-git-commit: e9deabe1e0514f44be085e558fd2fdbf54956f3e
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Modelli in linea

I modelli in linea consentono di riutilizzare più condizioni in numerose query. È possibile salvare i criteri in un modello e quindi riutilizzarli in più query. I modelli SQL riutilizzabili riducono le attività di sviluppo e il rischio di errori nella copia di istruzioni lunghe tra le query. Con i modelli in linea, è possibile apportare modifiche in una posizione e far sì che tali modifiche vengano applicate a qualsiasi query che fa riferimento a questo modello.

Questo documento descrive l’utilizzo e le limitazioni dei modelli in linea all’interno dell’editor delle query.

## Prerequisiti

I modelli in linea sono supportati sia dall’interfaccia utente che dall’API Query Service. Prima di continuare con questa guida, consulta la documentazione su come [creare un modello di query tramite l’API](../api/query-templates.md#create-a-query-template) o con [Editor query](../ui/user-guide.md#query-authoring).

## Sintassi del modello in linea {#syntax}

Una volta salvata, una query viene definita modello. Quando il modello fa riferimento a un altro modello all’interno dell’istruzione, viene denominato modello in linea. I modelli in linea sono indicati nel codice SQL utilizzando il simbolo hash (#) seguito dal nome del modello. Un esempio di questa sintassi è `#YOUR_TEMPLATE_NAME`.

## Caso d’uso {#use-case}

I seguenti modelli SQL dimostrano l’utilità dei modelli in linea, con un esempio per contare il numero di clienti statunitensi da qualsiasi area geografica che hanno speso più del &quot;ricavo massimo&quot; e hanno ordinato prima di giugno 2023. Il vantaggio del modello in linea è che è possibile modificare facilmente il modello figlio (in questo caso il ricavo massimo e la data dell’ordine) e non dover modificare il modello padre.

**Esempio**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Durante l’esecuzione della query, Query Service sostituisce il nome del modello a partire dal simbolo hash con l’istruzione SQL del modello denominato.

>[!NOTE]
>
>I modelli di query possono richiamare qualsiasi numero di altri modelli in linea. Non esiste alcuna restrizione al numero di modelli in linea che è possibile richiamare da una singola query. I modelli possono essere nidificati anche all’interno di altri modelli in linea.

È possibile utilizzare i modelli per memorizzare una o più condizioni. Non è necessario che siano query complete di per sé. Se il modello contiene una query valida, è possibile eseguirla semplicemente chiamando il nome del modello preceduto da un simbolo hash. Ad esempio, se hai memorizzato `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` come modello denominato `JUNE_2023_LOYALTY_MEMBERS`, il comando  `#JUNE_2023_LOYALTY_MEMBERS;` esegue la query valida contenuta nel modello.

>
>
>Nell’interfaccia utente di Adobe Experience Platform, i modelli in linea sotto forma di query con parametri sono supportati solo a livello principale. Ciò significa che le query con parametri funzionano solo se utilizzate nel modello originale. Il modello figlio deve essere statico e non può avere parametri dinamici. Consulta la [documentazione sulle query con parametri](../ui/parameterized-queries.md) per ulteriori informazioni.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come fare riferimento ad altri modelli all’interno dell’SQL, sia nell’Editor query che tramite l’API Query Service.

Inoltre, dovresti leggere [guida ai blocchi anonimi](./anonymous-block.md), che spiega come ridurre al minimo i costi comuni di sviluppo concatenando una o più istruzioni SQL eseguite in sequenza.
