---
title: Regole di collegamento del grafico delle identità
description: Scopri le regole di collegamento del grafico identità in Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: c9b5de33de91b93f179b4720f692eb876e94df72
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 7%

---

# Panoramica di [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Regole di collegamento del grafo delle identità"
>abstract="Per evitare queste unioni indesiderate, puoi utilizzare le configurazioni fornite tramite le Regole di collegamento del grafico identità e consentire una personalizzazione accurata per i tuoi utenti."

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules] è ora generalmente disponibile. Se disponi di una sandbox esistente che, dopo aver abilitato le impostazioni di identità, richiede che i grafici compressi non vengano compressi (&quot;corretti&quot;), contatta il supporto Adobe.

Con il servizio Adobe Experience Platform Identity e il profilo cliente in tempo reale, è facile presumere che i dati siano acquisiti perfettamente e che tutti i profili uniti rappresentino una singola persona tramite un identificatore di persona, come un CRMID. Tuttavia, esistono scenari possibili in cui alcuni dati potrebbero tentare di unire più profili disparati in un unico profilo (&quot;compressione del grafico&quot;). Per evitare queste unioni indesiderate, puoi utilizzare le configurazioni fornite tramite [!DNL Identity Graph Linking Rules] e consentire una personalizzazione accurata per i tuoi utenti.

## Introduzione

I seguenti documenti sono essenziali per comprendere [!DNL Identity Graph Linking Rules].

* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Guida all’implementazione](./implementation-guide.md)
* [Esempi di configurazioni del grafico](./example-configurations.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente simulazione grafico](./graph-simulation.md)
* [Interfaccia utente per le impostazioni delle identità](./identity-settings-ui.md)

## Raccolta video

Guarda i video seguenti per scoprire alcuni degli aspetti fondamentali delle regole di collegamento del grafico delle identità.

<!-- CARDS
{target = _blank}
* https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/overview
* https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation 

    {description = Learn how to use the graph simulator to test out identity graph linking rules.}

* https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings
    {description = Learn how to enable and configure identity graph linking rules to build accurate customer profiles}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" title="Panoramica delle regole di collegamento del grafo delle identità" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3448250/?format=jpeg&nocache=1747851655227" alt="Panoramica delle regole di collegamento del grafo delle identità"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" title="Panoramica delle regole di collegamento del grafo delle identità">Panoramica delle regole di collegamento del grafo delle identità</a>
                    </p>
                    <p class="is-size-6">Ottieni una panoramica del modo in cui le regole di collegamento del grafo delle identità consentono ai data architect di mantenere profili cliente accurati ed evitare l’unione non intenzionale dei grafi di due persone distinte.</p>
                </div>
                <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Graph Simulation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" title="Regole di collegamento del grafico delle identità - Simulazione del grafico" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3444032/?format=jpeg&nocache=1747851655237" alt="Regole di collegamento del grafico delle identità - Simulazione del grafico"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" title="Regole di collegamento del grafico delle identità - Simulazione del grafico">Regole di collegamento per il grafo delle identità - Simulazione del grafo</a>
                    </p>
                    <p class="is-size-6">Scopri come utilizzare il simulatore grafico per testare le regole di collegamento del grafico delle identità.</p>
                </div>
                <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Identity settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" title="Regole di collegamento del grafo delle identità - Impostazioni identità" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3458487/?format=jpeg&nocache=1747851655218" alt="Regole di collegamento del grafo delle identità - Impostazioni identità"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" title="Regole di collegamento del grafo delle identità - Impostazioni identità">Regole di collegamento del grafo delle identità - Impostazioni identità</a>
                    </p>
                    <p class="is-size-6">Scopri come abilitare e configurare le regole di collegamento del grafico delle identità per creare profili cliente precisi</p>
                </div>
                <a href="https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


## Scenari di collasso dei grafici {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Scenari di collasso dei grafici"
>abstract="Ci sono più motivi per cui i grafici potrebbero “collassare” o rappresentare più entità persona."

In questa sezione vengono descritti alcuni scenari di esempio da considerare durante la configurazione di [!DNL Identity Graph Linking Rules].

### Dispositivo condiviso

Esistono casi in cui si possono verificare più accessi su un singolo dispositivo:

| Dispositivo condiviso | Descrizione |
| --- | --- |
| Family computer e tablet | Marito e moglie accedono entrambi ai rispettivi conti bancari. |
| Chiosco pubblico | I viaggiatori che si registrano in aeroporto utilizzando il proprio ID fedeltà per effettuare il check-in delle borse e stampare le carte d’imbarco. |
| Call center | Il personale del call center accede a un singolo dispositivo per conto dei clienti che chiamano l’assistenza clienti per risolvere i problemi. |

![Diagramma di alcuni dispositivi condivisi comuni.](../images/identity-settings/shared-devices.png "Diagramma di alcuni dispositivi condivisi comuni."){zoomable="yes"}

