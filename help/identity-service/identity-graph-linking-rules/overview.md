---
title: Panoramica delle regole di collegamento del grafico delle identità
description: Scopri le regole di collegamento del grafico identità in Identity Service.
hide: true
hidefromtoc: true
badge: Alpha
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: f21b5519440f7ffd272361954c9e32ccca2ec2bc
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---

# Panoramica delle regole di collegamento del grafico delle identità

>[!IMPORTANT]
>
>Le regole di collegamento del grafo delle identità sono attualmente in Alpha. La funzione e la documentazione sono soggette a modifiche.

## Sommario 

* [Panoramica](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Scenari di esempio](./example-scenarios.md)

Con il servizio Adobe Experience Platform Identity e il profilo cliente in tempo reale, è facile presumere che i dati siano acquisiti perfettamente e che tutti i profili uniti rappresentino una singola persona tramite un identificatore di persona, ad esempio un ID del sistema di gestione delle relazioni con i clienti. Tuttavia, esistono scenari possibili in cui alcuni dati potrebbero tentare di unire più profili diversi in un unico profilo (&quot;compressione del profilo&quot;). Per evitare queste unioni indesiderate, puoi utilizzare le configurazioni fornite tramite le regole di collegamento del grafico delle identità e consentire una personalizzazione accurata per i tuoi utenti.

## Scenari di esempio in cui potrebbe verificarsi un collasso del profilo

* **Dispositivo condiviso**: per dispositivo condiviso si intendono i dispositivi utilizzati da più utenti. Alcuni esempi di dispositivi condivisi sono tablet, computer di libreria e chioschi.
* **Numeri e-mail e di telefono non validi**: i numeri di telefono e e-mail non validi si riferiscono agli utenti finali che registrano informazioni di contatto non valide, ad esempio &quot;test<span>@test.com&quot; per l’e-mail e &quot;+1-111-111-1111&quot; per il numero di telefono.
* **Valori di identità errati o errati**: i valori di identità errati o non validi si riferiscono a valori di identità non univoci che potrebbero unire gli ID del sistema di gestione delle relazioni con i clienti. Ad esempio, mentre gli identificatori IDFA devono avere 36 caratteri (32 caratteri alfanumerici e quattro trattini), ci sono scenari in cui un identificatore IDFA con valore di identità &quot;user_null&quot; può essere acquisito. Allo stesso modo, i numeri di telefono supportano solo caratteri numerici, ma è possibile che venga acquisito uno spazio dei nomi telefonico con un valore di identità &quot;non specificato&quot;.

Per ulteriori informazioni sugli scenari di utilizzo per le regole di collegamento del grafico delle identità, consulta il documento su [scenari di esempio](./example-scenarios.md).

## Obiettivi delle regole di collegamento del grafico delle identità

Con le regole di collegamento del grafico delle identità puoi:

* Crea un singolo grafo di identità/profilo unito per ogni utente configurando spazi dei nomi univoci (limiti), che impediranno a due identificatori di persona diversi di unirsi in un unico grafo di identità.
* Associa eventi online autenticati alla persona configurando le priorità

### Limiti

Uno spazio dei nomi univoco è un identificatore che rappresenta un individuo, ad esempio l’ID del sistema di gestione delle relazioni con i clienti, l’ID di accesso e l’e-mail con hash. Se uno spazio dei nomi è designato come univoco, un grafico può avere una sola identità con quello spazio dei nomi (`limit=1`). In questo modo si evita l’unione di due identificatori di persona diversi all’interno dello stesso grafico.

* Se non è configurato un limite, potrebbero verificarsi unioni di grafici indesiderate, ad esempio due identità con un ID del sistema di gestione delle relazioni con i clienti nello spazio dei nomi di un grafico.
* Se non è configurato un limite, il grafico può aggiungere tutti gli spazi dei nomi necessari, purché il grafico sia all’interno dei guardrail (50 identità/grafico).
* Se è configurato un limite, l’algoritmo di ottimizzazione identità farà in modo che il limite venga applicato.

### Algoritmo di ottimizzazione identità

L’algoritmo di ottimizzazione delle identità è una regola che assicura che i limiti vengano applicati. L’algoritmo rispetta i collegamenti più recenti e rimuove i collegamenti più vecchi per garantire che un dato grafico rimanga entro i limiti definiti.

