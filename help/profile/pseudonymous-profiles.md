---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;ora di vita;ttl;time-to-live;pseudonimo;profili pseudonimi;scadenza dati;scadenza;
solution: Experience Platform
title: Scadenza dei dati del profilo
description: Questo documento fornisce indicazioni generali sulla configurazione della scadenza dei dati per i profili Pseudonimi all’interno di Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 07ed7eb9644b2e8cc4da02743c48037afc247614
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Scadenza dati dei profili pseudonimi

In Adobe Experience Platform, puoi configurare i tempi di scadenza per i profili Pseudonimi, consentendo di rimuovere automaticamente dall’archivio profili i dati non più validi o utili per i casi d’uso.

## Profilo pseudonimo {#pseudonymous-profile}

Un profilo viene considerato per la scadenza di dati Pseudonimi se soddisfa le seguenti condizioni:

- I namespace di identità del profilo unione corrispondono a quello specificato dal cliente come spazio dei nomi di identità pseudonimo o sconosciuto.
   - Ad esempio, se lo spazio dei nomi di identità del profilo è `ECID`, `GAID`oppure `AAID`. Il profilo vincolato non dispone di ID da alcun altro namespace Identity. In questo esempio, un profilo con unione fa **not** avere un&#39;identità e-mail o CRM.
- Nessuna attività ha avuto luogo in un periodo di tempo definito dall&#39;utente. L’attività è definita da qualsiasi evento esperienza acquisito o dagli aggiornamenti degli attributi del profilo avviati dal cliente.
   - Ad esempio, un nuovo evento di visualizzazione della pagina o l’aggiornamento dell’attributo dell’età è considerato un’attività. Tuttavia, un aggiornamento dell’appartenenza a un segmento non avviato dall’utente è **not** considerata un’attività . Al momento, per calcolare la scadenza dei dati, il tracciamento a livello di profilo è basato sul momento dell’evento per gli eventi di esperienza e sull’ora dell’acquisizione per gli attributi di profilo.

## Accedere ad {#access}

La scadenza dei dati del profilo pseudonimo non può essere configurata tramite l’interfaccia utente o le API di Platform. Per abilitare questa funzione, contatta invece il supporto . Quando contatti il supporto, includi le seguenti informazioni:

- Gli spazi dei nomi di identità da considerare per le eliminazioni di profili Pseudonimi.
   - Ad esempio: `ECID` solo `AAID` o una combinazione di `ECID` e `AAID`.
- Tempo di attesa prima di eliminare un profilo pseudonimo. Il consiglio predefinito per i clienti è 14 giorni. Tuttavia, questo valore può variare a seconda del caso d’uso.

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti sulla scadenza dei dati dei profili Pseudonimi:

### In che modo la scadenza dei dati del profilo Pseudonimo differisce dalla scadenza dei dati di Experience Event?

La scadenza dei dati Pseudonimi dei profili e la scadenza dei dati Experience Event sono caratteristiche complementari.

#### Granularità

La scadenza dei dati del profilo pseudonimo funziona su un **sandbox** livello. Di conseguenza, la scadenza dei dati influenzerà tutti i profili nella sandbox.

La scadenza dei dati dell’evento esperienza funziona su un **set di dati** livello. Di conseguenza, ogni set di dati può avere un’impostazione di scadenza dei dati diversa.

#### Tipi di identità

Scadenza dei dati del profilo **only** considera i profili con grafici di identità contenenti spazi dei nomi di identità selezionati dal cliente, ad esempio `ECID`, `AAID`o altri tipi di cookie. Se il profilo contiene **qualsiasi** spazio dei nomi di identità aggiuntivo **not** nell’elenco selezionato del cliente, il profilo **not** essere soppressa.

La scadenza dei dati dell’evento esperienza rimuove gli eventi **only** in base alla marca temporale del record dell&#39;evento. Gli spazi dei nomi delle identità inclusi sono **ignorato** a fini di scadenza.

#### Elementi rimossi

La scadenza dei dati del profilo pseudonimo rimuove **entrambi** record evento e profilo. Di conseguenza, verranno rimossi anche i dati della classe di profilo.

Scadenza dati evento esperienza **only** rimuove eventi e esegue **not** rimuovere i dati della classe di profilo. I dati della classe di profilo vengono rimossi solo quando tutti i dati vengono rimossi **tutto** set di dati e sono disponibili **no** record della classe di profilo rimanenti per il profilo.

### Come può essere utilizzata la scadenza dei dati del profilo Pseudonimo insieme alla scadenza dei dati di Experience Event?

La scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza possono essere utilizzati per completarsi a vicenda.

Dovrebbe **sempre** imposta la scadenza dei dati Experience Event nei set di dati in base alle tue esigenze di conservazione dei dati sui clienti noti. Una volta impostata la scadenza dei dati di Experience Event, puoi utilizzare la scadenza dei dati di profilo Pseudonimo per rimuovere automaticamente i profili Pseudonimi. In genere, il periodo di scadenza dei dati per i profili pseudonimi è inferiore al periodo di scadenza dei dati per gli eventi di esperienza.

Per un caso d’uso tipico, puoi impostare la scadenza dei dati dell’Experience Event in base ai valori dei tuoi dati utente noti e impostare la scadenza dei dati del profilo Pseudonimo su una durata molto più breve per limitare l’impatto dei profili Pseudonimi sulla conformità della licenza Platform.

### Quali utenti dovrebbero utilizzare la scadenza dei dati dei profili pseudonimi?

- Se utilizzi l’SDK per web per inviare direttamente i dati a Platform.
- Se hai un sito web che serve in massa clienti non autenticati.
- Se nei set di dati sono presenti conteggi di profilo eccessivi e hai confermato che questo conteggio eccessivo di profili è dovuto allo spazio dei nomi di identità anonimo basato su cookie.
   - Per determinarlo, utilizza il rapporto di sovrapposizione dello spazio dei nomi identità. Ulteriori informazioni su questo rapporto sono disponibili nella sezione [sezione report di sovrapposizione identità](./api/preview-sample-status.md#identity-overlap-report) della guida API di stato dell’anteprima di esempio.

### Quali sono alcune avvertenze di cui dovresti essere a conoscenza prima di utilizzare la scadenza dei dati dei profili Pseudonimi?

- La scadenza dei dati di profilo pseudonimi verrà eseguita il **produzione** sandbox.
- Dopo aver attivato questa funzione, l’eliminazione dei profili è **permanente**. C&#39;è **no** modo per ripristinare o ripristinare i profili eliminati.
- Questo è **not** un lavoro di pulizia una tantum. La scadenza dei dati di profilo pseudonimi viene eseguita continuamente una volta al giorno ed elimina i profili che corrispondono all’input del cliente.
- **Tutto** i profili definiti come profili Pseudonimi saranno interessati dalla scadenza dei dati di profilo Pseudonimi. Lo fa **not** ha importanza se il profilo è solo Experience Event o se contiene solo attributi di profilo.
- Questa pulizia **only** si verifica in Profilo. Il servizio Identity può continuare a mostrare le identità eliminate all’interno del grafico dopo la pulizia, nei casi in cui il profilo abbia due o più identità pseudonime associate (ad esempio `AAID` e `ECID`). Questa discrepanza verrà affrontata nel prossimo futuro.