In questi casi, dal punto di vista del grafico, senza limiti abilitati, un singolo ECID sarà collegato a più CRMID.

Con [!DNL Identity Graph Linking Rules] è possibile:

* Configura l’ID utilizzato per l’accesso come identificatore univoco. Ad esempio, puoi limitare un grafico per memorizzare una sola identità con uno spazio dei nomi CRMID e quindi definire tale CRMID come identificatore univoco di un dispositivo condiviso.
   * In questo modo, puoi evitare che i CRMID vengano uniti dall’ECID.

### Scenari e-mail/telefono non validi

Ci sono anche esempi di utenti che forniscono valori falsi come numeri di telefono e/o indirizzi e-mail al momento della registrazione. In questi casi, se i limiti non sono abilitati, le identità relative a telefono/e-mail finiranno per essere collegate a più CRMID diversi.

![Diagramma che rappresenta scenari di posta elettronica o telefono non validi.](../images/identity-settings/invalid-email-phone.png "Diagramma che rappresenta scenari di posta elettronica o telefono non validi."){zoomable="yes"}

Con [!DNL Identity Graph Linking Rules] è possibile:

* Configura il CRMID, il numero di telefono o l’indirizzo e-mail come identificatore univoco e limita quindi una persona a un solo CRMID, numero di telefono e/o indirizzo e-mail associato al suo account.

### Valori di identità errati o errati

In alcuni casi, valori di identità errati e non univoci vengono acquisiti nel sistema, indipendentemente dallo spazio dei nomi. Gli esempi includono:

* Spazio dei nomi IDFA con valore di identità &quot;user_null&quot;.
   * I valori di identità IDFA devono contenere 36 caratteri: 32 caratteri alfanumerici e quattro trattini.
* Spazio dei nomi del numero di telefono con valore di identità &quot;non specificato&quot;.
   * I numeri di telefono non devono contenere caratteri dell’alfabeto.

Queste identità possono causare i seguenti grafici, in cui più identificatori CRMID vengono uniti insieme all’identità &quot;bad&quot;:

![Esempio di grafico di dati di identità con valori di identità errati o non validi.](../images/identity-settings/bad-data.png "Esempio di grafico di dati di identità con valori di identità errati o non validi."){zoomable="yes"}

Con [!DNL Identity Graph Linking Rules] è possibile configurare il CRMID come identificatore univoco per evitare la compressione del profilo indesiderata a causa di questo tipo di dati.

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

Con [!DNL Identity Graph Linking Rules] è possibile:

* Crea un singolo grafo di identità/profilo unito per ogni utente configurando spazi dei nomi univoci, che impedirà a due identificatori di persona diversi di unirsi in un unico grafo di identità.
* Associa eventi online autenticati alla persona configurando le priorità

### Terminologia {#terminology}

| Terminologia | Descrizione |
| --- | --- |
| Spazio dei nomi univoco | Uno spazio dei nomi univoco è uno spazio dei nomi delle identità che è stato impostato per essere distinto all’interno del contesto di un grafo delle identità. Puoi configurare uno spazio dei nomi in modo che sia univoco utilizzando l’interfaccia utente. Una volta definito uno spazio dei nomi come univoco, un grafo può avere una sola identità che lo contiene. |
| Priorità dello spazio dei nomi | La priorità dello spazio dei nomi si riferisce all’importanza relativa degli spazi dei nomi rispetto agli altri. La priorità dello spazio dei nomi è configurabile tramite l’interfaccia utente. Puoi classificare gli spazi dei nomi in un dato grafico delle identità. Una volta abilitata, la priorità dei nomi verrà utilizzata in vari scenari, ad esempio per l’input dell’algoritmo di ottimizzazione delle identità e per la determinazione dell’identità primaria dei frammenti di evento esperienza. |
| Algoritmo di ottimizzazione identità | L’algoritmo di ottimizzazione delle identità garantisce che le linee guida create configurando uno spazio dei nomi e priorità dello spazio dei nomi univoci vengano applicate in un dato grafico delle identità. |

### Spazio dei nomi univoco {#unique-namespace}

Puoi configurare uno spazio dei nomi in modo che sia univoco utilizzando l’area di lavoro dell’interfaccia utente per le impostazioni delle identità. In questo modo, informa l’algoritmo di ottimizzazione delle identità che un dato grafo può avere una sola identità che contiene quello spazio dei nomi univoco. Questo impedisce l’unione di due identificatori di persona diversi all’interno dello stesso grafico.

Considera lo scenario seguente:

* Scott utilizza un tablet e apre il browser Google Chrome per andare su acme<span>.com, dove accede e cerca nuove scarpe da basket.
   * Dietro le quinte, questo scenario registra le seguenti identità:
      * Uno spazio dei nomi e un valore ECID per rappresentare l’utilizzo del browser
      * Uno spazio dei nomi e un valore CRMID per rappresentare l&#39;utente autenticato (Scott ha effettuato l&#39;accesso con la combinazione di nome utente e password).
