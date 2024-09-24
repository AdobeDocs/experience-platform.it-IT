---
title: Metrica volume dati totale
description: Scopri la nuova metrica Volume totale dati e come sostituisce la precedente metrica di ricchezza media di profilo.
hide: true
hidefromtoc: true
source-git-commit: 9aba85d4e5a481b0eff53e1d87311c395934f585
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Metrica del volume totale dei dati

A partire dal 24 settembre 2024, la metrica Volume di dati totale sostituirà la metrica precedente Ricchezza media profilo.

Il volume di dati totale rappresenta la quantità totale di dati disponibili per Adobe Experience Platform Real-Time Customer Profile da utilizzare nei flussi di lavoro di coinvolgimento. Questo valore è equivalente alla metrica Pubblico di riferimento moltiplicata per la Ricchezza media del profilo.

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti su questo aggiornamento.

### Perché è stato fatto questo cambiamento?

Questa modifica è stata apportata per semplificare il processo di conformità alle metriche di adesione alla licenza. Abbiamo spesso sentito dire dai clienti che trovano la Ricchezza media del profilo difficile da capire e da gestire. Con questa modifica, ci auguriamo che tu sia in grado di comprendere e gestire meglio l’utilizzo del Profilo cliente in tempo reale concesso in licenza.

### Questa modifica nella metrica cambia il diritto all’archivio profili?

No. L’adesione all’archivio profili rimarrà invariata, poiché il volume totale di dati equivale al pubblico indirizzabile moltiplicato per la ricchezza media di profilo autorizzata.

### Questa modifica influisce sui pacchetti di adesione acquistati?

No. Potrai ancora usufruire dei vantaggi dei pacchetti di adesione acquistati in precedenza.

### Perché vedo un valore diverso per il volume totale dei dati rispetto al mio diritto all’archivio profili?

Il volume di dati totale rappresenta la quantità **totale** di dati disponibili per il profilo da utilizzare nei flussi di lavoro di coinvolgimento. La misurazione è stata aggiornata per essere più deterministica e spiegabile. La maggior parte degli utenti dovrebbe **non** vedere una modifica significativa tra il volume totale dei dati e l&#39;archiviazione totale dei profili. In caso di dubbi, crea un ticket con il rappresentante del servizio clienti.

### È necessario ricreare le modifiche per continuare a gestire la ricchezza media del profilo?

No. Qualsiasi azione, come filtraggio, disabilitazione del profilo per i set di dati, nonché la configurazione delle scadenze degli eventi esperienza e delle scadenze dei dati del profilo pseudonimo continuerà a svolgere un ruolo nella gestione del volume di dati totale.

### Perché il file che ho acquisito nella sandbox ha una dimensione diversa rispetto al volume totale dei dati?

Il profilo ottimizza i dati per una rapida elaborazione, in modo da eseguire i flussi di lavoro di personalizzazione e coinvolgimento per i quali il sistema è progettato. La dimensione del file sul lato client potrebbe essere diversa dal volume totale dei dati a causa di fattori quali il tipo di codifica, la compressione e il formato.

### Questa modifica si applica agli SKU che hanno un limite condiviso sia per il profilo che per il data lake?

I clienti che utilizzano SKU con profili di Richness medi condivisi tra il profilo e il data lake continueranno a visualizzare la metrica Totale spazio di archiviazione utilizzato e **non** visualizzeranno la metrica Ricchezza media profilo.
