---
title: Algoritmo di ottimizzazione delle identità
description: Scopri sull'algoritmo di ottimizzazione delle identità nel servizio Identity.
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: 7174c2c0d8c4ada8d5bba334492bad396c1cfb34
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 4%

---

# Algoritmo di ottimizzazione delle identità {#identity-optimization-algorithm}

>[!CONTEXTUALHELP]
>id="platform_identities_uniquenamespace"
>title="Spazio dei nomi univoco"
>abstract="Un grafico non può avere due identità con uno spazio dei nomi univoco. Se un grafico tenta di superare questo limite, vengono mantenuti i collegamenti più recenti e rimossi quelli più vecchi."

>[!AVAILABILITY]
>
>Le regole di collegamento del grafico delle identità sono attualmente in disponibilità limitata. Contatta il tuo team di account Adobe Systems per informazioni su come accesso la funzionalità nelle sandbox di sviluppo.

L&#39;algoritmo di ottimizzazione delle identità è un algoritmo grafico del servizio Identity che consente di garantire che un grafico di identità sia rappresentativo di una singola persona e, pertanto, impedisce l&#39;unione indesiderata di identità nel profilo cliente in tempo reale.

## Parametri di input {#input-parameters}

Leggi questa sezione per informazioni sui namespace univoci e sulla priorità degli spazi dei nomi. Questi due concetti fungono da parametri di input richiesti dall&#39;algoritmo di ottimizzazione delle identità.

### Spazio dei nomi univoco {#unique-namespace}

Un namespace univoco determina i collegamenti che vengono rimossi se si verifica il collasso del grafico.

Un singolo profilo unito e il relativo grafico di identità dovrebbero rappresentare un singolo individuo (entità personale). Un singolo individuo è solitamente rappresentato da CRMID e/o ID di accesso. L&#39;aspettativa è che non ci siano due individui (CRMID) uniti in un unico profilo o grafico.

È necessario specificare quali spazi dei nomi rappresentano un’entità persona in Identity Service utilizzando l’algoritmo di ottimizzazione delle identità. Ad esempio, se un database di gestione delle relazioni con i clienti definisce un account utente da associare a un singolo identificatore CRMID e a un singolo indirizzo e-mail, le impostazioni di identità per questa sandbox saranno simili alle seguenti:

* Spazio dei nomi CRMID = univoco
* Namespace e-mail = univoco

Uno spazio dei nomi dichiarato univoco verrà automaticamente configurato per avere un limite massimo di uno all&#39;interno di un determinato grafico di identità. Ad esempio, se dichiari uno spazio dei nomi CRMID come univoco, un grafico di identità può avere solo un&#39;identità che contiene uno spazio dei nomi CRMID. Se non dichiari che uno spazio dei nomi è univoco, il grafico può contenere più di un&#39;identità con tale spazio dei nomi.

>[!NOTE]
>
>* Al momento la rappresentazione delle entità domestiche (&quot;grafici delle famiglie&quot;) non è supportata.
>
>* Tutti gli spazi dei nomi che sono identificatori di persona e che vengono utilizzati nella sandbox per generare grafici di identità devono essere contrassegnati come spazi dei nomi univoci. In caso contrario, potrebbero verificarsi risultati di collegamento indesiderati.

### Priorità dello spazio dei nomi {#namespace-priority}

La priorità dello spazio dei nomi determina il modo in cui l’algoritmo di ottimizzazione delle identità rimuove i collegamenti.

Gli spazi dei nomi in Identity Service hanno un ordine relativo implicito di importanza. Si consideri un grafico strutturato like una piramide. C&#39;è un nodo sul livello superiore, due nodi sul livello intermedio e quattro nodi sul livello inferiore. La priorità dello spazio dei nomi deve riflettere questo ordine relativo per garantire che un&#39;entità personale sia rappresentata accuratamente.

Per informazioni approfondite sulla priorità dello spazio dei nomi e sulle relative funzionalità e utilizzi completi, leggere la [guida sulla priorità dello spazio dei nomi](./namespace-priority.md).

![livelli del grafico e priorità dello spazio dei nomi](../images/namespace-priority/graph-layers.png)

## Processo {#process}

Al momento dell’acquisizione di nuove identità, Identity Service controlla se le nuove identità e i corrispondenti spazi dei nomi aderiscono a configurazioni univoche dello spazio dei nomi. Se si seguono le configurazioni, l’acquisizione procede e le nuove identità sono collegate al grafico. Tuttavia, se non si seguono le configurazioni, l’algoritmo di ottimizzazione delle identità:

