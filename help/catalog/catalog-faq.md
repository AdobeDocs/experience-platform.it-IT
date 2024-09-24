---
keywords: servizio catalogo; domande; domande frequenti; FAQ; FAQ set di dati
title: Domande frequenti
description: Risposte alle domande più frequenti su Adobe Experience Platform Catalog Service e sui set di dati.
source-git-commit: 0bb10754e2f5bc289567368c803d4397cec77bf6
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Domande frequenti {#faq}

Questo documento fornisce le risposte alle domande più frequenti su Adobe Experience Platform Catalog Service e sui set di dati. Per domande e risoluzione dei problemi relativi ad altri servizi Platform, inclusi i problemi riscontrati in tutte le API Platform, consulta la [guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Regole e criteri di conservazione {#retention-policies-and-rules}

### A quali tipi di set di dati è possibile applicare le regole dei criteri di conservazione?

+++Risposta

Puoi impostare criteri di conservazione per i set di dati creati utilizzando la classe XDM di ExperienceEvent. Per Profile Service, i criteri di conservazione possono essere applicati ai set di dati ExperienceEvent solo dopo che sono stati abilitati per Profile.

+++

### Posso impostare diversi criteri di conservazione per il data lake e il servizio profilo?

+++Risposta

Sì, puoi applicare diversi criteri di conservazione per il data lake e il servizio profilo.

+++

## Esecuzione e tempistica del processo di conservazione {#retention-job-execution-and-timing}

### Quando il processo di conservazione dei set di dati eliminerà i dati dai servizi del data lake?

+++Risposta

Le scadenze dei set di dati vengono valutate ed elaborate settimanalmente, eliminando tutti i record scaduti. Un evento è considerato scaduto se è stato acquisito in Platform per più di 30 giorni (data di acquisizione > 30 giorni) e la sua data evento supera il periodo di conservazione definito.

+++

### Quando il processo di conservazione dei set di dati eliminerà i dati dai servizi profilo?

+++Risposta

Una volta impostati i criteri di conservazione, gli eventi esistenti vengono immediatamente eliminati da Platform se la loro marca temporale supera il periodo di conservazione. I nuovi eventi vengono eliminati dopo che il loro timestamp supera il periodo di conservazione.

Ad esempio, se applichi un criterio di scadenza di 30 giorni il 15 maggio, si verifica quanto segue:

- I nuovi eventi ricevono una scadenza di 30 giorni al momento dell’acquisizione.
- Gli eventi esistenti con una marca temporale precedente al 15 aprile vengono eliminati immediatamente.
- Gli eventi esistenti con una marca temporale successiva al 15 aprile scadono 30 giorni dopo la loro marca temporale. Ad esempio, un evento del 18 aprile verrebbe eliminato il 18 maggio.

+++

## Utilizzo e monitoraggio del set di dati

### Come posso verificare l’utilizzo del set di dati corrente?

+++Risposta

Puoi visualizzare le dimensioni di archiviazione più recenti a livello di set di dati nel data lake e nel profilo come metriche separate nella pagina di inventario [!UICONTROL Set di dati]. Puoi anche ordinare le colonne per identificare i set di dati più grandi e garantire l’applicazione dei criteri di conservazione. L’utilizzo a livello di sandbox è disponibile nella dashboard Utilizzo licenze. Per ulteriori informazioni, consulta la [documentazione sull&#39;utilizzo delle licenze](../dashboards/guides/license-usage.md).

+++

### Come posso verificare se il processo di conservazione dei dati ha avuto esito positivo?

+++Risposta

Puoi controllare la marca temporale dell&#39;ultimo processo di conservazione dei dati nell&#39;[interfaccia utente di configurazione conservazione dei set di dati](./datasets/user-guide.md#data-retention-policy) e nella [!UICONTROL pagina inventario dei set di dati]. I rapporti per l’utilizzo storico dei set di dati non sono attualmente disponibili, ma sono pianificati per le versioni future.

+++

## Ripristino dei dati {#data-recovery}

### Posso recuperare i dati eliminati?

+++Risposta

No, una volta applicati i criteri di conservazione, tutti i dati precedenti al periodo di conservazione vengono eliminati definitivamente e non possono essere recuperati.

+++

