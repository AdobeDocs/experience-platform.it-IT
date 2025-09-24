---
keywords: Experience Platform;home;argomenti popolari;schema basato su modello;schema relazionale;schemi relazionali;schema;schema;xdm;experience data model;
solution: Experience Platform
title: Schemi basati su modelli
description: Scopri gli schemi basati su modelli (detti anche schemi relazionali) in Adobe Experience Platform, che includono funzioni, campi obbligatori, relazioni e limitazioni.
badge: Disponibilità limitata
source-git-commit: 192e97c97ffcb2d695bcfa6269cc6920f5440832
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Schemi basati su modelli

>[!AVAILABILITY]
>
>Data Mirror e gli schemi basati su modelli sono disponibili per i titolari di licenze di **Campagne orchestrate** Adobe Journey Optimizer. Sono disponibili anche come **versione limitata** per gli utenti di Customer Journey Analytics, a seconda della licenza e dell&#39;abilitazione della funzione. Contatta il tuo rappresentante Adobe per accedere.

Gli schemi basati su modelli forniscono un modello di modellazione flessibile e controllato per la rappresentazione di dati strutturati nel data lake di Adobe Experience Platform. Supportano le chiavi primarie applicate, le relazioni a livello di schema e il controllo dettagliato sui record, il tutto senza affidarsi a schemi di unione o a sistemi di database relazionali completi.

