---
title: Profili Edge
description: Scopri i profili edge, la terminologia correlata, le aree disponibili per i profili edge e i servizi disponibili per i profili edge.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Profili Edge

In Adobe Experience Platform, Real-Time Customer Profile è l’unica fonte di verità per i dati delle entità. Questi dati di profilo si trovano in un hub centrale e consentono di gestire i casi d’uso che si basano sulla completezza e sulla completezza dei dati. Tuttavia, in casi di utilizzo più in tempo reale, in cui la sensibilità al tempo è più importante, l’opzione preferita sono i profili edge. I profili Edge sono profili leggeri che si trovano ai margini e aiutano nei casi di utilizzo di personalizzazione in tempo reale.

Ad Adobe, applicazioni come Adobe Target, Custom Personalization Destination e Adobe Campaign utilizzano Edge per fornire ai clienti esperienze personalizzate in tempo reale. I dati vengono instradati a uno spigolo da una proiezione, con una destinazione di proiezione che definisce lo spigolo a cui verranno inviati i dati.

## Terminologia {#terminology}

Quando lavorate con gli spigoli, assicuratevi di comprendere i seguenti concetti:

- **Edge**: un server perimetrale è un server posizionato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni.
- **Proiezione Edge**: una proiezione Edge è la visualizzazione di proiezione di sistema del profilo su un perimetro specifico per rappresentare i dati del profilo con un ID univoco conforme a uno schema specifico per un cliente specifico. Ad esempio, un&#39;entità che rispetta lo schema del profilo con ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visitatore del sito Web Luma, replicato nel data center VA6, contenente i campi `age = 35` e `gender = male`.

In altri termini, i dati vengono instradati a un perimetro da una proiezione, con la **destinazione della proiezione** che definisce **quale** perimetro a cui verranno inviati i dati.

## Aree geografiche disponibili {#regions}

Le seguenti aree sono disponibili per l’utilizzo con Edge:

- VA6
- OR2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Tutte queste aree sono opzioni valide in cui i profili possono arrivare.

## Servizi disponibili {#services}

I seguenti servizi sono abilitati per la ricerca profilo all’edge:

- [Servizio di lavoro proiezione](#mepw)
- [Servizio di profilo rapido](#xps)

### Servizio di lavoro proiezione {#mepw}

Il Servizio di lavoro di proiezione (MEPW) monitora le modifiche che si verificano sull’hub sui profili. Dopo aver esaminato le modifiche nelle configurazioni, questo servizio prepara le proiezioni e le invia alle aree edge precedentemente specificate. Inoltre, questo servizio elabora le richieste di aggiornamento delle entità e invia le proiezioni richieste alle aree necessarie. Gli aggiornamenti delle entità vengono utilizzati per garantire che l’entità sia accessibile con elevata disponibilità.

### Servizio di profilo rapido {#xps}

Il servizio XPS (Express Profile Service) recupera i profili sui diversi bordi. Questo servizio riceve richieste da soluzioni downstream, come destinazioni Adobe Target o Personalization personalizzate, cerca i profili dai database ai bordi e invia il profilo richiesto alla soluzione richiedente. Se il profilo non viene trovato, viene inviata una richiesta di aggiornamento all’hub associato.

## Passaggi successivi

Dopo aver letto questa guida, avrai acquisito una conoscenza di base dei profili edge, comprese informazioni sulle aree geografiche e sui servizi disponibili per i profili edge. Per ulteriori informazioni su Adobe Experience Edge, consulta la [panoramica dell&#39;Edge Network](../web-sdk/home.md#edge-network).

## Appendice

Nella sezione seguente sono elencate le domande frequenti relative ai profili edge:

### In quali aree possono arrivare i profili edge?

I profili Edge possono arrivare in diverse aree geografiche a seconda della situazione.

Inoltre, ogni profilo edge dispone di un attributo di schema denominato Area attività utente (UAR). In questo attributo di profilo sono elencati tutti i bordi visitati da questo profilo negli ultimi 14 giorni. Di conseguenza, quando questo attributo è presente in un profilo, tutte le modifiche apportate al profilo vengono inviate anche a tutte le aree elencate nell’UAR.

### Come funzionano le scadenze dei dati con i profili edge?

Per i profili edge, la scadenza dei dati determina per quanto tempo il profilo rimarrà sul bordo prima di essere rimosso. La scadenza dei dati è **continua**, il che significa che ogni volta che si accede al profilo su Edge, la data di scadenza dei dati viene ripristinata. Per impostazione predefinita, la scadenza dei dati dura 14 giorni.

### Quali dati vengono memorizzati sul profilo Edge?

Il profilo Edge memorizza gli attributi del profilo, gli ID profilo e gli ID di pubblico qualificati. Per impostazione predefinita, la scadenza dei dati dura 14 giorni.
