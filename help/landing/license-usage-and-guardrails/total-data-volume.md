---
title: Metrica volume dati totale
description: Scopri la nuova metrica Volume totale dati e come sostituisce la precedente metrica di ricchezza media di profilo.
exl-id: 4b21d25c-b82b-4d1a-83ce-b510f02fd160
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Metrica del volume totale dei dati

Il volume di dati totale sostituisce la metrica Ricchezza media profilo precedente come modo più semplice e spiegabile per monitorare l’utilizzo rispetto all’adesione all’archivio profili.

**Volume di dati totale = Pubblico indirizzabile × Ricchezza media profilo**

Questa metrica riflette la quantità totale di dati archiviati nell&#39;**archivio profili** e disponibili per l&#39;utilizzo nei flussi di lavoro di coinvolgimento dei clienti in tempo reale. **not** include i dati archiviati nel **data lake**. Questa modifica fornisce una visualizzazione più mirata e trasparente dei dati rilevanti per la personalizzazione e il coinvolgimento basati su profili.

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

### Calcolo del volume totale dei dati Include lo storage Data Lake?

Il volume totale dei dati viene calcolato con la seguente formula:

**Volume di dati totale = Pubblico indirizzabile × Ricchezza media profilo**

Questa metrica riflette la quantità totale di dati memorizzati nell’archivio profili disponibile per Real-Time Customer Profile da utilizzare nei flussi di lavoro di coinvolgimento. **not** include i dati archiviati nel data lake.

In precedenza, alcune offerte legacy utilizzavano una metrica di &quot;archiviazione totale&quot; che combinava l’utilizzo sia dell’archivio profili che del Data Lake. Tuttavia, il volume totale dei dati è limitato solo all’archivio profili, fornendo una visualizzazione più mirata dei dati rilevanti per il coinvolgimento basato sul profilo.

### È necessario ricreare le modifiche per continuare a gestire la ricchezza media del profilo?

No. Qualsiasi azione, come filtraggio, disabilitazione del profilo per i set di dati, nonché la configurazione delle scadenze degli eventi esperienza e delle scadenze dei dati del profilo pseudonimo continuerà a svolgere un ruolo nella gestione del volume di dati totale.

### Perché il file che ho acquisito nella sandbox ha una dimensione diversa rispetto al volume totale dei dati?

Il profilo ottimizza i dati per una rapida elaborazione, in modo da eseguire i flussi di lavoro di personalizzazione e coinvolgimento per i quali il sistema è progettato. La dimensione del file sul lato client potrebbe essere diversa dal volume totale dei dati a causa di fattori quali il tipo di codifica, la compressione e il formato.

### Questa modifica si applica agli SKU che hanno un limite condiviso sia per il profilo che per il data lake?

I clienti che utilizzano SKU con profili di Richness medi condivisi tra il profilo e il data lake continueranno a visualizzare la metrica Totale spazio di archiviazione utilizzato e **non** visualizzeranno la metrica Ricchezza media profilo.
