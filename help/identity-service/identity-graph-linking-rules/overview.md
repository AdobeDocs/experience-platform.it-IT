---
title: Regole di collegamento del grafico delle identità
description: Scopri le regole di collegamento del grafico delle identità in Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 9243da3ebe5e963ec457da5ae3e300e852787d37
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 4%

---

# Panoramica delle regole di collegamento del grafico delle identità {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Regole di collegamento del grafo delle identità"
>abstract="Per evitare queste unioni indesiderate, puoi utilizzare le configurazioni fornite tramite le regole di collegamento del grafico delle identità e consentire una personalizzazione accurata per i tuoi utenti."

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo delle identità sono attualmente a disponibilità limitata. Contatta il team del tuo account Adobe per informazioni su come accedere alla funzione nelle sandbox di sviluppo.

Con il servizio Adobe Experience Platform Identity e il profilo cliente in tempo reale, è facile presumere che i dati siano acquisiti perfettamente e che tutti i profili uniti rappresentino una singola persona tramite un identificatore di persona, come un CRMID. Tuttavia, esistono scenari possibili in cui alcuni dati potrebbero tentare di unire più profili disparati in un unico profilo (&quot;compressione del grafico&quot;). Per evitare queste unioni indesiderate, puoi utilizzare le configurazioni fornite tramite le regole di collegamento del grafico delle identità e consentire una personalizzazione accurata per i tuoi utenti.

Per ulteriori informazioni sull’utilizzo delle regole di collegamento del grafico delle identità, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops)

## Introduzione

I seguenti documenti sono essenziali per comprendere le regole di collegamento del grafico delle identità.