* Assimilare l&#39;evento più recente, mantenendo la priorità dello spazio dei nomi in account.
* Rimuovi il collegare che unirebbe due entità persona dal livello grafico appropriato.

## Dettagli dell&#39;algoritmo di ottimizzazione dell&#39;identità

Quando viene violato il vincolo univoco dello spazio dei nomi, l&#39;algoritmo di ottimizzazione delle identità &quot;riprodurrà&quot; i collegamenti e ricostruirà il grafico da zero.

* I collegamenti sono ordinati in base al seguente ordine:
   * Ultimo evento.
   * Marca temporale basata sulla somma della priorità dello spazio dei nomi (somma inferiore = ordine superiore).
* Il grafico verrebbe ristabilito in base all&#39;ordine di cui sopra. Se l&#39;aggiunta del collegare viola il vincolo limite (ad esempio, il grafico contiene due o più identità con un namespace univoco), i collegamenti vengono rimossi.
* Il grafico risultante sarà quindi conforme al vincolo univoco dello spazio dei nomi configurato.

![Diagramma che visualizza l&#39;algoritmo di ottimizzazione delle identità.](../images/ido_algorithm.png)

## Scenari di esempio per l&#39;algoritmo di ottimizzazione delle identità

Nella sezione seguente viene illustrato il comportamento dell&#39;algoritmo di ottimizzazione delle identità, in scenari quali dispositivo condivisi o inserimento di dati con lo stesso timestamp.

### Dispositivo condiviso

Per dispositivo condivisa si intende un dispositivo utilizzato da più individui. Ad esempio, un dispositivo condiviso può essere un laptop o un tablet condiviso con un partner o un familiare, un computer libreria o un chiosco multimediale pubblico.

>[!BEGINTABS]

>[!TAB Esempio uno]

| Namespace | Spazio dei nomi univoco |
| --- | --- |
| CRMID | Sì |
| E-mail | Sì |
| ECID | No |

In questo esempio, sia CRMID che Email sono designati come spazi dei nomi univoci. In `timestamp=0`, un set di dati di record CRM viene inserito e crea due grafici diversi a causa della configurazione univoca dello spazio dei nomi. Ogni grafico contiene uno spazio dei nomi CRMID e uno Email.

* `timestamp=1`: Jane accede al tuo sito Web e-commerce utilizzando un laptop. Jane è rappresentata dal suo CRMID e Email, mentre il browser web sul suo laptop che usa è rappresentato da un ECID.
* `timestamp=2`: John accede al tuo sito Web e-commerce utilizzando lo stesso laptop. John è rappresentato dal suo CRMID e Email, mentre il browser web che ha usato è già rappresentato da un ECID. Poiché lo stesso ECID è collegato a due grafici diversi, Identity Service è in grado di sapere che questo dispositivo (laptop) è un dispositivo condiviso.
* Tuttavia, a causa della configurazione univoca dello spazio dei nomi che imposta un massimo di uno spazio dei nomi CRMID e uno spazio dei nomi Email per grafico, l&#39;algoritmo di ottimizzazione dell&#39;identità divide il grafico in due.
   * Infine, poiché John è l&#39;ultimo utente autenticato, l&#39;ECID che rappresenta il laptop, rimane collegato al suo grafico anziché a quello di Jane.

![condiviso dispositivo caso uno](../images/identity-settings/shared-device-case-one.png)

>[!TAB Esempio due]

| Namespace | Spazio dei nomi univoco |
| --- | --- |
| CRMID | Sì |
| ECID | No |

In questo esempio, lo spazio dei nomi CRMID è designato come spazio dei nomi univoco.

* `timestamp=1`: Jane accede al tuo sito Web e-commerce utilizzando un laptop. È rappresentata dal suo CRMID e il browser web sul laptop è rappresentato dall&#39;ECID.
* `timestamp=2`: John accede al tuo sito Web di e-commerce utilizzando lo stesso laptop. È rappresentato dal suo CRMID e il browser web che utilizza è rappresentato dallo stesso ECID.
   * Questo evento collega due CRMID indipendenti allo stesso ECID, superando il limite configurato di un CRMID.
   * Di conseguenza, l&#39;algoritmo di ottimizzazione dell&#39;identità rimuove il collegare precedente, che in questo caso è il CRMID di Jane collegato a `timestamp=1`.
   * Tuttavia, sebbene Jane&#39;s CRMID non esista più come grafico su Identity Service, continuerà a persistere come profilo in Real-Time Customer Profile. Questo perché un grafico delle identità deve contenere almeno due identità collegate e, a seguito della rimozione dei collegamenti, il CRMID di Jane non ha più un&#39;altra identità a cui collegare.

![dispositivo condivisa caso due](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### E-mail errata

Ci sono casi in cui un utente può inserire valori errati per la propria e-mail e / o numeri di telefono.

| Namespace | Spazio dei nomi univoco |
| --- | --- |
| CRMID | Sì |
| E-mail | Sì |
| ECID | No |

In questo esempio, gli spazi dei nomi CRMID e E-mail sono designati come univoci. Considera lo scenario in cui Jane e John si sono iscritti al tuo sito Web di e-commerce utilizzando un valore di e-mail non valido (ad esempio, test<span>@test.com).

* `timestamp=1`: Jane accede al tuo sito Web di e-commerce utilizzando Safari sul suo iPhone, stabilendo il suo CRMID (informazioni di accesso) e il suo ECID (browser).
* `timestamp=2`: John accede al tuo sito web e-commerce utilizzando Google Effetto cromatura sul suo iPhone, stabilendo le sue informazioni CRMID (login) ed ECID (browser).
* `timestamp=3`: il tuo ingegnere dei dati ingerisce il record CRM di Jane, il che fa sì che il suo CRMID venga collegato all&#39;e-mail errata.
* `timestamp=4`: il tuo ingegnere dei dati acquisisce il record CRM di John, il che fa sì che il suo CRMID venga collegato all&#39;e-mail errata.
   * Questo diventa quindi una violazione della configurazione dello spazio dei nomi univoco, in quanto crea un singolo grafico con due spazi dei nomi CRMID.
   * Di conseguenza, l&#39;algoritmo di ottimizzazione delle identità elimina il collegamento precedente, che in questo caso è il collegamento tra l&#39;identità di Jane con lo spazio dei nomi CRMID e l&#39;identità con il test<span>@test.

Con l’algoritmo di ottimizzazione dell’identità, i valori di identità errati, come e-mail o numeri di telefono falsi, non vengono propagati attraverso diversi grafici di identità.

![e-mail errata](../images/identity-settings/bad-email.png)

### Associazione evento anonimo

Gli ECID memorizzano gli eventi non autenticati (anonimi), mentre CRMID archivia gli eventi autenticati. Nel caso di dispositivi condivisi, l&#39;ECID (portatore di eventi non autenticati) viene associato all&#39;**ultimo utente autenticato**.

Per comprendere meglio il funzionamento dell’associazione anonima degli eventi, consulta il diagramma seguente:

* Kevin e Nora condividono un tablet.
   * `timestamp=1`: Kevin accede a un sito Web di e-commerce utilizzando il suo account, stabilendo in tal modo il suo CRMID (informazioni di accesso) e un ECID (browser). Al momento dell&#39;accesso, Kevin è ora considerato l&#39;ultimo utente autenticato.
   * `timestamp=2`: Nora accede a un sito Web di e-commerce utilizzando il suo account, stabilendo in tal modo il suo CRMID (informazioni di accesso) e lo stesso ECID. Al momento dell’accesso, Nora è considerato l’ultimo utente autenticato.
   * `timestamp=3`: Kevin utilizza il tablet per sfogliare il sito Web di e-commerce, ma non accede con il proprio account. L&#39;attività di navigazione di Kevin viene quindi memorizzata nell&#39;ECID, che a sua volta è associata a Nora perché è l&#39;ultimo utente autenticato. A questo punto, Nora è la proprietaria degli eventi anonimi.
      * Fino a quando Kevin non accede di nuovo, il profilo unito di Nora verrà associato a tutti gli eventi non autenticati archiviati nell&#39;ECID (con gli eventi in cui ECID è l&#39;identità primaria).
   * `timestamp=4`: Kevin accede per la seconda volta. A questo punto, diventa di nuovo l&#39;ultimo utente autenticato e ora possiede anche gli eventi non autenticati:
      * Prima della sua login iniziale prima di `timestamp=1`; e
      * Qualsiasi attività che lui o Nora hanno fatto durante la navigazione anonima tra il primo e il secondo accesso di Kevin.

![anon-evento-associazione](../images/identity-settings/anon-event-association.png)


## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento dei grafici di identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico di identità](./overview.md)
* [Guida all&#39;implementazione](./implementation-guide.md)
* [Esempi di configurazioni del grafico](./example-configurations.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Simulazione grafica interfaccia](./graph-simulation.md)
* [Impostazioni di identità interfaccia](./identity-settings-ui.md)