---
title: Esempi di configurazioni
description: Scopri di più sulle configurazioni di esempio con utilizzando lo strumento di simulazione del grafico.
badge: Beta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 10%

---

# Esempio di configurazioni del grafico

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo delle identità sono attualmente in versione beta. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione. La funzione e la documentazione sono soggette a modifiche.

>[!NOTE]
>
>* &quot;CRMID&quot; e &quot;loginID&quot; sono spazi dei nomi personalizzati. In questo documento, &quot;CRMID&quot; è un identificatore di persona e &quot;loginID&quot; è un identificatore di accesso associato a una determinata persona.
>* Per simulare gli scenari del grafico di esempio descritti in questo documento, devi innanzitutto creare due spazi dei nomi personalizzati, uno con il simbolo di identità &quot;CRMID&quot; e un altro con il simbolo di identità &quot;loginID&quot;. I simboli di identità fanno distinzione tra maiuscole e minuscole.

Questo documento illustra configurazioni grafiche di esempio di scenari comuni che potrebbero verificarsi quando si utilizzano dati di identità.

## Solo CRMID

Questo è un esempio di un semplice scenario di implementazione in cui gli eventi online (CRMID ed ECID) vengono acquisiti e gli eventi offline (record di profilo) vengono memorizzati solo in base al CRMID.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

* CRMID: Tom, ECID: 111

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

>[!BEGINTABS]

>[!TAB Scenario grafico a persona singola ideale]

Di seguito è riportato un esempio di grafico ideale a persona singola, in cui il CRMID è univoco e riceve la priorità più elevata.

![Esempio simulato di un grafico a persona singola ideale, in cui il CRMID è univoco e a cui viene assegnata la priorità più elevata.](../images/graph-examples/crmid_only_single.png)

>[!TAB scenario grafico con più persone]

Di seguito è riportato un esempio di grafico a più persone. In questo esempio viene visualizzato lo scenario &quot;dispositivo condiviso&quot;, in cui sono presenti due CRMID e viene rimosso quello con il collegamento stabilito precedente.

![Esempio simulato di un grafico a più persone. In questo esempio viene visualizzato uno scenario di dispositivo condiviso, in cui sono presenti due CRMID e il collegamento stabilito precedente viene rimosso.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## CRMID con e-mail con hash

In questo scenario, viene acquisito un CRMID che rappresenta sia dati online (evento esperienza) che offline (record profilo). Questo scenario comporta anche l’acquisizione di un’e-mail con hash, che rappresenta un altro spazio dei nomi inviato nel set di dati del record di gestione delle relazioni con i clienti insieme al CRMID.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, E-mail_LC_SHA256, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

* CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRMID: Tom, ECID: 111
* CRMID: Summer, Email_LC_SHA256: summer<span>@acme.com
* CRMID: Summer, ECID: 222

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

>[!BEGINTABS]

>[!TAB Scenario grafico a persona singola ideale]

![In questo esempio vengono generati due grafici distinti, ciascuno dei quali rappresenta un&#39;entità a persona singola.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB grafico a più persone: dispositivo condiviso]

![In questo esempio, il grafico simulato visualizza uno scenario di &quot;dispositivo condiviso&quot; perché sia Tom che Summer sono associati allo stesso ECID.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB grafico a più persone: e-mail non univoca]

![Questo scenario è simile a uno scenario &quot;dispositivo condiviso&quot;. Tuttavia, invece di avere le entità persona condivise ECID, esse vengono associate allo stesso account e-mail.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID con e-mail con hash, telefono con hash, GAID e IDFA

Questo scenario è simile a quello precedente. Tuttavia, in questo scenario, le e-mail e il telefono con hash vengono contrassegnati come identità da utilizzare nella corrispondenza dei segmenti.

**Implementazione:**

| Namespace utilizzati | Metodo di raccolta del comportamento Web |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | SDK per web |

**Eventi:**

Puoi creare questo scenario nella simulazione del grafico copiando i seguenti eventi in modalità testo:

* CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: Tom, ECID: 111
* CRMID: Tom, ECID: 222, IDFA: A-A-A
* CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Summer, ECID: 333
* CRMID: Summer, ECID: 444, GAID:B-B-B

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

>[!BEGINTABS]

>[!TAB Scenario grafico a persona singola ideale]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->
