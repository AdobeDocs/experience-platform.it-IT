---
title: Panoramica delle regole di collegamento del grafico delle identità
description: Scopri le regole di collegamento del grafico identità in Identity Service.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 67b08acaecb4adf4d30d6d4aa7b8c24b30dfac2e
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 1%

---

# Panoramica delle regole di collegamento del grafico delle identità

>[!AVAILABILITY]
>
>Questa funzione non è ancora disponibile; il programma beta per le regole di collegamento del grafo delle identità dovrebbe iniziare a luglio per le sandbox di sviluppo. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione.

## Sommario 

* [Panoramica](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Scenari di esempio](./example-scenarios.md)

Con il servizio Adobe Experience Platform Identity e il profilo cliente in tempo reale, è facile presumere che i dati siano acquisiti perfettamente e che tutti i profili uniti rappresentino una singola persona tramite un identificatore di persona, ad esempio un ID del sistema di gestione delle relazioni con i clienti. Tuttavia, esistono scenari possibili in cui alcuni dati potrebbero tentare di unire più profili disparati in un unico profilo (&quot;compressione del grafico&quot;). Per evitare queste unioni indesiderate, puoi utilizzare le configurazioni fornite tramite le regole di collegamento del grafico delle identità e consentire una personalizzazione accurata per i tuoi utenti.

## Scenari di esempio in cui potrebbe verificarsi una compressione del grafico

* **Dispositivo condiviso**: per dispositivo condiviso si intendono i dispositivi utilizzati da più utenti. Alcuni esempi di dispositivi condivisi sono tablet, computer di libreria e chioschi.
* **Numeri e-mail e di telefono non validi**: i numeri di telefono e e-mail non validi si riferiscono agli utenti finali che registrano informazioni di contatto non valide, ad esempio &quot;test<span>@test.com&quot; per l’e-mail e &quot;+1-111-111-1111&quot; per il numero di telefono.
* **Valori di identità errati o errati**: i valori di identità errati o non validi si riferiscono a valori di identità non univoci che potrebbero unire gli ID del sistema di gestione delle relazioni con i clienti. Ad esempio, mentre gli identificatori IDFA devono avere 36 caratteri (32 caratteri alfanumerici e quattro trattini), ci sono scenari in cui un identificatore IDFA con valore di identità &quot;user_null&quot; può essere acquisito. Allo stesso modo, i numeri di telefono supportano solo caratteri numerici, ma è possibile che venga acquisito uno spazio dei nomi telefonico con un valore di identità &quot;non specificato&quot;.

Per ulteriori informazioni sugli scenari di utilizzo per le regole di collegamento del grafico delle identità, consulta il documento su [scenari di esempio](./example-scenarios.md).

## Regole di collegamento del grafo delle identità {#identity-graph-linking-rules}

Con le regole di collegamento del grafico delle identità puoi:

* Crea un singolo grafo di identità/profilo unito per ogni utente configurando spazi dei nomi univoci, che impedirà a due identificatori di persona diversi di unirsi in un unico grafo di identità.
* Associa eventi online autenticati alla persona configurando le priorità

### Terminologia {#terminology}

| Terminologia | Descrizione |
| --- | --- |
| Spazio dei nomi univoco | Uno spazio dei nomi univoco è uno spazio dei nomi delle identità che è stato impostato per essere distinto all’interno del contesto di un grafo delle identità. Puoi configurare uno spazio dei nomi in modo che sia univoco utilizzando l’interfaccia utente. Una volta definito uno spazio dei nomi come univoco, un grafo può avere una sola identità che lo contiene. |
| Priorità dello spazio dei nomi | La priorità dello spazio dei nomi si riferisce all’importanza relativa degli spazi dei nomi rispetto agli altri. La priorità dello spazio dei nomi è configurabile tramite l’interfaccia utente. Puoi classificare gli spazi dei nomi in un dato grafico delle identità. Una volta abilitata, la priorità dei nomi verrà utilizzata in vari scenari, ad esempio per l’input dell’algoritmo di ottimizzazione delle identità e per la determinazione dell’identità primaria dei frammenti di evento esperienza. |
| Algoritmo di ottimizzazione identità | L’algoritmo di ottimizzazione delle identità garantisce che le linee guida create configurando uno spazio dei nomi e priorità dello spazio dei nomi univoci vengano applicate in un dato grafico delle identità. |

### Spazio dei nomi univoco {#unique-namespace}

Puoi configurare uno spazio dei nomi in modo che sia univoco utilizzando l’area di lavoro dell’interfaccia utente per le impostazioni delle identità. In questo modo, informa l’algoritmo di ottimizzazione dell’identità che un dato grafo può avere una sola identità che contiene tale spazio dei nomi univoco. Questo impedisce l’unione di due identificatori di persona diversi all’interno dello stesso grafico.

