---
title: Guida alla risoluzione dei problemi per le regole di collegamento del grafico identità
description: Scopri come risolvere i problemi comuni nelle regole di collegamento del grafico delle identità.
badge: Beta
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: 56e2e359812fcbfd011505ad917403d6f5317b4a
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi per le regole di collegamento del grafico delle identità

>[!AVAILABILITY]
>
>La funzione delle regole di collegamento del grafo delle identità è attualmente in versione beta. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione. La funzione e la documentazione sono soggette a modifiche.

Durante il test e la convalida delle regole di collegamento del grafico delle identità, potresti riscontrare alcuni problemi relativi all’acquisizione dei dati e al comportamento del grafico. Leggi questo documento per scoprire come risolvere alcuni problemi comuni che potrebbero verificarsi quando utilizzi le regole di collegamento del grafico delle identità.

## Panoramica sul flusso di acquisizione dei dati {#data-ingestion-flow-overview}

Il diagramma seguente è una rappresentazione semplificata del modo in cui i dati fluiscono in Adobe Experience Platform e Applications. Utilizza questo diagramma come riferimento per comprendere meglio i contenuti di questa pagina.

![Diagramma del flusso dell&#39;acquisizione dei dati in Identity Service.](../images/troubleshooting/dataflow_in_identity.png)

È importante notare i seguenti fattori:

* Per i dati in streaming, Real-Time Customer Profile, Identity Service e data lake inizieranno a elaborare i dati quando vengono inviati. Tuttavia, la latenza per completare l’elaborazione dei dati dipende dal servizio. In genere, l’elaborazione del data lake richiede un tempo più lungo rispetto a Profilo e Identità.
   * Se i dati non vengono visualizzati durante l’esecuzione di una query su un set di dati anche dopo un paio d’ore, è probabile che i dati non siano stati acquisiti in Experience Platform.
* Per i dati batch, tutti i dati fluiranno prima nel data lake, quindi i dati verranno propagati a Profilo e Identità se il set di dati è abilitato per Profilo e Identità.
* Per i problemi relativi all’acquisizione, è importante che il problema venga isolato a livello di servizio per consentire una risoluzione accurata dei problemi e il debug. Esistono tre tipi di problemi potenziali da considerare:

| Tipo di problema di acquisizione | I dati vengono acquisiti nel data lake? | I dati vengono acquisiti nel profilo? | I dati vengono acquisiti in Identity Service? |
| --- | --- | --- | --- |
| Problema generale di acquisizione | No | No | No |
| Problema del grafico | Sì | Sì | No |
| Problema relativo al frammento di profilo | Sì | No | Sì |

## Problemi di acquisizione dei dati {#data-ingestion-issues}

>[!NOTE]
>
>* Questa sezione presuppone che i dati siano stati correttamente acquisiti nel data lake e che non ci sia stata alcuna sintassi o altri errori che avrebbero impedito, in primo luogo, l’acquisizione dei dati in Experience Platform.
>
>* Negli esempi vengono utilizzati ECID come spazio dei nomi dei cookie e CRMID come spazio dei nomi della persona.

### Le mie identità non vengono acquisite in Identity Service{#my-identities-are-not-getting-ingested-into-identity-service}

Questo può accadere per vari motivi, tra cui, ma non solo:

* [Set di dati non abilitato per il profilo](../../catalog/datasets/enable-for-profile.md).
* Il record viene ignorato perché nell’evento è presente una sola identità.
* [Errore di convalida in Identity Service](../guardrails.md#identity-value-validation).
   * Ad esempio, un ECID potrebbe aver superato la lunghezza massima di 38 caratteri.
* Per impostazione predefinita, [AAID non possono essere acquisiti](../guardrails.md#identity-namespace-ingestion).
* L&#39;identità è stata rimossa a causa di [guardrail di sistema](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated).

Nel contesto delle regole di collegamento del grafo delle identità, un record può essere rifiutato da Identity Service perché l’evento in ingresso ha due o più identità con lo stesso spazio dei nomi univoco ma un valore di identità diverso. Questo scenario si verifica in genere a causa di errori di implementazione.

Considera il seguente evento con due presupposti:

* Il nome del campo CRMID è contrassegnato come identità con lo spazio dei nomi CRMID.
* Il CRMID dello spazio dei nomi è definito come uno spazio dei nomi univoco.

L’evento seguente restituisce un messaggio di errore che indica che l’acquisizione non è riuscita.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**Risoluzione dei problemi**

Per risolvere l&#39;errore, è necessario innanzitutto raccogliere le informazioni seguenti:

* Valore di identità (`identity_value`) previsto per essere acquisito nel grafico delle identità.
* Set di dati (`dataset_name`) in cui è stato inviato l&#39;evento.

Quindi, utilizzare [Adobe Experience Platform Query Service](../../query-service/home.md) ed eseguire la seguente query:

>[!TIP]
>
>Sostituisci `dataset_name` e `identity_value` con le informazioni raccolte.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

Dopo aver eseguito la query, individua il record dell’evento che si prevedeva di generare un grafico, quindi verifica che i valori di identità siano diversi nella stessa riga. Per un esempio, visualizza l’immagine seguente:

![Query senza titolo che ha restituito spazi dei nomi duplicati.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Se le due identità sono esattamente le stesse e se l’evento viene acquisito tramite streaming, sia Identità che Profilo deduplicheranno l’identità.

### I miei frammenti di evento esperienza non vengono acquisiti nel profilo {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Esistono diversi motivi che contribuiscono al motivo per cui i frammenti di evento esperienza non vengono acquisiti in Profilo, tra cui:

* [Set di dati non abilitato per il profilo](../../catalog/datasets/enable-for-profile.md).
* [Errore di convalida nel profilo](../../xdm/classes/experienceevent.md).
   * Ad esempio, un evento esperienza deve contenere sia `_id` che `timestamp`.
   * Inoltre, `_id` deve essere univoco per ogni evento (record).

Nel contesto della priorità dello spazio dei nomi, Profile rifiuterà qualsiasi evento che contiene due o più identità con la priorità dello spazio dei nomi più elevata. Ad esempio, se GAID non è contrassegnato come spazio dei nomi univoco e sono presenti due identità con uno spazio dei nomi GAID e valori di identità diversi, l’evento non verrà memorizzato in Profilo.

**Risoluzione dei problemi**

Per risolvere questo errore, leggere i passaggi per la risoluzione dei problemi descritti nella guida precedente su [errori di risoluzione dei problemi relativi ai dati non acquisiti in Identity Service](#my-identities-are-not-getting-ingested-into-identity-service).

### I miei frammenti di evento esperienza vengono acquisiti, ma hanno l’identità primaria &quot;errata&quot; nel profilo

La priorità dello spazio dei nomi svolge un ruolo importante nel modo in cui i frammenti di evento determinano l’identità primaria.

* Dopo aver configurato e salvato le [impostazioni identità](./identity-settings-ui.md) per una data sandbox, il profilo utilizzerà [priorità spazio dei nomi](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) per determinare l&#39;identità primaria. Nel caso di identityMap, il profilo non utilizzerà più il flag `primary=true`.
* Anche se il profilo non farà più riferimento a questo flag, gli altri servizi in Experience Platform potrebbero continuare a utilizzare il flag `primary=true`.

Affinché [eventi utente autenticati](configuration.md#ingest-your-data) siano associati allo spazio dei nomi della persona, tutti gli eventi autenticati devono contenere lo spazio dei nomi della persona (CRMID). Ciò significa che anche dopo che un utente effettua l’accesso, lo spazio dei nomi della persona deve essere ancora presente in ogni evento autenticato.

Puoi continuare a visualizzare il flag &#39;eventi&#39; di `primary=true` durante la ricerca di un profilo nel visualizzatore di profili. Tuttavia, questo viene ignorato e non verrà utilizzato dal profilo.

AAID sono bloccati per impostazione predefinita. Pertanto, se utilizzi il [connettore di origine Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md), assicurati che l&#39;ECID abbia una priorità più alta rispetto all&#39;ECID in modo che gli eventi non autenticati abbiano un&#39;identità primaria di ECID.

**Risoluzione dei problemi**

* Per verificare che gli eventi autenticati contengano sia lo spazio dei nomi della persona che quello dei cookie, leggere i passaggi descritti nella sezione relativa alla risoluzione di [errori relativi ai dati non acquisiti in Identity Service](#my-identities-are-not-getting-ingested-into-identity-service).
* Per verificare che gli eventi autenticati abbiano l’identità primaria dello spazio dei nomi della persona (ad esempio, CRMID), cerca lo spazio dei nomi della persona nel visualizzatore profili senza unire i criteri di unione (questo è il criterio di unione che non utilizza un grafico privato). Questa ricerca restituirà solo gli eventi associati allo spazio dei nomi della persona.

## Problemi relativi al comportamento del grafico {#graph-behavior-related-issues}

Questa sezione illustra i problemi comuni che potresti incontrare sul funzionamento del grafo delle identità.

### L’identità viene collegata alla persona &quot;sbagliata&quot;

L&#39;algoritmo di ottimizzazione delle identità rispetterà [i collegamenti stabiliti più di recente e rimuoverà i collegamenti meno recenti](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). Pertanto, una volta abilitata questa funzione, gli ECID potrebbero essere riassegnati (ricollegati) da una persona all’altra. Per comprendere la cronologia del modo in cui un’identità viene collegata nel tempo, segui i passaggi seguenti:

**Risoluzione dei problemi**

>[!NOTE]
>
>La procedura seguente consente di recuperare le informazioni in base ai seguenti presupposti:
>
>* È in uso un singolo set di dati (non verranno eseguiti query su più set di dati).
>
>* I dati non vengono eliminati dal data lake a causa dell&#39;eliminazione da parte di [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) o di altri servizi che eseguono l&#39;eliminazione.

Innanzitutto, devi raccogliere le seguenti informazioni:

* Il simbolo di identità (namespaceCode) dello spazio dei nomi del cookie (ad esempio ECID) e dello spazio dei nomi della persona (ad esempio CRMID) che sono stati inviati.
   * Per le implementazioni dell’SDK web, in genere si tratta degli spazi dei nomi inclusi in identityMap.
   * Per le implementazioni del connettore di origine di Analytics, si tratta dell’identificatore del cookie incluso in identityMap. L’identificatore della persona è un campo eVar contrassegnato come identità.
* Set di dati in cui è stato inviato l’evento (dataset_name).
* Il valore di identità dello spazio dei nomi del cookie da cercare (identity_value).

I simboli di identità (namespaceCode) fanno distinzione tra maiuscole e minuscole. Per recuperare tutti i simboli di identità per un dato set di dati in identityMap, esegui la seguente query:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Se non conosci il valore di identità dell’identificatore del cookie e desideri cercare un ID cookie che sarebbe stato collegato a più identificatori di persona, devi eseguire la seguente query. Questa query assume ECID come spazio dei nomi dei cookie e CRMID come spazio dei nomi della persona.

>[!BEGINTABS]

>[!TAB Implementazione Web SDK]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Implementazione del connettore di origine di Analytics]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Nota:** personID fa riferimento al percorso del descrittore. Puoi trovare queste informazioni negli schemi.

>[!ENDTABS]

Quindi, esamina l’associazione dello spazio dei nomi del cookie in ordine di marca temporale eseguendo la seguente query:

>[!BEGINTABS]

>[!TAB Implementazione Web SDK]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Implementazione del connettore di origine di Analytics]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Nota**: questo esempio presuppone che `eVar10` sia contrassegnato come identità. Per le configurazioni, devi modificare l’eVar in base all’implementazione dell’organizzazione.

>[!ENDTABS]

### L&#39;algoritmo di ottimizzazione delle identità non funziona come previsto

**Risoluzione dei problemi**

Consulta la documentazione sull&#39;[algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md) e i tipi di strutture di grafo supportati.

* Per esempi di strutture di grafo supportate, consulta la [guida alla configurazione del grafo](./example-configurations.md).
* È inoltre possibile leggere la [guida all&#39;implementazione](./configuration.md#appendix) per esempi di strutture di grafico non supportate. Esistono due scenari possibili:
   * Non esiste un singolo spazio dei nomi in tutti i profili.
   * Si verifica uno scenario [&quot;ID pendente&quot;](./configuration.md#dangling-loginid-scenario). In questo scenario, il servizio Identity non è in grado di determinare se l’ID penzolante è associato a una qualsiasi delle entità persona nei grafici.

Puoi anche utilizzare lo strumento di simulazione del grafico [nell&#39;interfaccia utente](./graph-simulation.md) per simulare eventi e configurare le impostazioni univoche dello spazio dei nomi e della priorità dello spazio dei nomi. Questo può aiutarti a capire come dovrebbe comportarsi l’algoritmo di ottimizzazione delle identità.

Se i risultati della simulazione corrispondono alle aspettative di comportamento del grafico, puoi verificare se le [impostazioni identità](./identity-settings-ui.md) corrispondono alle impostazioni configurate nella simulazione.

### Continuo a vedere grafici compressi nella sandbox anche dopo aver configurato le impostazioni di identità

I grafi di identità rispetteranno lo spazio dei nomi univoco configurato e la priorità dello spazio dei nomi _dopo_ il salvataggio delle impostazioni. Eventuali grafici &quot;compressi&quot; esistenti _prima_ del salvataggio delle nuove impostazioni non saranno interessati, finché non verranno acquisiti nuovi dati in modo tale che il grafico compresso venga aggiornato. L’identità primaria dei frammenti di evento in Real-Time Customer Profile non verrà aggiornata nemmeno dopo le modifiche di priorità dello spazio dei nomi.

**Risoluzione dei problemi**

Puoi usare [visualizzatore grafo identità](../features/identity-graph-viewer.md) per verificare se il grafo è stato acquisito prima o dopo le impostazioni. Esamina l&#39;ultimo timestamp aggiornato in [!UICONTROL Proprietà collegamento] per vedere quando Identity Service ha acquisito il grafico. Se la marca temporale è precedente alla configurazione, ciò suggerisce che il grafico &quot;compresso&quot; è stato creato prima di abilitare la funzione.

![Visualizzatore del grafico delle identità con un grafico di esempio.](../images/troubleshooting/graph_viewer.png)

### Voglio sapere quanti grafici &quot;compressi&quot; esistono nella mia sandbox

Utilizza il dashboard delle identità per ottenere informazioni sullo stato del grafico delle identità, ad esempio il conteggio di identità e grafici. Per un conteggio dei grafici compressi, consulta la metrica &quot;Conteggio dei grafici con più spazi dei nomi&quot;: si tratta di grafici che contengono due o più identità con lo stesso spazio dei nomi. Supponendo che la sandbox non disponga di dati e che uno spazio dei nomi (ad esempio, CRMID) sia stato configurato come univoco, l’aspettativa è che non ci siano grafici con due o più CRMID. Nell’esempio seguente, sono presenti due grafici che contengono due o più indirizzi e-mail.

![Dashboard delle identità con metriche per conteggio identità, conteggio grafico, conteggio per spazio dei nomi, conteggio grafico per dimensione e conteggio grafico di grafici con più di due spazi dei nomi.](../images/troubleshooting/identity_dashboard.png)

Puoi trovare un raggruppamento dettagliato nel [set di dati di esportazione snapshot del profilo](../../dashboards/query.md) nel data lake eseguendo la query seguente:

>[!NOTE]
>
>* Sostituisci `dataset_name` con il nome effettivo del set di dati.
>
>* I conteggi potrebbero non corrispondere esattamente. Il dashboard delle identità è basato sul conteggio del grafico delle identità e la seguente query è basata sul conteggio dei profili con due o più identità. I dati vengono elaborati e aggiornati in modo indipendente dal servizio.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

Puoi utilizzare la seguente query nel set di dati di esportazione dello snapshot del profilo per ottenere identità di esempio da grafici &quot;compressi&quot;.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>Le due query elencate sopra produrranno i risultati previsti se la sandbox non è abilitata per l’approccio provvisorio per dispositivo condiviso e si comporterà in modo diverso dalle regole di collegamento del grafico delle identità.
