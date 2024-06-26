---
title: Algoritmo di ottimizzazione identità
description: Scopri l’algoritmo di ottimizzazione delle identità in Identity Service.
badge: Beta
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: f1779ee75c877649a69f9fa99f3872aea861beca
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 1%

---

# Algoritmo di ottimizzazione identità

>[!AVAILABILITY]
>
>Questa funzione non è ancora disponibile; il programma beta per le regole di collegamento del grafo delle identità dovrebbe iniziare a luglio per le sandbox di sviluppo. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione.

L’algoritmo di ottimizzazione delle identità è un algoritmo grafico sul servizio Identity che garantisce che un grafico delle identità sia rappresentativo di una singola persona e, pertanto, impedisce l’unione indesiderata di identità sul profilo cliente in tempo reale.

## Parametri di input {#input-parameters}

Leggi questa sezione per informazioni sugli spazi dei nomi univoci e sulla priorità dello spazio dei nomi. Questi due concetti fungono da parametri di input richiesti dall’algoritmo di ottimizzazione delle identità.

### Spazio dei nomi univoco {#unique-namespace}

Uno spazio dei nomi univoco determina i collegamenti che vengono rimossi in caso di compressione del grafico.

Un singolo profilo unito e il grafico delle identità corrispondente devono rappresentare un singolo individuo (entità persona). Un singolo individuo è solitamente rappresentato dagli ID CRM e/o dagli ID di accesso. L’aspettativa è che non ci siano due individui (ID del sistema di gestione delle relazioni con i clienti) uniti in un singolo profilo o grafico.

È necessario specificare quali spazi dei nomi rappresentano un’entità persona in Identity Service utilizzando l’algoritmo di ottimizzazione delle identità. Ad esempio, se un database di gestione delle relazioni con i clienti definisce un account utente da associare a un singolo ID di gestione delle relazioni con i clienti e a un singolo indirizzo e-mail, le impostazioni di identità per questa sandbox saranno simili alle seguenti:

* ID CRM spazio dei nomi = univoco
* Spazio dei nomi e-mail = univoco

Uno spazio dei nomi che dichiari univoco verrà configurato automaticamente in modo da avere un limite massimo di uno all’interno di un dato grafico delle identità. Ad esempio, se dichiari univoco uno spazio dei nomi ID del sistema di gestione delle relazioni con i clienti, un grafo delle identità può avere una sola identità contenente uno spazio dei nomi ID del sistema di gestione delle relazioni con i clienti. Se non dichiari uno spazio dei nomi univoco, il grafico può contenere più di un’identità con tale spazio dei nomi.

>[!NOTE]
>
>* Al momento non è supportata la rappresentazione di entità familiari (&quot;grafici delle famiglie&quot;).
>
>* Tutti gli spazi dei nomi che sono identificatori di persona e che vengono utilizzati nella sandbox per generare grafici di identità devono essere contrassegnati come spazi dei nomi univoci. In caso contrario, potrebbero verificarsi risultati di collegamento indesiderati.

### Priorità dello spazio dei nomi {#namespace-priority}

La priorità dello spazio dei nomi determina il modo in cui l’algoritmo di ottimizzazione delle identità rimuove i collegamenti.

Gli spazi dei nomi in Identity Service hanno un ordine di importanza relativo implicito. Consideriamo un grafico strutturato come una piramide. Vi sono un nodo sul livello superiore, due nodi sul livello intermedio e quattro nodi sul livello inferiore. La priorità dello spazio dei nomi deve riflettere questo ordine relativo per garantire che un’entità persona sia rappresentata correttamente.

Per informazioni approfondite sulla priorità dello spazio dei nomi e sulle sue funzionalità e utilizzi completi, leggi [guida alla priorità namespace](./namespace-priority.md).

![livelli di grafico e priorità dello spazio dei nomi](../images/namespace-priority/graph-layers.png)

## Processo {#process}


Al momento dell’acquisizione di nuove identità, Identity Service controlla se le nuove identità e i corrispondenti spazi dei nomi aderiscono a configurazioni univoche dello spazio dei nomi. Se si seguono le configurazioni, l’acquisizione procede e le nuove identità sono collegate al grafico. Tuttavia, se non si seguono le configurazioni, l’algoritmo di ottimizzazione delle identità:


* Acquisisci l’evento più recente tenendo conto della priorità dello spazio dei nomi.
* Rimuove il collegamento che unirebbe due entità persona dal livello grafico appropriato.

## Dettagli dell’algoritmo di ottimizzazione delle identità