* [Algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md)
* [Guida all&#39;implementazione](./implementation-guide.md)
* [Esempi di configurazioni del grafico](./example-configurations.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente simulazione grafico](./graph-simulation.md)
* [Interfaccia utente per le impostazioni delle identità](./identity-settings-ui.md)

## Scenari di collasso dei grafici {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Scenari di collasso dei grafici"
>abstract="Ci sono più motivi per cui i grafici potrebbero “collassare” o rappresentare più entità persona."

In questa sezione vengono illustrati scenari di esempio che è possibile prendere in considerazione durante la configurazione delle regole di collegamento del grafico delle identità.

### Dispositivo condiviso

Esistono casi in cui possono verificarsi più accessi su una singola dispositivo:

| Dispositivo condiviso | Descrizione |
| --- | --- |
| Computer e tablet di famiglia | Marito e moglie login entrambi ai rispettivi conti bancari. |
| Chiosco pubblico | I viaggiatori in un aeroporto registrazione di utilizzare il loro ID fedeltà per registrare i bagagli e stampare le carte d&#39;imbarco. |
| Call center | Il personale del call center accede da un unico dispositivo per conto dei clienti che chiamano l&#39;assistenza clienti per risolvere i problemi. |

![A diagram of some common shared devices.](../images/identity-settings/shared-devices.png)

In questi casi, dal punto di vista del grafico, senza limiti abilitati, un singolo ECID sarà collegato a più CRMID.

Con le regole di collegamento del grafico delle identità, puoi:

* Configura l’ID utilizzato per l’accesso come identificatore univoco. Ad esempio, è possibile limitare un grafico a store una sola identità con uno spazio dei nomi CRMID e quindi definire tale CRMID come identificatore univoco di un dispositivo condiviso.
   * In questo modo, puoi evitare che i CRMID vengano uniti dall’ECID.

### Invalid email/phone scenarios

There are also instances of users who provide fake values as phone numbers and/or email addresses when registering. In these cases, if limits are not enabled, then phone/email related identities will end up being linked to multiple different CRMIDs.

![A diagram that represents invalid email or phone scenarios.](../images/identity-settings/invalid-email-phone.png)

With identity graph linking rules, you can:

* Configure either the CRMID, phone number, or email address as the unique identifier and thus limit one person to just one CRMID, phone number, and/or email address associated with their account.

### Valori di identità errati o errati

In alcuni casi, valori di identità errati e non univoci vengono acquisiti nel sistema, indipendentemente dallo spazio dei nomi. Gli esempi includono:

* Namespace IDFA con il valore identità &quot;utente_null&quot;.
   * I valori di identità IDFA devono avere 36 caratteri: 32 caratteri alfanumerici e quattro trattini.
* Spazio dei nomi del numero di telefono con valore di identità &quot;non specificato&quot;.
   * I numeri di telefono non devono contenere caratteri dell&#39;alfabeto.

Queste identità potrebbero portare ai seguenti grafici, in cui più CRMID vengono fusi insieme con l&#39;identità &quot;cattiva&quot;:

![Esempio di grafico di dati di identità con valori di identità errati o non validi.](../images/identity-settings/bad-data.png)

Con le regole di collegamento del grafico di identità è possibile configurare il CRMID come identificatore univoco per evitare il collasso del profilo indesiderato a causa di questo tipo di dati.

## Regole di collegamento del grafo delle identità {#identity-graph-linking-rules}

With Identity graph linking rules you can:

* Crea un singolo grafo di identità/profilo unito per ogni utente configurando spazi dei nomi univoci, che impedirà a due identificatori di persona diversi di unirsi in un unico grafo di identità.
* Associate online, authenticated events to the person by configuring priorities

### Terminologia {#terminology}

| Terminologia | Descrizione |
| --- | --- |
| Spazio dei nomi univoco | Uno spazio dei nomi univoco è uno spazio dei nomi delle identità che è stato impostato per essere distinto all’interno del contesto di un grafo delle identità. Puoi configurare uno spazio dei nomi in modo che sia univoco utilizzando l’interfaccia utente. Una volta definito uno spazio dei nomi come univoco, un grafo può avere una sola identità che lo contiene. |
| Priorità dello spazio dei nomi | La priorità dello spazio dei nomi si riferisce all’importanza relativa degli spazi dei nomi rispetto agli altri. La priorità dello spazio dei nomi è configurabile tramite l’interfaccia utente. Puoi classificare gli spazi dei nomi in un dato grafico delle identità. Una volta abilitata, la priorità dei nomi verrà utilizzata in vari scenari, ad esempio per l’input dell’algoritmo di ottimizzazione delle identità e per la determinazione dell’identità primaria dei frammenti di evento esperienza. |
| Algoritmo di ottimizzazione delle identità | L’algoritmo di ottimizzazione delle identità garantisce che le linee guida create configurando uno spazio dei nomi e priorità dello spazio dei nomi univoci vengano applicate in un dato grafico delle identità. |

### Spazio dei nomi univoco {#unique-namespace}

Puoi configurare uno spazio dei nomi in modo che sia univoco utilizzando l’area di lavoro dell’interfaccia utente per le impostazioni delle identità. In questo modo, informa l’algoritmo di ottimizzazione dell’identità che un dato grafo può avere una sola identità che contiene tale spazio dei nomi univoco. Ciò impedisce l&#39;unione di due identificatori di persona diversi all&#39;interno dello stesso grafico.

Si consideri lo scenario seguente:

* Scott usa un tablet e apre il suo browser Google Effetto cromatura per andare su acme<span>.com, dove accede e cerca nuove scarpe da basket.
   * Dietro le quinte, questo scenario registra le seguenti identità:
      * Uno spazio dei nomi ECID e un valore per rappresentare l&#39;utilizzo del browser
      * Uno spazio dei nomi e un valore CRMID per rappresentare il utente autenticato (Scott ha effettuato l&#39;accesso con il suo nome utente e password combinazione).
* Suo figlio Peter utilizza quindi lo stesso tablet e utilizza anche Google Chrome per visitare il sito acme<span>.com, dove accede con il proprio account per cercare attrezzature per il calcio.
   * Dietro le quinte, questo scenario registra le seguenti identità:
      * Lo stesso spazio dei nomi e valore ECID per rappresentare il browser.
      * Nuovo spazio dei nomi e valore CRMID per rappresentare l’utente autenticato.

Se CRMID è stato configurato come uno spazio dei nomi univoco, l’algoritmo di ottimizzazione delle identità divide i CRMID in due grafici di identità separati, invece di unirli.

Se non si configura uno spazio dei nomi univoco, è possibile che si verifichino fusioni di grafi indesiderate, ad esempio due identità con lo stesso spazio dei nomi CRMID, ma valori di identità diversi (scenari like questi spesso rappresentano due entità diverse nello stesso grafico).

È necessario configurare uno spazio dei nomi univoco per informare l&#39;algoritmo di ottimizzazione delle identità per applicare limitazioni sui dati di identità che vengono inseriti in un determinato grafico dell&#39;identità.

### Priorità dello spazio dei nomi {#namespace-priority}

La priorità degli spazi dei nomi si riferisce all&#39;importanza relativa degli spazi dei nomi l&#39;uno rispetto all&#39;altro. La priorità dello spazio dei nomi è configurabile tramite il interfaccia ed è possibile classificare gli spazi dei nomi in un determinato grafico di identità.

One way in which namespace priority is used is in determining the primary identity of experience event fragments (user behavior) in Real-Time Customer Profile. If priority settings are configured, then the primary identity setting on Web SDK will no longer be used to determine which profile fragments are stored.

Gli spazi dei nomi univoci e le priorità degli spazi dei nomi possono essere configurati nelle impostazioni dell&#39;identità interfaccia&#39;area di lavoro. Tuttavia, gli effetti delle loro configurazioni sono diversi:

| | Identity Service | Profilo cliente in tempo reale |
| --- | --- | --- |
| Spazio dei nomi univoco | In Identity Service l&#39;algoritmo di ottimizzazione delle identità fa riferimento a spazi dei nomi univoci per determinare i dati di identità inseriti in un determinato grafico dell&#39;identità. | Gli spazi di nomi univoci non influiscono sul profilo cliente in tempo reale. |
| Priorità dello spazio dei nomi | In Identity Service, per i grafici con più livelli, la priorità dello spazio dei nomi determinerà la rimozione dei collegamenti appropriati. | Quando un evento esperienza viene acquisito in Profilo, lo spazio dei nomi con priorità più elevata diventa l’identità primaria del frammento di profilo. |

* La priorità dello spazio dei nomi non influisce sul comportamento del grafico quando viene raggiunto il limite di 50 identità per grafico.
* **Namespace priority is a numerical value** assigned to a namespace indicating its relative importance. This is a property of a namespace.
* **L&#39;identità primaria è l&#39;identità in cui viene memorizzato un frammento di** profilo. Un frammento di profilo è un record di dati in cui sono memorizzate informazioni su un determinato utente: attributi (in genere acquisiti tramite record CRM) o eventi (in genere acquisiti da eventi di esperienza o dati online).
* La priorità dello spazio dei nomi determina l&#39;identità primaria per i frammenti di evento esperienza.
   * Per i record di profilo, è possibile utilizzare l&#39;area di lavoro Schemi nel interfaccia Experience Platform per definire i campi di identità, inclusa l&#39;identità primaria. Per ulteriori informazioni, leggere la guida alla [definizione dei campi di identità nell&#39;interfaccia](../../xdm/ui/fields/identity.md) .
* Se un evento esperienza ha due o più identità con la massima priorità dello spazio dei nomi nella identityMap, verrà rifiutato dall&#39;inserimento perché sarà considerato come &quot;dati non validi&quot;. Ad esempio, se la identityMap contiene `{ECID: 111, CRMID: John, CRMID: Jane}`, l&#39;intero evento verrà rifiutato come dati non validi perché implica che l&#39;evento è associato a entrambi `CRMID: John` e `CRMID: Jane` contemporaneamente.

Per ulteriori informazioni, leggi la guida sulla priorità](./namespace-priority.md) dello [spazio dei nomi.

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento dei grafici di identità, consulta la documentazione seguente:

* [Algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md)
* [Guida all’implementazione](./implementation-guide.md)
* [Esempi di configurazioni del grafico](./example-configurations.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente simulazione grafico](./graph-simulation.md)
* [Interfaccia utente per le impostazioni delle identità](./identity-settings-ui.md)