Di seguito è riportato un elenco delle implicazioni dell’algoritmo sull’associazione di eventi anonimi a identificatori noti:

* L’ECID verrà associato all’ultimo utente autenticato se sono soddisfatte le seguenti condizioni:
   * Se gli ID del sistema di gestione delle relazioni con i clienti vengono uniti da ECID (dispositivo condiviso).
   * Se i limiti sono configurati per un solo ID CRM.

Per ulteriori informazioni, leggere il documento [algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md).

### Priorità

>[!IMPORTANT]
>
>Le priorità dello spazio dei nomi non sono attualmente disponibili per Alfa.

È possibile utilizzare la priorità dello spazio dei nomi per definire quali spazi dei nomi sono più importanti degli altri. La priorità impostata per gli spazi dei nomi viene quindi utilizzata per definire le identità primarie, ovvero l’identità che memorizza i frammenti di profilo (dati di attributi ed eventi) in Real-Time Customer Profile. Se sono configurate le impostazioni di priorità, l’impostazione di identità primaria su Web SDK non verrà più utilizzata per determinare quali frammenti di profilo sono memorizzati.

* I limiti e la priorità sono configurazioni indipendenti e **non** influenzarsi a vicenda:
   * Limiti è una configurazione del grafico delle identità in Identity Service.
   * Priorità è una configurazione di frammento di profilo in Real-Time Customer Profile.
   * Priorità **non** influenza i guardrail di sistema del grafo delle identità.
* **La priorità dello spazio dei nomi è un valore numerico** assegnato a uno spazio dei nomi che ne indica l’importanza relativa. Si tratta di una proprietà di uno spazio dei nomi.
* **L’identità primaria è l’identità in cui è memorizzato un frammento di profilo in base a**. Un frammento di profilo è un record di dati che memorizza informazioni su un determinato utente: attributi (di solito acquisiti tramite record di gestione delle relazioni con i clienti) o eventi (di solito acquisiti da eventi di esperienza o dati online).
* La priorità dello spazio dei nomi determina l’identità primaria degli eventi esperienza.
   * Per i record di profilo, puoi utilizzare l’area di lavoro schemi nell’interfaccia utente di Experienci Platform per definire i campi di identità, inclusa l’identità primaria. Leggi la guida su [definizione dei campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md) per ulteriori informazioni.

>[!BEGINSHADEBOX]

**Esempio di priorità dello spazio dei nomi**

Supponiamo di aver configurato la seguente priorità per i namespace:

1. ID CRM: rappresenta un utente.
2. IDFA: rappresenta un dispositivo hardware Apple, ad esempio iPhone e iPad.
3. GAID: rappresenta un dispositivo hardware Google, ad esempio Google Pixel.
4. ECID: rappresenta un browser web, come Firefox, Safari e Chrome.
5. AAID: rappresenta un browser web.
Se ECID e AAID vengono inviati contemporaneamente, entrambe le identità rappresentano lo stesso browser web (duplicato).

Se in Experienci Platform vengono acquisiti i seguenti eventi di esperienza, i frammenti di profilo vengono memorizzati in base allo spazio dei nomi con priorità maggiore.

**Eventi autenticati:**

* Se la mappa di identità contiene un ECID, un GAID e un ID del sistema di gestione delle relazioni con i clienti, le informazioni sull’evento verranno memorizzate in base all’ID del sistema di gestione delle relazioni con i clienti (identità primaria).
   * GAID rappresenta un dispositivo hardware Google (ad esempio, Google Pixel), ECID rappresenta un browser web (ad esempio, Google Chrome) e l’ID del sistema di gestione delle relazioni con i clienti rappresenta un utente autenticato.
   * Se la mappa delle identità contiene un ID del sistema di gestione delle relazioni con i clienti, un ECID e un AAID, le informazioni sull’evento verranno memorizzate in base all’ID del sistema di gestione delle relazioni con i clienti (identità primaria).

**Eventi non autenticati:**

* Se la mappa delle identità contiene un ECID, IDFA e AAID, le informazioni sull’evento verranno memorizzate in base all’IDFA (identità primaria).
   * IDFA rappresenta un dispositivo hardware Apple (ad esempio iPhone), ECID e AAID rappresentano entrambi un browser web (Safari).

>[!ENDSHADEBOX]

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Scenari di esempio per la configurazione delle regole di collegamento del grafico delle identità](./example-scenarios.md)