Considera lo scenario seguente:

* Scott usa un tablet e apre il suo browser Google Chrome per andare a nike<span>.com, dove accede e cerca nuove scarpe da basket.
   * Dietro le quinte, questo scenario registra le seguenti identità:
      * Uno spazio dei nomi e un valore ECID per rappresentare l’utilizzo del browser
      * Uno spazio dei nomi e un valore ID CRM per rappresentare l&#39;utente autenticato (Scott ha effettuato l&#39;accesso con la sua combinazione di nome utente e password).
* Suo figlio Peter usa quindi la stessa tavoletta e anche Google Chrome per andare a nike<span>.com, dove effettua l’accesso con il proprio account per cercare attrezzature per il calcio.
   * Dietro le quinte, questo scenario registra le seguenti identità:
      * Lo stesso spazio dei nomi e valore ECID per rappresentare il browser.
      * Nuovo spazio dei nomi e valore ID CRM per rappresentare l’utente autenticato.

Se l’ID del sistema di gestione delle relazioni con i clienti è stato configurato come spazio dei nomi univoco, l’algoritmo di ottimizzazione delle identità divide gli ID del sistema di gestione delle relazioni con i clienti in due grafici di identità separati, invece di unirli.

Se non configuri uno spazio dei nomi univoco, potresti riscontrare unioni di grafici indesiderate, ad esempio due identità con lo stesso ID del sistema di gestione delle relazioni con i clienti, ma diversi valori di identità (scenari come questi spesso rappresentano due entità persona diverse nello stesso grafico).

Devi configurare uno spazio dei nomi univoco per informare l’algoritmo di ottimizzazione dell’identità in modo da applicare limitazioni ai dati di identità acquisiti in un dato grafo di identità.

### Priorità dello spazio dei nomi {#namespace-priority}

La priorità dello spazio dei nomi si riferisce all’importanza relativa degli spazi dei nomi rispetto agli altri. La priorità dello spazio dei nomi è configurabile tramite l’interfaccia utente e puoi classificare gli spazi dei nomi in un dato grafico delle identità.

Uno dei modi in cui viene utilizzata la priorità dello spazio dei nomi è determinare l’identità primaria dei frammenti di evento esperienza (comportamento dell’utente) sul profilo cliente in tempo reale. Se sono configurate le impostazioni di priorità, l’impostazione di identità primaria su Web SDK non verrà più utilizzata per determinare quali frammenti di profilo sono memorizzati.

Nell’area di lavoro dell’interfaccia utente delle impostazioni delle identità è possibile configurare spazi dei nomi e priorità dello spazio dei nomi univoci. Tuttavia, gli effetti delle loro configurazioni sono diversi:

| | Identity Service | Profilo cliente in tempo reale |
| --- | --- | --- |
| Spazio dei nomi univoco | In Identity Service, l’algoritmo di ottimizzazione delle identità fa riferimento a spazi dei nomi univoci per determinare i dati di identità acquisiti in un dato grafo di identità. | Gli spazi dei nomi univoci non influiscono sul profilo cliente in tempo reale. |
| Priorità dello spazio dei nomi | In Identity Service, per i grafici che hanno più livelli, la priorità dello spazio dei nomi determinerà la rimozione dei collegamenti appropriati. | Quando un evento esperienza viene acquisito in Profilo, lo spazio dei nomi con priorità più elevata diventa l’identità primaria del frammento di profilo. |

* La priorità dello spazio dei nomi non influisce sul comportamento del grafico quando viene raggiunto il limite di 50 identità per grafico.
* **La priorità dello spazio dei nomi è un valore numerico** assegnato a uno spazio dei nomi che ne indica l’importanza relativa. Si tratta di una proprietà di uno spazio dei nomi.
* **L’identità primaria è l’identità in cui è memorizzato un frammento di profilo in base a**. Un frammento di profilo è un record di dati che memorizza informazioni su un determinato utente: attributi (di solito acquisiti tramite record di gestione delle relazioni con i clienti) o eventi (di solito acquisiti da eventi di esperienza o dati online).
* La priorità dello spazio dei nomi determina l’identità primaria dei frammenti dell’evento esperienza.
   * Per i record di profilo, puoi utilizzare l’area di lavoro schemi nell’interfaccia utente di Experienci Platform per definire i campi di identità, inclusa l’identità primaria. Leggi la guida su [definizione dei campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md) per ulteriori informazioni.

Per ulteriori informazioni, consulta la guida su [priorità dello spazio dei nomi](./namespace-priority.md).

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md).
* [Priorità dello spazio dei nomi](./namespace-priority.md).
* [Scenari di esempio per la configurazione delle regole di collegamento del grafico delle identità](./example-scenarios.md).
