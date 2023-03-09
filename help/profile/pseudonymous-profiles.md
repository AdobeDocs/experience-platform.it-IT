---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;durata;ttl;durata;pseudonimo;profili pseudonimi;scadenza dati;scadenza dati;
solution: Experience Platform
title: Scadenza dati profilo pseudonimo
description: Questo documento fornisce indicazioni generali sulla configurazione della scadenza dei dati per i profili pseudonimi in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 3f776255ca858a86f501fd587c44fe176c45e103
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---


# Scadenza dati profili pseudonimi [!BADGE Versione limitata]

In Adobe Experience Platform, un profilo viene considerato per la scadenza dei dati pseudonimi se soddisfa le seguenti condizioni:

- I tipi di identità del profilo uniti corrispondono a quelli specificati dal cliente come tipo di identità pseudonimo o sconosciuto.
   - Ad esempio, se il tipo di identità del profilo è `ECID`, `GAID`, o `AAID`. Il profilo unito non dispone di ID di altri tipi di identità. In questo esempio, un profilo unito **non** hanno un’identità e-mail o CRM.
- Non è stata eseguita alcuna attività in un periodo di tempo definito dall&#39;utente. L’attività è definita da qualsiasi evento esperienza acquisito o dagli aggiornamenti degli attributi del profilo avviati dal cliente.
   - Ad esempio, un nuovo evento di visualizzazione della pagina o un aggiornamento dell’attributo age è considerato un’attività. Tuttavia, un aggiornamento dell’iscrizione a un segmento non avviato dall’utente è **non** considerata come un’attività. Attualmente, per calcolare la scadenza dei dati, il tracciamento a livello di profilo si basa sul momento dell’acquisizione.

## Accedere ad {#access}

La scadenza dei dati del profilo pseudonimo non può essere configurata tramite l’interfaccia utente o le API di Platform. Per abilitare questa funzione, è necessario contattare il supporto tecnico. Quando si contatta l’assistenza, includere le seguenti informazioni:

- I tipi di identità da considerare per le eliminazioni di profili pseudonimi.
   - Ad esempio: `ECID` solo, `AAID` solo, o una combinazione di `ECID` e `AAID`.
- Quantità di tempo di attesa prima di eliminare un profilo pseudonimo. Il consiglio predefinito per i clienti è di 30 giorni. Tuttavia, questo valore può variare in base al caso d’uso.
- Il conteggio dei profili corrente confrontato con il conteggio dei profili di licenza.

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti relative alla scadenza dei dati dei profili pseudonimi:

### Quali utenti dovrebbero utilizzare la scadenza dei dati dei profili pseudonimi?

- Se utilizzi un connettore che invia direttamente i dati dalla rispettiva origine a Platform.
- Se disponi di un sito web che serve in massa clienti non autenticati.
- Se nei set di dati sono presenti conteggi di profilo eccessivi e hai confermato che tali conteggi sono dovuti a un tipo di identità anonima basata su cookie.
   - Per determinare ciò, è necessario utilizzare il rapporto di sovrapposizione del tipo di identità. Ulteriori informazioni su questo report sono disponibili SUL LINK

### Quali sono alcune avvertenze di cui dovresti essere a conoscenza prima di utilizzare la scadenza dei dati dei profili pseudonimi?

- La scadenza dei dati del profilo pseudonimo verrà eseguita il **produzione** sandbox.
- Dopo aver attivato questa funzione, l’eliminazione dei profili avviene **permanente**. È presente **no** modo per ripristinare o ripristinare i profili eliminati.
- Questo è **non** un processo di pulizia una tantum. La scadenza dei dati del profilo pseudonimo viene continuamente eseguita una volta al giorno ed elimina i profili che corrispondono all’input del cliente.
- **Tutti** I profili definiti come profili pseudonimi saranno interessati dalla scadenza dei dati del profilo pseudonimo. È vero **non** è importante se il profilo è solo Evento esperienza o se contiene solo attributi di profilo.
- Questa pulizia **solo** verificarsi in Profilo. Il servizio Identity può continuare a mostrare le identità eliminate all’interno del grafico dopo la pulizia nei casi in cui al profilo siano associate due o più identità pseudonime (ad esempio `AAID` e `ECID`). Questa discrepanza sarà affrontata nel prossimo futuro.

### In che modo la scadenza dei dati del profilo pseudonimo differisce da quella dei dati Experience Event esistenti?

La scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza sono funzioni complementari.

#### Granularità

La scadenza dei dati di Experience Event funziona su un **set di dati** livello. Di conseguenza, ogni set di dati può avere un’impostazione di scadenza dati diversa.

La scadenza dei dati del profilo pseudonimo funziona su una **sandbox** livello. Di conseguenza, la scadenza dei dati influirà su tutti i profili nella sandbox.

#### Tipi di identità

La scadenza dei dati dell’evento esperienza rimuove gli eventi **solo** in base alla marca temporale del record evento. I tipi di identità inclusi sono **ignorato** a scopo di scadenza.

Scadenza dati profilo pseudonimo **solo** considera i profili con grafici di identità contenenti tipi di identità selezionati dal cliente, ad esempio `ECID`, `AAID`, o altri tipi di cookie. Se il profilo contiene **qualsiasi** tipo di identità aggiuntivo **non** nell’elenco selezionato del cliente, il profilo **non** essere soppressa.

#### Elementi rimossi

Scadenza dati evento esperienza **solo** rimuove eventi e non **non** rimuovere i dati della classe di profilo. I dati della classe profilo vengono rimossi solo quando tutti i dati vengono rimossi in **tutto** set di dati e sono **no** record della classe di profilo rimanenti per il profilo.

La scadenza dei dati del profilo pseudonimo rimuove **entrambi** record di eventi e profili. Di conseguenza, verranno rimossi anche i dati della classe di profilo.

### In che modo la scadenza dei dati di profilo pseudonimo può essere utilizzata insieme alla scadenza dei dati di Experience Event?

La scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza possono essere utilizzate per completarsi a vicenda.

Dovresti **sempre** imposta la scadenza dei dati Experience Event nei set di dati, in base alle tue esigenze di conservazione dei dati sui tuoi clienti noti. Una volta impostata la scadenza dei dati di Experience Event, puoi utilizzare la scadenza dei dati di profilo pseudonimo per rimuovere automaticamente i profili pseudonimi. In genere, il periodo di scadenza dei dati per i profili pseudonimi è inferiore al periodo di scadenza dei dati per gli eventi esperienza.

Per un caso d’uso tipico, puoi impostare la scadenza dei dati Experience Event in base ai valori dei dati utente noti e impostare la scadenza dei dati del profilo pseudonimo su una durata molto più breve per limitare l’impatto dei profili pseudonimi sulla conformità della licenza di Platform.