>[!IMPORTANT]
>
>Le considerazioni sull’eliminazione dei dati si applicano a tutte le implementazioni dello schema basate su modelli. Le applicazioni che utilizzano questi schemi devono comprendere in che modo le eliminazioni influiscono sui set di dati correlati, sui requisiti di conformità e sui processi a valle. Pianifica gli scenari di eliminazione e rivedi [le linee guida sull&#39;igiene dei dati](../../hygiene/ui/record-delete.md#model-based-record-delete) prima dell&#39;implementazione.

>[!NOTE]
>
>Le applicazioni possono fare riferimento agli schemi basati su modelli come &quot;schemi relazionali&quot; quando richiedono la creazione di schemi per casi di utilizzo di modellazione di dati relazionali.

Utilizzare gli schemi basati su modelli per:

* Garantire l&#39;integrità dei dati con chiavi primarie composite o a campo singolo imposte.
* Attivare il rilevamento preciso delle modifiche mediante il controllo delle versioni per gli inserimenti, gli aggiornamenti e le eliminazioni.
* Definisci relazioni riutilizzabili a livello di schema per modellare connessioni di entità nel mondo reale.
* Evita di duplicare le strutture degli schemi tra le applicazioni supportando più modelli di dati.
* Ignora i vincoli dello schema di unione per semplificare l’onboarding, ridurre il gonfiore dello schema ed evitare modifiche indesiderate allo schema.

## Differenze tra gli schemi basati su modelli e gli schemi XDM standard

Gli schemi XDM standard in Experience Platform seguono uno dei tre comportamenti di dati seguenti: Record, Serie temporali o Ad hoc. Per definizioni e dettagli, vedi [Comportamenti dei dati XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors).

Nel modello tradizionale, gli schemi record e serie temporali partecipano a [schemi unione](../api/unions.md) (vedi anche la [guida dell&#39;interfaccia utente dello schema unione](../../profile/ui/union-schema.md)). Questi schemi si evolvono automaticamente quando [gruppi di campi](./composition.md#field-group) condivisi vengono aggiornati e i campi personalizzati devono essere nidificati in uno spazio dei nomi tenant. Anche se potente, questo modello può rallentare l’onboarding, produrre schemi eccessivamente complessi con campi non utilizzati e richiedere una mappatura o trasformazione dei dati aggiuntiva. Questi fattori aumentano la curva di apprendimento e il lavoro di manutenzione in corso.

Gli schemi basati su modelli rimuovono le dipendenze dello schema di unione, che eliminano gli aggiornamenti automatici dai gruppi di campi condivisi e consentono le definizioni dirette dei campi senza restrizioni dello spazio dei nomi del tenant. Puoi ottenere un controllo esplicito sulle chiavi primarie, sulle relazioni e sulla progettazione dello schema iniziale, semplificando il modello dei dati in base alle tue esigenze al momento della creazione.

## Caratteristiche degli schemi basati su modelli

Utilizza le seguenti funzionalità per modellare i dati strutturati nel data lake mantenendo al contempo governance, integrità e interoperabilità.

* **Supporto del comportamento dello schema**: configurare con:
   * **Comportamento record**: acquisisce lo stato corrente di un&#39;entità, ad esempio un cliente, un account o una campagna.
   * **Comportamento della serie temporale**: acquisisce gli eventi e il momento in cui si verificano, utile per tenere traccia di sequenze o modifiche nel tempo.
* **Applicazione della chiave primaria**: definisci una chiave primaria per identificare in modo univoco ogni record e impedire duplicati durante l&#39;acquisizione.
* **Controllo versione**: utilizzare un **identificatore versione** (descrittore) per assicurarsi che gli aggiornamenti vengano applicati nell&#39;ordine corretto, anche se i record arrivano fuori sequenza.
* **Mappatura relazioni**: creare relazioni uno-a-uno o molti-a-uno tra schemi basati su modelli o tra schemi basati su modelli e schemi standard. Le definizioni delle relazioni vengono memorizzate come descrittori per consentire join efficienti.
* **Evoluzione semplificata**: gli schemi basati su modelli non partecipano alle visualizzazioni unione e non vengono aggiornati quando i gruppi di campi condivisi cambiano, impedendo modifiche a valle impreviste.
* **Definizione di campo flessibile**: aggiungere campi direttamente senza spazio dei nomi dell&#39;ID tenant. Gli schemi basati su modelli non supportano gruppi di campi XDM.
* **Nessuna dipendenza da schemi di unione**: migliora le prestazioni delle query e riduce il sovraccarico operativo della gestione delle visualizzazioni schema globali.
* **Ordinamento evento-ora**: per gli schemi di serie temporali, utilizza un **identificatore marca temporale** per ordinare gli eventi in base al tempo di occorrenza anziché al tempo di acquisizione.

## Campi obbligatori

Gli schemi basati su modelli richiedono determinati descrittori, ovvero metadati nella definizione dello schema che controlla i comportamenti e i vincoli chiave. Aggiungi i seguenti descrittori come parte della definizione dello schema.

### Descrittore della chiave primaria

Utilizzare un descrittore di chiave primaria per garantire che ogni record sia identificabile in modo univoco. Le configurazioni supportate sono:

* **Chiave primaria a campo singolo**: utilizzare un campo con un valore univoco per ogni record.
* **Chiave primaria composita**: utilizzare più campi per creare un identificatore univoco. Per gli schemi di serie temporali, la chiave composita deve includere il campo timestamp identificato dal descrittore timestamp.

>[!NOTE]
>
>Nell&#39;Editor schema dell&#39;interfaccia utente, i descrittori di versione e di marca temporale vengono visualizzati rispettivamente come &quot;[!UICOTRNOL Identificatore versione]&quot; e &quot;[!UICOTRNOL Identificatore marca temporale]&quot;.

**Esempio (campo singolo):**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Esempio (composito per serie temporali)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Descrittore della versione (identificatore)

Definisci un descrittore di versione (identificatore) per mantenere lo stato del record corretto e garantire che venga applicato l’ultimo aggiornamento. Quando più record condividono la stessa chiave primaria, il record con il valore di versione più alto viene considerato il più recente.

**Esempio:**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Descrittore marca temporale (identificatore)

Per gli schemi di serie temporali, definisci un descrittore (identificatore) di marca temporale per impostare l’ora dell’evento per l’ordine.

**Esempio:**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>I descrittori fanno parte dei metadati di definizione dello schema e non sono memorizzati nelle righe di dati.

Per istruzioni sulla creazione di descrittori nell&#39;Editor schemi, vedere [Creare descrittori nell&#39;Editor schemi](../tutorials/relationship-ui.md). Per la creazione basata su API, vedere [Creare descrittori utilizzando l&#39;API](../tutorials/relationship-api.md).

## Supporto delle relazioni {#relationship-support}

La modellazione di dati relazionali è un utilizzo principale degli schemi basati su modelli. I casi di utilizzo delle applicazioni possono anche fare riferimento a questi schemi come &quot;schemi relazionali&quot;. I descrittori di relazione abilitano queste connessioni collegando i set di dati tra schemi senza incorporare chiavi esterne nelle righe di dati. Migliorano l’integrità referenziale, abilitano modelli di modellazione riutilizzabili e supportano le query connesse tra le applicazioni.

Crea descrittori di relazione a livello di schema per la risoluzione dinamica in fase di query. I valori di cardinalità (1:1, molti a uno) forniscono indicazioni ma non applicano vincoli durante l’acquisizione, supportando la modellazione flessibile dei dati tra set di dati connessi.

Prima di aggiungere i descrittori di relazione, determinare il tipo e la destinazione appropriati:

* **Uno a uno** - Ogni record nello schema di origine corrisponde al massimo a un record nello schema di destinazione.
* **Molti a uno** - Più record nello schema di origine possono fare riferimento allo stesso record nello schema di destinazione.

>[!NOTE]
>
>È possibile definire relazioni tra due schemi basati su modello o tra uno schema basato su modello e uno schema standard. Le relazioni con schemi ad hoc non sono supportate.

<!-- Q) 
Madeline commented: "model-based schema to standard might only be offered for b2b customers; that's how it will be on the UI" - is that still accurate? -->

**Esempio: relazione uno-a-uno**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

<!-- Q) 
Should these be `@type: "xdm:descriptorRelationship",` This could be a copy-pasting error? -->

**Esempio: relazione molti-a-uno**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

Per un elenco dei tipi e della sintassi dei descrittori di relazione, vedere il riferimento all&#39;API [descriptors](../api/descriptors.md).Per informazioni su come applicare questi concetti nella pratica, seguire le esercitazioni per [definire una relazione nell&#39;API](../tutorials/relationship-api.md) o [creare una relazione nell&#39;interfaccia utente](../tutorials/relationship-ui.md).

>[!NOTE]
>
>Poiché le relazioni sono definite a livello di schema, assicurati di unire in modo esplicito i set di dati correlati nelle query. Utilizza uno strumento come Data Distiller per risolvere queste relazioni durante il tempo di query.

>[!IMPORTANT]
>
>La cardinalità di relazione è informativa e non viene applicata durante l’acquisizione. Viene applicata solo durante la risoluzione delle relazioni durante la query o l&#39;analisi. Non fare affidamento sulle impostazioni di cardinalità per convalidare i dati durante l’acquisizione. Controlla e pulisci i dati e assicurati che le regole di relazione definite corrispondano al modo in cui intendi eseguire query o analizzare i dati.

>[!NOTE]
>
> Gli schemi basati su modelli possono collegarsi a schemi standard, ma non a schemi ad hoc.

## Considerazioni sull’eliminazione dei dati e sull’igiene {#data-hygiene-support}

Gli schemi basati su modelli consentono eliminazioni precise a livello di record con implicazioni universali per tutte le applicazioni e i casi d’uso. I descrittori di chiave primaria, versione e marca temporale forniscono la base per l’identificazione accurata dei record durante le operazioni di eliminazione.

### Impatto dell’eliminazione universale

Tutte le applicazioni che utilizzano schemi basati su modelli devono considerare:

* **Integrità referenziale**: le eliminazioni possono influire sui record correlati tra i set di dati connessi
* **Requisiti di conformità**: alcuni settori richiedono comportamenti di eliminazione e audit trail specifici
* **Comportamento dell&#39;applicazione**: i sistemi a valle potrebbero dover gestire in modo appropriato gli eventi di eliminazione
* **Coerenza dei dati**: i set di dati correlati devono mantenere la coerenza durante le operazioni di eliminazione
* **Pianificazione dell&#39;eliminazione**: tenere conto degli impatti a valle su tutti i set di dati e le applicazioni connessi durante la fase di progettazione

Per istruzioni sull&#39;implementazione, vedere [Eliminazione di record dai set di dati basati su modelli](../../hygiene/ui/record-delete.md#model-based-record-delete).

## Limitazioni e considerazioni {#limitations}

Esamina le seguenti limitazioni prima di utilizzare gli schemi basati su modelli:

* Gli schemi basati su modelli non partecipano agli schemi di unione.
* L’evoluzione dello schema è manuale; non viene aggiornata automaticamente quando cambiano i gruppi di campi.

>[!IMPORTANT]
>
>L’evoluzione dello schema diventa limitata dopo che un set di dati è stato inizializzato utilizzando lo schema. Pianifica in anticipo i nomi e i tipi di campo: una volta acquisiti i dati, non è più possibile eliminare o modificare i campi.

* Le relazioni sono limitate a uno a uno e a molti a uno.
* La disponibilità dipende dall’abilitazione della licenza o della funzione.
* Le chiavi primarie composite sono necessarie per gli schemi di serie temporali.