Quando il vincolo dello spazio dei nomi univoco viene violato, l’algoritmo di ottimizzazione dell’identità &quot;riprodurrà&quot; i collegamenti e ricostruirà il grafico da zero.

* I collegamenti sono ordinati in base al seguente ordine:
   * Ultimo evento.
   * Marca temporale per somma della priorità dello spazio dei nomi (somma inferiore = ordine più elevato).
* Il grafico verrà ristabilito in base all’ordine indicato sopra. Se l’aggiunta del collegamento viola il vincolo del limite (ad esempio, il grafico contiene due o più identità con uno spazio dei nomi univoco), i collegamenti vengono rimossi.
* Il grafico risultante sarà quindi conforme al vincolo dello spazio dei nomi univoco configurato.

![Un diagramma che visualizza l’algoritmo di ottimizzazione delle identità.](../images/ido.png)

## Scenari di esempio per l’algoritmo di ottimizzazione delle identità

La sezione seguente illustra il comportamento dell’algoritmo di ottimizzazione delle identità, in scenari come il dispositivo condiviso o l’acquisizione di dati con la stessa marca temporale.

### Dispositivo condiviso

Per dispositivo condiviso si intende un dispositivo utilizzato da più utenti. Ad esempio, un dispositivo condiviso può essere un laptop o un tablet condiviso con un partner o un membro della famiglia, un computer di libreria o un chiosco pubblico.

>[!BEGINTABS]

>[!TAB Esempio uno]

| Namespace | Spazio dei nomi univoco |
| --- | --- |
| ID CRM | Sì |
| E-mail | Sì |
| ECID | No |

In questo esempio, sia l’ID CRM che l’E-mail sono designati come spazi dei nomi univoci. A `timestamp=0`, viene acquisito un set di dati del record CRM e crea due grafici diversi a causa della configurazione univoca dello spazio dei nomi. Ogni grafico contiene un ID CRM e uno spazio dei nomi e-mail.

* `timestamp=1`: Jane accede al tuo sito web di e-commerce utilizzando un laptop. Jane è rappresentata dal suo ID CRM e dal suo indirizzo e-mail, mentre il browser web sul suo laptop che utilizza è rappresentato da un ECID.
* `timestamp=2`: John accede al tuo sito web di e-commerce utilizzando lo stesso laptop. John è rappresentato dal suo ID CRM e dal suo indirizzo e-mail, mentre il browser web che ha usato è già rappresentato da un ECID. Poiché lo stesso ECID è collegato a due grafici diversi, Identity Service è in grado di sapere che questo dispositivo (laptop) è condiviso.
* Tuttavia, a causa della configurazione univoca dello spazio dei nomi che imposta un massimo di uno spazio dei nomi ID del sistema di gestione delle relazioni con i clienti e di uno spazio dei nomi e-mail per grafico, l’algoritmo di ottimizzazione dell’identità divide il grafico in due.
   * Infine, poiché John è l&#39;ultimo utente autenticato, l&#39;ECID che rappresenta il laptop, rimane collegato al suo grafo invece di quello di Jane.

![caso dispositivo condiviso 1](../images/identity-settings/shared-device-case-one.png)

>[!TAB Esempio due]

| Namespace | Spazio dei nomi univoco |
| --- | --- |
| ID CRM | Sì |
| ECID | No |

In questo esempio, lo spazio dei nomi dell’ID del sistema di gestione delle relazioni con i clienti è designato come spazio dei nomi univoco.

* `timestamp=1`: Jane accede al tuo sito web di e-commerce utilizzando un laptop. È rappresentata dal suo ID CRM, e il browser web sul laptop è rappresentato dall’ECID.
* `timestamp=2`: John accede al tuo sito web di e-commerce utilizzando lo stesso laptop. È rappresentato dal suo ID CRM e il browser web che utilizza è rappresentato dallo stesso ECID.
   * Questo evento collega due ID CRM indipendenti allo stesso ECID, che supera il limite configurato di un ID CRM.
   * Di conseguenza, l’algoritmo di ottimizzazione dell’identità rimuove il collegamento precedente, che in questo caso è l’ID CRM di Jane che era collegato in `timestamp=1`.
   * Tuttavia, anche se l’ID CRM di Jane non esisterà più come grafico sul servizio Identity, persisterà ancora come profilo sul profilo cliente in tempo reale. Questo perché un grafo di identità deve contenere almeno due identità collegate e, a seguito della rimozione dei collegamenti, l’ID del sistema di gestione delle relazioni con i clienti di Jane non ha più un’altra identità a cui collegarsi.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### E-mail non valida

