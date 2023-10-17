---
title: Logica di collegamento del servizio Identity
description: Scopri in che modo il servizio Identity collega identità diverse per creare una visualizzazione completa di un cliente.
hide: true
hidefromtoc: true
source-git-commit: 03228eef47100096e98666966c4e5065eb7f478a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# Logica di collegamento del servizio Identity

Quando lo spazio dei nomi dell’identità e i valori dell’identità corrispondono, viene stabilito un collegamento tra due identità.

Esistono due tipi di identità collegate:

* **Record profilo**: queste identità di solito provengono dai sistemi di gestione delle relazioni con i clienti.
* **Eventi esperienza**: queste identità provengono in genere dall’implementazione Web SDK o dal sorgente Adobe Analytics.

## Informazioni sulla logica di collegamento del servizio Identity

Un’identità è costituita da uno spazio dei nomi dell’identità e da un valore di identità.

* Uno spazio dei nomi di identità è il contesto di un dato valore di identità a. Esempi comuni di spazi dei nomi di identità includono ID CRM, E-mail e Telefono.
* Un valore di identità è la stringa che rappresenta un’entità del mondo reale. Ad esempio: &quot;julien<span>@acme.com&quot; può essere un valore di identità per uno spazio dei nomi E-mail e 555-555-1234 può essere un valore di identità corrispondente per uno spazio dei nomi Telefono.

>[!TIP]
>
>Lo spazio dei nomi dell’identità è importante perché senza di esso, il valore dell’identità perde il contesto e non avrà informazioni sufficienti per corrispondere correttamente alle identità.

Per una rappresentazione visiva del funzionamento della logica di collegamento del servizio Identity, consulta i seguenti diagrammi:

>[!BEGINTABS]

>[!TAB Grafico esistente]

Supponiamo di avere un grafo di identità esistente con tre identità collegate:

* TEL. (555)-555-1234
* E-MAIL:julien<span>@acme.com
* CRM ID:60013ABC

![grafico esistente](../images/identity-settings/existing-graph.png)

>[!TAB Dati in arrivo]

Una coppia di identità viene acquisita nel grafico e questa coppia contiene:

* CRM ID:60013ABC
* ECID:100066526

![dati in arrivo](../images/identity-settings/incoming-data.png)

>[!TAB Grafico aggiornato]

Identity Service riconosce che CRM ID:60013ABC esiste già nel tuo grafico, e quindi collega solo il nuovo ECID

![grafico aggiornato](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Scenario cliente

In qualità di ingegnere dati, acquisisci il seguente set di dati CRM (record profilo) in Experienci Platform.

| ID del sistema di gestione delle relazioni con i clienti** | Telefono* | E-mail* | Nome | Cognome |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` : indica un campo contrassegnato come identità primaria.
>* `*` : indica un campo contrassegnato come identità secondaria.
>
>Identity Service non distingue tra identità primaria e secondaria. Se un campo è contrassegnato come identità, verrà acquisito in Identity Service.

Hai anche implementato Web SDK e acquisito un set di dati Web SDK (Experience Event) con le seguenti tabelle di dati:

| Marca temporale | Identità nell’evento* | Evento |
| --- | --- | --- |
| `t=1` | ECID:38652 | Visualizza pagina Home |
| `t=2` | ECID:38652, ID CRM:31260XYZ | Cerca scarpe |
| `t=3` | ECID:44675 | Visualizza pagina Home |
| `t=4` | ECID:44675, ID CRM: 31260XYZ | Visualizza cronologia acquisti |

>[!NOTE]
>
>* `*` - Indica un campo contrassegnato come identità, con ECID contrassegnato come primario.
>* Per impostazione predefinita, l’identificatore della persona (in questo caso, l’ID del sistema di gestione delle relazioni con i clienti) è designato come identità primaria. Se l’identificatore della persona non esiste, allora l’identificatore del cookie (in questo caso, l’ECID) diventa l’identità primaria.

In questo esempio:

* `t=1`, utilizzava un computer desktop (ECID:38652) e per visualizzare la home page in modo anonimo.
* `t=2`, utilizzava lo stesso computer desktop, accedeva (CRM ID:31260XYZ) e cercava le scarpe.
   * Una volta effettuato l’accesso, l’evento invia sia l’ECID che l’ID del sistema di gestione delle relazioni con i clienti al servizio Identity.
* `t=3`, utilizzava un computer portatile (ECID:44675) e navigava in modo anonimo.
* `t=4`, utilizzava lo stesso computer portatile, accedeva (ID gestione delle relazioni con i clienti: 31260XYZ) e visualizzava la cronologia degli acquisti.


>[!BEGINTABS]

>[!TAB timestamp=0]

A `timestamp=0`, disponi di due grafici di identità per due clienti diversi. Entrambi sono rappresentati da tre identità collegate.

| | ID del sistema di gestione delle relazioni con i clienti | E-mail | Telefono |
| --- | --- | --- | --- |
| Cliente uno | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Cliente due | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

A `timestamp=1`, un cliente utilizza un laptop per visitare il sito web di e-commerce, visualizzare la pagina principale e navigare in modo anonimo. Questo evento di navigazione anonimo è identificato come ECID:38652. Poiché il servizio Identity memorizza solo gli eventi con almeno due identità, queste informazioni non vengono memorizzate.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

A `timestamp=2`, un cliente utilizza lo stesso laptop per visitare il sito web di e-commerce. Accedono con la combinazione di nome utente e password e cercano le scarpe. Identity Service identifica l’account del cliente quando effettua l’accesso perché corrisponde al suo ID CRM: 31260XYZ. Inoltre, Identity Service mette in relazione ECID:38562 con CRM ID:31260XYZ, in quanto entrambi utilizzano lo stesso browser sullo stesso dispositivo.

![timestamp-due](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

A `timestamp=3` un cliente utilizza un tablet per visitare il sito web di e-commerce e navigare in modo anonimo. Questo evento di navigazione anonimo è identificato come ECID:44675. Poiché il servizio Identity memorizza solo gli eventi con almeno due identità, queste informazioni non vengono memorizzate.

![timestamp-tre](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

A `timestamp=4`, un cliente utilizza lo stesso tablet, accede al proprio account (CRM ID:31260XYZ) e visualizza la cronologia degli acquisti. Questo evento collega il relativo ID CRM:31260XYZ all’identificatore del cookie assegnato all’attività di navigazione anonima, ECID:44675, e collega ECID:44675 al grafico delle identità del cliente 2.

![timestamp-quattro](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico delle identità](./overview.md)
* [Scenari di esempio per la configurazione delle regole di collegamento del grafico delle identità](./example-scenarios.md)
* [Servizio Identity e Real-Time Customer Profile](identity-and-profile.md)
