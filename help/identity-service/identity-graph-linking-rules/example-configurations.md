---
title: Esempi di configurazioni dei grafici
description: Scopri gli scenari di grafico comuni che potresti incontrare quando utilizzi le regole di collegamento del grafico delle identità e i dati di identità.
badge: Beta
exl-id: fd0afb0b-a368-45b9-bcdc-f2f3b7508cee
source-git-commit: 1ea840e2c6c44d5d5080e0a034fcdab4cbdc87f1
workflow-type: tm+mt
source-wordcount: '2786'
ht-degree: 6%

---

# Esempi di configurazioni del grafico

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo delle identità sono attualmente in versione beta. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione. La funzione e la documentazione sono soggette a modifiche.

>[!NOTE]
>
>* &quot;CRMID&quot; e &quot;loginID&quot; sono spazi dei nomi personalizzati. In questo documento, &quot;CRMID&quot; è un identificatore di persona e &quot;loginID&quot; è un identificatore di accesso associato a una determinata persona.
>* Per simulare gli scenari del grafico di esempio descritti in questo documento, devi innanzitutto creare due spazi dei nomi personalizzati, uno con il simbolo di identità &quot;CRMID&quot; e un altro con il simbolo di identità &quot;loginID&quot;. I simboli di identità fanno distinzione tra maiuscole e minuscole.


Questo documento illustra alcuni esempi di configurazione del grafico di scenari comuni che potresti incontrare quando lavori con regole di collegamento del grafico delle identità e dati di identità.

## Solo CRMID

Questo è un esempio di un semplice scenario di implementazione in cui gli eventi online (CRMID ed ECID) vengono acquisiti e gli eventi offline (record di profilo) vengono memorizzati solo in base al CRMID.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

```shell
CRMID: Tom, ECID: 111
```

**Configurazione algoritmo:**

Puoi creare questo scenario nella simulazione del grafico configurando la seguente configurazione per la configurazione dell’algoritmo:

| Priorità | Nome visualizzato | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sì |
| 2 | ECID | COOKIE | No |

**Selezione identità primaria per Real-Time Customer Profile:**

Nel contesto di questa configurazione, l’identità primaria sarà definita come segue:

| Stato di autenticazione | Spazio dei nomi negli eventi | Identità primaria |
| --- | --- | --- |
| autenticato | CRMID, ECID | CRMID |
| Non autenticato | ECID | ECID |

**Esempi di grafici**

>[!BEGINTABS]

>[!TAB Grafico a persona singola ideale]

Di seguito è riportato un esempio di grafico ideale a persona singola, in cui il CRMID è univoco e riceve la priorità più elevata.

![Esempio simulato di un grafico a persona singola ideale, in cui il CRMID è univoco e a cui viene assegnata la priorità più elevata.](../images/graph-examples/crmid_only_single.png)

>[!TAB Grafico a più persone]

Di seguito è riportato un esempio di grafico a più persone. In questo esempio viene visualizzato lo scenario &quot;dispositivo condiviso&quot;, in cui sono presenti due CRMID e viene rimosso quello con il collegamento stabilito precedente.