* Suo figlio Peter utilizza quindi lo stesso tablet e utilizza anche Google Chrome per visitare il sito acme<span>.com, dove accede con il proprio account per cercare attrezzature per il calcio.
   * Dietro le quinte, questo scenario registra le seguenti identità:
      * Lo stesso spazio dei nomi e valore ECID per rappresentare il browser.
      * Nuovo spazio dei nomi e valore CRMID per rappresentare l’utente autenticato.

Se CRMID è stato configurato come uno spazio dei nomi univoco, l’algoritmo di ottimizzazione delle identità divide i CRMID in due grafici di identità separati, invece di unirli.

Se non configuri uno spazio dei nomi univoco, potresti riscontrare unioni di grafici indesiderate, ad esempio due identità con lo stesso spazio dei nomi CRMID, ma valori di identità diversi (scenari come questi spesso rappresentano due entità persona diverse nello stesso grafico).

Devi configurare uno spazio dei nomi univoco per informare l’algoritmo di ottimizzazione delle identità in modo da applicare limitazioni ai dati di identità acquisiti in un dato grafico delle identità.

### Priorità dello spazio dei nomi {#namespace-priority}

La priorità dello spazio dei nomi si riferisce all’importanza relativa degli spazi dei nomi rispetto agli altri. La priorità dello spazio dei nomi è configurabile tramite l’interfaccia utente e puoi classificare gli spazi dei nomi in un dato grafico delle identità.

Uno dei modi in cui viene utilizzata la priorità dello spazio dei nomi è determinare l’identità primaria dei frammenti di eventi esperienza (comportamento dell’utente) nel profilo cliente in tempo reale. Se sono configurate le impostazioni di priorità, l’impostazione di identità primaria sul Web SDK non verrà più utilizzata per determinare quali frammenti di profilo sono archiviati.

Nell’area di lavoro dell’interfaccia utente delle impostazioni delle identità è possibile configurare spazi dei nomi e priorità dello spazio dei nomi univoci. Tuttavia, gli effetti delle loro configurazioni sono diversi:

| | Identity Service | Profilo cliente in tempo reale |
| --- | --- | --- |
| Spazio dei nomi univoco | In Identity Service, l’algoritmo di ottimizzazione delle identità fa riferimento a spazi dei nomi univoci per determinare i dati di identità acquisiti in un dato grafo di identità. | Gli spazi dei nomi univoci non influiscono sul profilo cliente in tempo reale. |
| Priorità dello spazio dei nomi | In Identity Service, per i grafici che hanno più livelli, la priorità dello spazio dei nomi determinerà la rimozione dei collegamenti appropriati. | Quando un evento esperienza viene acquisito in Profilo, lo spazio dei nomi con priorità più elevata diventa l’identità primaria del frammento di profilo. |

* La priorità dello spazio dei nomi non influisce sul comportamento del grafico quando viene raggiunto il limite di 50 identità per grafico.
* **La priorità dello spazio dei nomi è un valore numerico** assegnato a uno spazio dei nomi che ne indica l&#39;importanza relativa. Si tratta di una proprietà di uno spazio dei nomi.
* **L&#39;identità primaria è l&#39;identità in cui è archiviato un frammento di profilo rispetto a**. Un frammento di profilo è un record di dati che memorizza informazioni su un determinato utente: attributi (di solito acquisiti tramite record di gestione delle relazioni con i clienti) o eventi (di solito acquisiti da eventi di esperienza o dati online).
* La priorità dello spazio dei nomi determina l’identità primaria dei frammenti dell’evento esperienza.
   * Per i record di profilo, puoi utilizzare l’area di lavoro schemi nell’interfaccia utente di Experience Platform per definire i campi di identità, inclusa l’identità primaria. Per ulteriori informazioni, consulta la guida su [definizione dei campi di identità nell&#39;interfaccia utente](../../xdm/ui/fields/identity.md).
* Se un evento esperienza ha due o più identità con la priorità più elevata per lo spazio dei nomi in identityMap, verrà rifiutato dall’acquisizione perché verrà considerato come &quot;dati non validi&quot;. Ad esempio, se identityMap contiene `{ECID: 111, CRMID: John, CRMID: Jane}`, l&#39;intero evento verrà rifiutato come dati non validi perché implica che l&#39;evento sia associato contemporaneamente a `CRMID: John` e `CRMID: Jane`.

Per ulteriori informazioni, leggere la guida sulla [priorità dello spazio dei nomi](./namespace-priority.md).

## Passaggi successivi

Per ulteriori informazioni su [!DNL Identity Graph Linking Rules], leggere la seguente documentazione:

* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Guida all’implementazione](./implementation-guide.md)
* [Esempi di configurazioni del grafico](./example-configurations.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente simulazione grafico](./graph-simulation.md)
* [Interfaccia utente per le impostazioni delle identità](./identity-settings-ui.md)