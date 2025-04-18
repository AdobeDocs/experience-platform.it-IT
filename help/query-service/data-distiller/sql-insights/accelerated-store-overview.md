---
title: Panoramica di Accelerated Store
description: Scopri come utilizzare l’archivio accelerato in Adobe Experience Platform per ottenere informazioni rapide e basate su SQL utilizzando i dati aggregati. Questa pagina illustra l’utilizzo previsto, le restrizioni sull’identità e i dati BI e le best practice per garantire la conformità con le policy di governance dei dati di Adobe.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Panoramica più rapida dello store

Lo store accelerato in Adobe Experience Platform è un livello di storage ottimizzato per le prestazioni disponibile attraverso lo SKU di Data Distiller. È progettato per contenere set di dati preaggregati, consentendo insights rapidi basati su SQL e il rendering del dashboard.

Questo documento illustra come utilizzare in modo appropriato lo store accelerato, spiega perché i set di dati aggregati sono esenti dai processi standard di igiene dei dati e sottolinea che i dati di identità non devono essere memorizzati. Per restare conforme alle linee guida di Adobe, devi rispettare i criteri di governance dei dati e le restrizioni di utilizzo descritti in questo documento.

## Funzionalità principali {#key-capabilities}

Lo store accelerato è progettato appositamente per garantire prestazioni ed efficienza. Consente flussi di lavoro semplificati per query e reporting, concentrandosi sui dati aggregati. L’elenco seguente evidenzia le sue funzionalità principali:

- Distribuire dashboard e widget ad alte prestazioni tramite query SQL
- Archivia set di dati preaggregati progettati per informazioni ricorrenti
- Supporto della creazione di modelli di dati personalizzati per la generazione di rapporti sui casi di utilizzo

## Uso previsto {#intended-use}

L&#39;archivio accelerato è progettato **esclusivamente** per l&#39;archiviazione di dati aggregati che consente l&#39;esecuzione di dashboard e visualizzazioni semplificati. La sua architettura non è destinata a supportare carichi di lavoro complessi, come l’elaborazione di business intelligence o il data warehousing.

>[!IMPORTANT]
>
>L&#39;archivio accelerato non sostituisce il data lake o una soluzione di storage generica.

## Limitazioni di utilizzo {#usage-restrictions}

Per garantire la conformità al modello di governance dei dati e ai termini di licenza di Adobe, si applicano le seguenti restrizioni:

- **Non memorizzare dati evento non elaborati**
- **Non archiviare i dati di identità**
- **Non memorizzare informazioni personali (PII)** quali indirizzi e-mail, dati sanitari o identificatori cliente
- **Non utilizzare l&#39;archivio accelerato per replicare l&#39;intero data lake**

Solo i dati aggregati e non identificabili possono essere conservati nell&#39;archivio accelerato. I set di dati aggregati non possono essere decodificati per rivelare i dati di origine originali, il che li rende esenti dai processi centralizzati di igiene dei dati di Experience Platform.

## Governance e conformità {#governance-and-compliance}

L’utilizzo dello store accelerato al di fuori dello scopo previsto potrebbe esporre la tua organizzazione al rischio di violare il contratto di licenza di Adobe e i limiti di governance dei dati. Se si verificano problemi di governance dei dati a causa di modelli di utilizzo non supportati, l’organizzazione si assume la piena responsabilità.

Adobe non è responsabile per eventuali conseguenze derivanti dall’uso improprio di questa funzione.

Per ulteriori informazioni su come gestire i dati in modo responsabile in Experience Platform, consulta [Governance, privacy e sicurezza in Experience Platform](../../../landing/governance-privacy-security/overview.md). Questa pagina illustra i servizi e gli strumenti che consentono di controllare i dati sull’esperienza in conformità con le politiche aziendali, i requisiti legali e gli standard di sviluppo. Per collegamenti a istruzioni più dettagliate sull&#39;etichettatura di utilizzo e sull&#39;applicazione dei criteri, visita la [panoramica sulla governance dei dati](../../../data-governance/home.md).

## Best practice {#best-practices}

Per garantire un utilizzo efficiente e conforme dello store accelerato, segui queste best practice consigliate:

- Utilizzare i set di dati derivati per creare tabelle preaggregate personalizzate in base alle esigenze del dashboard
- Evita di utilizzare l’archivio accelerato come posizione di gestione temporanea o di backup per i set di dati non elaborati
- Rivedi regolarmente il tuo utilizzo per garantire l’allineamento con i guardrail consigliati da Adobe

## Passaggi successivi

Dopo aver letto questo documento, hai imparato cos’è l’archivio accelerato, il suo utilizzo previsto per i dati aggregati negli scenari di reporting e le regole di governance da seguire per garantire un utilizzo conforme. Per approfondire la comprensione e applicare queste linee guida in modo efficace, esplora le risorse seguenti:

- [Panoramica di SQL Insights](./overview.md): scopri come SQL Insights abilita la generazione di rapporti ottimizzati in base alle prestazioni utilizzando set di dati aggregati.
- [Invia query accelerate](./send-accelerated-queries.md): scopri come eseguire query nell&#39;archivio accelerato su dashboard e widget di alimentazione.
- [Governance e igiene dei dati](../../data-governance/overview.md): rivedi i criteri di igiene dei dati e le linee guida per la governance di Adobe per assicurarne l&#39;utilizzo conforme.