![Esempio simulato di un grafico a più persone. In questo esempio viene visualizzato uno scenario di dispositivo condiviso, in cui sono presenti due CRMID e il collegamento stabilito precedente viene rimosso.](../images/graph-examples/crmid_only_multi.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, ECID: 111
CRMID: Summer, ECID: 111
```

>[!ENDTABS]

## CRMID con e-mail con hash

In questo scenario, viene acquisito un CRMID che rappresenta sia dati online (evento esperienza) che offline (record profilo). Questo scenario comporta anche l’acquisizione di un’e-mail con hash, che rappresenta un altro spazio dei nomi inviato nel set di dati del record di gestione delle relazioni con i clienti insieme al CRMID.

>[!IMPORTANT]
>
>**È fondamentale che il CRMID venga sempre inviato per ogni utente**. In caso contrario, potrebbe verificarsi uno scenario con ID di accesso &quot;tralasciato&quot;, in cui si presume che una singola persona condivida un dispositivo con un’altra persona.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, E-mail_LC_SHA256, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

```shell
CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
CRMID: Tom, ECID: 111
CRMID: Summer, Email_LC_SHA256: summer<span>@acme.com
CRMID: Summer, ECID: 222
```

**Configurazione algoritmo:**

Puoi creare questo scenario nella simulazione del grafico configurando la seguente configurazione per la configurazione dell’algoritmo:

| Priorità | Nome visualizzato | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sì |
| 2 | E-mail (SHA256, in minuscolo) | E-mail | No |
| 3 | ECID | COOKIE | No |

**Selezione identità primaria per il profilo:**

Nel contesto di questa configurazione, l’identità primaria sarà definita come segue:

| Stato di autenticazione | Spazio dei nomi negli eventi | Identità primaria |
| --- | --- | --- |
| autenticato | CRMID, ECID | CRMID |
| Non autenticato | ECID | ECID |

**Esempi di grafici**

>[!BEGINTABS]

>[!TAB Grafico a persona singola ideale]

Di seguito sono riportati alcuni esempi di una coppia di grafici ideali per singola persona, in cui ogni CRMID è associato al rispettivo spazio dei nomi e-mail con hash ed ECID.

![In questo esempio vengono generati due grafici distinti, ciascuno dei quali rappresenta un&#39;entità a persona singola.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB Grafico a più persone: dispositivo condiviso]

Di seguito è riportato un esempio di uno scenario con grafico a più persone in cui un dispositivo è condiviso da due persone.

![In questo esempio, il grafico simulato visualizza uno scenario di &quot;dispositivo condiviso&quot; perché sia Tom che Summer sono associati allo stesso ECID.](../images/graph-examples/crmid_hashed_shared_device.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc
CRMID: Tom, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff
CRMID: Summer, ECID: 222
CRMID: Summer, ECID: 111
```

>[!TAB Grafico a più persone: e-mail non univoca]

Di seguito è riportato un esempio di uno scenario con grafico a più persone in cui l’e-mail non è univoca e viene associata a due diversi CRMID.

![Questo scenario è simile a uno scenario &quot;dispositivo condiviso&quot;. Tuttavia, invece di avere le entità persona condivise ECID, esse vengono associate allo stesso account e-mail.](../images/graph-examples/crmid_hashed_nonunique_email.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc
CRMID: Tom, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff
CRMID: Summer, ECID: 222
CRMID: Summer, Email_LC_SHA256: aabbcc
```

>[!ENDTABS]

## CRMID con e-mail con hash, telefono con hash, GAID e IDFA

Questo scenario è simile a quello precedente. Tuttavia, in questo scenario, le e-mail e il telefono con hash vengono contrassegnati come identità da utilizzare in [[!DNL Segment Match]](../../segmentation/ui/segment-match/overview.md).

>[!IMPORTANT]
>
>**È fondamentale che il CRMID venga sempre inviato per ogni utente**. In caso contrario, potrebbe verificarsi uno scenario con ID di accesso &quot;tralasciato&quot;, in cui si presume che una singola persona condivida un dispositivo con un’altra persona.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID:B-B-B
```

**Configurazione algoritmo:**

Puoi creare questo scenario nella simulazione del grafico configurando la seguente configurazione per la configurazione dell’algoritmo:

| Priorità | Nome visualizzato | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sì |
| 2 | E-mail (SHA256, in minuscolo) | E-mail | No |
| 3 | Telefono (SHA256) | Telefono | No |
| 4 | Google Ad ID (GAID) | DISPOSITIVO | No |
| 5 | Apple IDFA (ID per Apple) | DISPOSITIVO | No |
| 6 | ECID | COOKIE | No |

**Selezione identità primaria per il profilo:**

Nel contesto di questa configurazione, l’identità primaria sarà definita come segue:

| Stato di autenticazione | Spazio dei nomi negli eventi | Identità primaria |
| --- | --- | --- |
| autenticato | CRMID, IDFA, ECID | CRMID |
| autenticato | CRMID, GAID, ECID | CRMID |
| autenticato | CRMID, ECID | CRMID |
| Non autenticato | GAID, ECID | GAID |
| Non autenticato | IDFA, ECID | IDFA |
| Non autenticato | ECID | ECID |

**Esempi di grafici**

>[!BEGINTABS]

>[!TAB Grafico a persona singola ideale]

Di seguito è riportato uno scenario di grafico a persona singola ideale in cui e-mail con hash e telefono con hash sono contrassegnati come identità da utilizzare in [!DNL Segment Match]. In questo scenario, i grafici sono suddivisi in due, per rappresentare entità persona diverse.

![Scenario di grafico a persona singola ideale.](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!TAB Grafico a più persone: dispositivo condiviso, computer condiviso]

Di seguito è riportato uno scenario di grafico a più persone in cui un dispositivo (computer) è condiviso da due persone. In questo scenario, il computer condiviso è rappresentato da `{ECID: 111}` ed è collegato a `{CRMID: Summer}` perché il collegamento è quello stabilito più di recente. `{CRMID: Tom}` è stato rimosso perché il collegamento tra `{CRMID: Tom}` e `{ECID: 111}` è meno recente e perché CRMID è lo spazio dei nomi univoco designato in questa configurazione.

![Scenario di grafico a più persone in cui due utenti condividono un computer.](../images/graph-examples/shared_device_shared_computer.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID:B-B-B
CRMID: Summer, ECID: 111
```

>[!TAB Grafico a più persone: dispositivo condiviso, dispositivo mobile Android]

Di seguito è riportato uno scenario con un grafico a più persone in cui un dispositivo android è condiviso da due persone. In questo scenario, CRMID è configurato come spazio dei nomi univoco e pertanto il collegamento più recente di `{CRMID: Tom, GAID: B-B-B, ECID:444}` sostituisce il precedente `{CRMID: Summer, GAID: B-B-B, ECID:444}`.

![Scenario di grafico a più persone in cui due utenti condividono un dispositivo mobile android.](../images/graph-examples/shared_device_android.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID: B-B-B
CRMID: Tom, ECID: 444, GAID: B-B-B
```

>[!TAB Grafico multi-persona: dispositivo condiviso, dispositivo mobile apple, nessun ECID reimpostato]

Di seguito è riportato uno scenario di grafico a più persone in cui un dispositivo Apple è condiviso da due persone. In questo scenario l’identificatore IDFA è condiviso, ma l’identificatore ECID non viene reimpostato.

![Scenario di grafico a più persone in cui due utenti condividono un dispositivo mobile Apple.](../images/graph-examples/shared_device_apple_no_reset.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID: B-B-B
CRMID: Summer, ECID: 222, IDFA: A-A-A
```

>[!TAB Grafico a più persone: dispositivo condiviso, apple, ripristini ECID]

Di seguito è riportato uno scenario di grafico a più persone in cui un dispositivo Apple è condiviso da due persone. In questo scenario, l’ECID viene ripristinato, ma l’IDFA rimane lo stesso.

![Scenario di grafico a più persone in cui due utenti condividono un dispositivo mobile Apple, ma l&#39;ECID è reimpostato.](../images/graph-examples/shared_device_apple_with_reset.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID: B-B-B
CRMID: Summer, ECID: 555, IDFA: A-A-A
```

>[!TAB Grafico a più persone: telefono non univoco]

Di seguito è riportato uno scenario con grafico a più persone in cui lo stesso numero di telefono viene condiviso da due persone.

![Scenario di grafico a più persone in cui lo spazio dei nomi del telefono non è univoco.](../images/graph-examples/non_unique_phone.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID: B-B-B
CRMID: Summer, Phone_SHA256: 123-4567
```

In questo esempio, anche `{Phone_SHA256}` è contrassegnato come spazio dei nomi univoco. Pertanto, un grafico non può avere più di un&#39;identità con lo spazio dei nomi `{Phone_SHA256}`. In questo scenario, `{Phone_SHA256: 765-4321}` è scollegato da `{CRMID: Summer}` e `{Email_LC_SHA256: ddeeff}` perché è il collegamento precedente,

![Scenario di grafico a più persone in cui Phone_SHA256 è univoco.](../images/graph-examples/unique_phone.png)

>[!TAB Grafico a più persone: e-mail non univoca]

Di seguito è riportato uno scenario di grafico a più persone in cui l’e-mail è condivisa da due persone.

![Uno scenario con un grafico a più persone in cui l&#39;e-mail non è univoca](../images/graph-examples/non_unique_email.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, ECID: 111
CRMID: Tom, ECID: 222, IDFA: A-A-A
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, ECID: 333
CRMID: Summer, ECID: 444, GAID: B-B-B
CRMID: Summer, Email_LC_SHA256: aabbcc
```

>[!ENDTABS]

## CRMID singolo con più ID di accesso (versione semplice)

In questo scenario, esiste un singolo CRMID che rappresenta un’entità persona. Tuttavia, un’entità persona può avere più identificatori di accesso:

* Una determinata entità persona può avere diversi tipi di conto (personale o aziendale, conto per stato, conto per marchio, ecc.)
* Una determinata entità persona può utilizzare indirizzi e-mail diversi per qualsiasi numero di account.

>[!IMPORTANT]
>
>**È fondamentale che il CRMID venga sempre inviato per ogni utente**. In caso contrario, potrebbe verificarsi uno scenario con ID di accesso &quot;tralasciato&quot;, in cui si presume che una singola persona condivida un dispositivo con un’altra persona.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, loginID, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

```shell
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
```

**Configurazione algoritmo:**

Puoi creare questo scenario nella simulazione del grafico configurando la seguente configurazione per la configurazione dell’algoritmo:

| Priorità | Nome visualizzato | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sì |
| 2 | loginID | CROSS_DEVICE | No |
| 3 | ECID | COOKIE | No |

**Selezione identità primaria per il profilo:**

Nel contesto di questa configurazione, l’identità primaria sarà definita come segue:

| Stato di autenticazione | Spazio dei nomi negli eventi | Identità primaria |
| --- | --- | --- |
| autenticato | loginID, ECID | loginID |
| autenticato | loginID, ECID | loginID |
| autenticato | CRMID, loginID, ECID | CRMID |
| autenticato | CRMID, ECID | CRMID |
| Non autenticato | ECID | ECID |

**Esempi di grafici**

>[!BEGINTABS]

>[!TAB Scenario a persona singola ideale]

Di seguito è riportato uno scenario di grafico a persona singola con un singolo CRMID e più ID di accesso.

![Uno scenario grafico che include un singolo CRMID e più ID di accesso.](../images/graph-examples/single_crmid.png)

>[!TAB Scenario con grafico a più persone: dispositivo condiviso]

Di seguito è riportato uno scenario di grafico a più persone in cui un dispositivo è condiviso da due persone. In questo scenario, `{ECID:111}` è collegato sia a `{loginID:ID_A}` che a `{loginID:ID_C}` e il precedente collegamento stabilito di `{ECID:111, loginID:ID_A}` viene rimosso.

![Uno scenario di dispositivo condiviso da più persone.](../images/graph-examples/single_crmid_shared_device.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
loginID: ID_C, ECID: 111
```

>[!TAB Scenario con grafico a più persone: dati non validi]

Di seguito è riportato uno scenario di grafico a più persone che coinvolge dati non validi. In questo scenario, `{loginID:ID_D}` è collegato erroneamente a due utenti diversi e il collegamento con la marca temporale precedente viene eliminato, a favore del collegamento stabilito più di recente.

![Scenario di grafico a più persone con dati non validi.](../images/graph-examples/single_crmid_bad_data.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
CRMID: Tom, loginID: ID_D
```

>[!TAB &quot;Dangling&quot; loginID]

Il grafico seguente simula uno scenario di loginID &quot;penzolante&quot;. In questo esempio, due diversi loginID sono associati allo stesso ECID. Tuttavia, `{loginID:ID_C}` non è collegato al CRMID. Pertanto, il servizio Identity non è in grado di rilevare che questi due ID di accesso rappresentano due entità diverse.

![Uno scenario LoginID penzolante.](../images/graph-examples/dangling_example.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
loginID: ID_C, ECID: 111
```

>[!ENDTABS]

## CRMID singolo con più ID di accesso (versione complessa)

In questo scenario, esiste un singolo CRMID che rappresenta un’entità persona. Tuttavia, un’entità persona può avere più identificatori di accesso:

* Una determinata entità persona può avere diversi tipi di conto (personale o aziendale, conto per stato, conto per marchio, ecc.)
* Una determinata entità persona può utilizzare indirizzi e-mail diversi per qualsiasi numero di account.

>[!IMPORTANT]
>
>**È fondamentale che il CRMID venga sempre inviato per ogni utente**. In caso contrario, potrebbe verificarsi uno scenario con ID di accesso &quot;tralasciato&quot;, in cui si presume che una singola persona condivida un dispositivo con un’altra persona.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID | Connettore sorgente Adobe Analytics. <br> **Nota:** per impostazione predefinita, gli AAID sono bloccati in Identity Service, pertanto devi assegnare agli ECID una priorità maggiore rispetto agli AAID quando utilizzi l&#39;origine Analytics. Per ulteriori informazioni, leggere la [guida all&#39;implementazione](./implementation-guide.md#ingest-your-data).</br> |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
```

**Configurazione algoritmo:**

Puoi creare questo scenario nella simulazione del grafico configurando la seguente configurazione per la configurazione dell’algoritmo:

| Priorità | Nome visualizzato | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- | 
| 1 | CRMID | CROSS_DEVICE | Sì |
| 2 | Email_LC_SHA256 | E-mail | No |
| 3 | Telefono_SHA256 | Telefono | No |
| 4 | loginID | CROSS_DEVICE | No |
| 5 | ECID | COOKIE | No |
| 6 | AAID | COOKIE | No |

**Selezione identità primaria per il profilo:**

Nel contesto di questa configurazione, l’identità primaria sarà definita come segue:

| Stato di autenticazione | Spazio dei nomi negli eventi | Identità primaria |
| --- | --- | --- |
| autenticato | loginID, ECID | loginID |
| autenticato | loginID, ECID | loginID |
| autenticato | CRMID, loginID, ECID | CRMID |
| autenticato | CRMID, ECID | CRMID |
| Non autenticato | ECID | ECID |

**Esempi di grafici**

>[!BEGINTABS]

>[!TAB Grafico a persona singola ideale]

Di seguito è riportato un esempio di due grafici a persona singola con un identificatore CRMID e più ID di accesso.

![Un grafico a persona singola che coinvolge un identificatore CRMID e più ID di accesso](../images/graph-examples/complex_single_person.png)

>[!TAB Grafico a più persone: dispositivo condiviso 1]

Di seguito è riportato uno scenario di dispositivo condiviso tra più persone in cui `{ECID:111}` è collegato sia a `{loginID:ID_A}` che a `{loginID:ID_C}`. In questo caso, i collegamenti precedentemente stabiliti vengono rimossi a favore di quelli stabiliti più di recente.

![Scenario grafico dei dispositivi condiviso da più persone.](../images/graph-examples/complex_shared_device_one.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
loginID: ID_C, ECID: 111
```

>[!TAB Grafico a più persone: dispositivo condiviso 2]

In questo scenario, invece di inviare solo il loginID, sia loginID che CRMID vengono inviati come eventi di esperienza.

![Uno scenario con grafico dei dispositivi condiviso da più persone in cui sia l&#39;ID di accesso che il CRMID vengono inviati come eventi di esperienza.](../images/graph-examples/complex_shared_device_two.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
CRMID: Summer, loginID: ID_C, ECID: 111
loginID: ID_A, ECID: 111
```

>[!TAB Grafico a più persone: dati loginID non validi]

In questo scenario, `{loginID:ID_C}` è collegato sia a `{CRMID:Tom}` che a `{CRMID:Summer}` e pertanto è considerato un dato non valido perché gli scenari di grafo ideali non devono collegare gli stessi loginID a due utenti diversi. In questo caso, i vecchi collegamenti stabiliti vengono rimossi a favore di quelli stabiliti più di recente.

![Uno scenario di grafico a più persone che include dati di accesso non validi.](../images/graph-examples/complex_bad_data.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
CRMID: Tom, loginID: ID_C
```

>[!TAB Grafico a più persone: e-mail non univoca]

In questo scenario, un’e-mail non univoca viene collegata a due diversi CRMID, pertanto i collegamenti stabiliti in precedenza vengono rimossi a favore di quelli stabiliti più di recente.

![Scenario di grafico a più persone che include un messaggio e-mail non univoco.](../images/graph-examples/complex_non_unique_email.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
CRMID: Summer, Email_LC_SHA256: aabbcc
```

>[!TAB Grafico a più persone: telefono non univoco]

In questo scenario, un numero di telefono non univoco viene collegato a due diversi CRMID, i collegamenti meno recenti vengono rimossi a favore di quelli più recenti.

![Scenario di grafico a più persone che include un numero di telefono non univoco.](../images/graph-examples/complex_non_unique_phone.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
CRMID: Tom, loginID: ID_A
CRMID: Tom, loginID: ID_B
loginID: ID_A, ECID: 111
CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
CRMID: Summer, loginID: ID_C
CRMID: Summer, loginID: ID_D
loginID: ID_C, ECID: 222
CRMID: Tom, Phone_SHA256: 111-1111
CRMID: Summer, Phone_SHA256: 111-1111
```

>[!ENDTABS]

## Utilizzo in altre Adobe Commerce

Gli esempi di configurazione del grafico riportati in questa sezione descrivono i casi di utilizzo di Adobe Commerce. Gli esempi seguenti si concentrano sui clienti al dettaglio con due tipi di utenti:

* Utente registrato (utenti che hanno creato un account)
* Utenti ospiti (utenti che hanno solo un indirizzo e-mail)

>[!IMPORTANT]
>
>**È fondamentale che il CRMID venga sempre inviato per ogni utente**. In caso contrario, potrebbe verificarsi uno scenario con ID di accesso &quot;tralasciato&quot;, in cui si presume che una singola persona condivida un dispositivo con un’altra persona.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, E-mail, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

```shell
CRMID: Tom, Email: tom@acme.com
CRMID: Tom, ECID: 111
```

**Configurazione algoritmo:**

Puoi creare questo scenario nella simulazione del grafico configurando la seguente configurazione per la configurazione dell’algoritmo:

| Priorità | Nome visualizzato | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- | 
| 1 | CRMID | CROSS_DEVICE | Sì |
| 2 | E-mail | E-mail | Sì |
| 5 | ECID | COOKIE | No |

**Selezione identità primaria per il profilo:**

Nel contesto di questa configurazione, l’identità primaria sarà definita come segue:

| Attività utente | Spazio dei nomi negli eventi | Identità primaria |
| --- | --- | --- |
| Esplorazione autenticata | CRMID, ECID | CRMID |
| Pagamento per gli ospiti | E-mail, ECID | E-mail |
| Esplorazione non autenticata | ECID | ECID |

>[!WARNING]
>
>Gli utenti registrati devono usare sia CRMID che e-mail nei loro profili, affinché i seguenti scenari di grafico funzionino.

**Esempi di grafici**

>[!BEGINTABS]

>[!TAB Grafico a persona singola ideale]

Di seguito è riportato un esempio di grafico ideale a persona singola.

![Esempio di grafico a persona singola ideale con uno spazio dei nomi e-mail.](../images/graph-examples/single_person_email.png)

>[!TAB Grafici a più persone]

Di seguito è riportato un esempio di grafico a più persone in cui due utenti registrati stanno navigando utilizzando lo stesso dispositivo.

![Scenario di grafico a più persone in cui due utenti registrati stanno navigando utilizzando lo stesso dispositivo.](../images/graph-examples/two_registered_users.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email: tom@acme.com
CRMID: Summer, Email: summer@acme.com
CRMID: Tom, ECID: 111
CRMID: Summer, ECID: 111
```

In questo scenario, un utente registrato e un utente guest condividono lo stesso dispositivo.

![Un esempio di grafico a più persone in cui un utente registrato e un ospite condividono lo stesso dispositivo.](../images/graph-examples/one_guest.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, Email: tom@acme.com
CRMID: Tom, ECID: 111
Email: summer@acme.com, ECID: 111
```

In questo scenario, un utente registrato e un utente guest condividono un dispositivo. Tuttavia, si verifica un errore di implementazione poiché il CRMID non contiene uno spazio dei nomi e-mail corrispondente. In questo scenario, Tom è l&#39;utente registrato e Summer è l&#39;utente ospite. A differenza dello scenario precedente, le due entità vengono unite poiché non esistono spazi dei nomi e-mail comuni tra le due entità persona.

![Un esempio di grafico a più persone in cui un utente registrato e un ospite condividono lo stesso dispositivo. Tuttavia, si verifica un errore di implementazione poiché il CRMID non contiene uno spazio dei nomi di posta elettronica.](../images/graph-examples/no_email_namespace_in_crmid.png)

**Input eventi simulazione grafico**

```shell
CRMID: Tom, ECID: 111
Email: summer@acme.com, ECID: 111
```

In questo scenario, due utenti guest condividono lo stesso dispositivo.

![Scenario di grafico con più persone in cui due utenti guest condividono lo stesso dispositivo.](../images/graph-examples/two_guests.png)

**Input eventi simulazione grafico**

```shell
Email: tom@acme.com, ECID: 111
Email: summer@acme.com, ECID: 111
```

In questo caso, un utente guest estrae un elemento e quindi si registra utilizzando lo stesso dispositivo.

![Scenario grafico in cui un utente guest acquista e crea un elemento e quindi si registra per un account.](../images/graph-examples/guest_purchase.png)

**Input eventi simulazione grafico**

```shell
Email: tom@acme.com, ECID: 111
Email: tom@acme.com, CRMID: Tom
CRMID: Tom, ECID: 111
```

>[!ENDTABS]

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico delle identità](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Guida all’implementazione](./implementation-guide.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente simulazione grafico](./graph-simulation.md)
* [Interfaccia utente per le impostazioni delle identità](./identity-settings-ui.md)