In alcuni casi, un utente potrebbe immettere valori non validi per i propri numeri di telefono e/o e-mail.

| Namespace | Spazio dei nomi univoco |
| --- | --- |
| ID CRM | Sì |
| E-mail | Sì |
| ECID | No |

In questo esempio, l’ID del sistema di gestione delle relazioni con i clienti e gli spazi dei nomi e-mail sono designati come univoci. Considera lo scenario in cui Jane e John si sono iscritti al tuo sito web di e-commerce utilizzando un valore e-mail errato (ad esempio, test<span>@test.com).

* `timestamp=1`: Jane accede al tuo sito web di e-commerce utilizzando Safari sul suo iPhone, stabilendo il suo ID di gestione delle relazioni con i clienti (informazioni di accesso) e il suo ECID (browser).
* `timestamp=2`: John accede al tuo sito web di e-commerce utilizzando Google Chrome sul suo iPhone, stabilendo il suo ID CRM (informazioni di accesso) e ECID (browser).
* `timestamp=3`: l’ingegnere dati acquisisce il record CRM di Jane, il che fa sì che il suo ID CRM venga collegato all’e-mail errata.
* `timestamp=4`: il tuo ingegnere dati acquisisce il record CRM di John, il che fa sì che il suo ID CRM venga collegato all’e-mail errata.
   * Questo diventa quindi una violazione della configurazione dello spazio dei nomi univoco, in quanto crea un singolo grafico con due spazi dei nomi ID del sistema di gestione delle relazioni con i clienti.
   * Di conseguenza, l’algoritmo di ottimizzazione dell’identità elimina il collegamento precedente, che in questo caso è il collegamento tra l’identità di Jane con lo spazio dei nomi dell’ID del sistema di gestione delle relazioni con i clienti e l’identità con il test<span>@test.

Con l’algoritmo di ottimizzazione dell’identità, i valori di identità errati, come e-mail o numeri di telefono falsi, non vengono propagati attraverso diversi grafici di identità.

![bad-email](../images/identity-settings/bad-email.png)

### Associazione evento anonimo

Gli ECID memorizzano gli eventi non autenticati (anonimi), mentre l&#39;ID del sistema di gestione delle relazioni con i clienti memorizza gli eventi autenticati. Nel caso di dispositivi condivisi, l’ECID (portatore di eventi non autenticati) viene associato al **ultimo utente autenticato**.

Per comprendere meglio il funzionamento dell’associazione anonima degli eventi, consulta il diagramma seguente:

* Kevin e Nora condividono un tablet.
   * `timestamp=1`: Kevin accede a un sito web di e-commerce utilizzando il suo account, stabilendo in tal modo il suo ID CRM (informazioni di accesso) e un ECID (browser). Al momento dell&#39;accesso, Kevin è ora considerato l&#39;ultimo utente autenticato.
   * `timestamp=2`: Nora accede a un sito web di e-commerce utilizzando il suo account, stabilendo in tal modo il suo ID di gestione delle relazioni con i clienti (informazioni di accesso) e lo stesso ECID. Al momento dell’accesso, Nora è considerato l’ultimo utente autenticato.
   * `timestamp=3`: Kevin utilizza il tablet per navigare nel sito web di e-commerce, ma non accede con il suo account. L&#39;attività di navigazione di Kevin viene quindi memorizzata nell&#39;ECID, che a sua volta è associata a Nora perché è l&#39;ultimo utente autenticato. A questo punto, Nora è la proprietaria degli eventi anonimi.
      * Fino a quando Kevin non effettua di nuovo l’accesso, il profilo unito di Nora verrà associato a tutti gli eventi non autenticati memorizzati nell’ECID (dove gli eventi sono dove ECID è l’identità primaria).
   * `timestamp=4`: Kevin accede per la seconda volta. A questo punto, diventa di nuovo l’ultimo utente autenticato e ora è anche il proprietario degli eventi non autenticati:
      * Prima del primo accesso prima di `timestamp=1`; e
      * Tutte le attività che lui o Nora hanno svolto durante la navigazione anonima tra il primo e il secondo accesso di Kevin.

![anon-event-association](../images/identity-settings/anon-event-association.png)


## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico delle identità](./overview.md)
* [Scenari di esempio per la configurazione delle regole di collegamento del grafico delle identità](./example-scenarios.md)
* [Logica di collegamento dell’identità](../features/identity-linking-logic.md)
* [Servizio Identity e Real-Time Customer Profile](../identity-and-profile.md)
