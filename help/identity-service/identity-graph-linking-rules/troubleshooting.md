---
title: Guida alla risoluzione dei problemi per le regole di collegamento del grafico identità
description: Scopri come risolvere i problemi comuni nelle regole di collegamento del grafico delle identità.
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: b50633a8518f32051549158b23dfc503db255a82
workflow-type: tm+mt
source-wordcount: '3335'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi per le regole di collegamento del grafo identità

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo identità sono attualmente a disponibilità limitata. Contatta il team del tuo account Adobe per informazioni su come accedere alla funzione nelle sandbox di sviluppo.

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

1. Il nome del campo CRMID è contrassegnato come identità con lo spazio dei nomi CRMID.
2. Il CRMID dello spazio dei nomi è definito come uno spazio dei nomi univoco.

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

### Gli ExperienceEvents di post-autenticazione sono stati attribuiti al profilo autenticato errato

La priorità dello spazio dei nomi svolge un ruolo importante nel modo in cui i frammenti di evento determinano l’identità primaria.

* Dopo aver configurato e salvato le [impostazioni identità](./identity-settings-ui.md) per una data sandbox, il profilo utilizzerà [priorità spazio dei nomi](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) per determinare l&#39;identità primaria. Nel caso di identityMap, il profilo non utilizzerà più il flag `primary=true`.
* Anche se il profilo non farà più riferimento a questo flag, gli altri servizi in Experience Platform potrebbero continuare a utilizzare il flag `primary=true`.

Affinché [eventi utente autenticati](implementation-guide.md#ingest-your-data) siano associati allo spazio dei nomi della persona, tutti gli eventi autenticati devono contenere lo spazio dei nomi della persona (CRMID). Ciò significa che anche dopo che un utente effettua l’accesso, lo spazio dei nomi della persona deve essere ancora presente in ogni evento autenticato.

Puoi continuare a visualizzare il flag &#39;eventi&#39; di `primary=true` durante la ricerca di un profilo nel visualizzatore di profili. Tuttavia, questo viene ignorato e non verrà utilizzato dal profilo.

AAID sono bloccati per impostazione predefinita. Pertanto, se utilizzi il [connettore di origine Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md), assicurati che l&#39;ECID abbia una priorità più alta rispetto all&#39;ECID in modo che gli eventi non autenticati abbiano un&#39;identità primaria di ECID.

**Risoluzione dei problemi**

1. Per verificare che gli eventi autenticati contengano sia lo spazio dei nomi della persona che quello dei cookie, leggere i passaggi descritti nella sezione relativa alla risoluzione di [errori relativi ai dati non acquisiti in Identity Service](#my-identities-are-not-getting-ingested-into-identity-service).
2. Per verificare che gli eventi autenticati abbiano l’identità primaria dello spazio dei nomi della persona (ad esempio, CRMID), cerca lo spazio dei nomi della persona nel visualizzatore profili senza unire i criteri di unione (questo è il criterio di unione che non utilizza un grafico privato). Questa ricerca restituirà solo gli eventi associati allo spazio dei nomi della persona.

### I miei frammenti di evento esperienza non vengono acquisiti nel profilo {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Esistono diversi motivi che contribuiscono al motivo per cui i frammenti di evento esperienza non vengono acquisiti in Profilo, tra cui:

* [Set di dati non abilitato per il profilo](../../catalog/datasets/enable-for-profile.md).
* [Errore di convalida nel profilo](../../xdm/classes/experienceevent.md).
   * Ad esempio, un evento esperienza deve contenere sia `_id` che `timestamp`.
   * Inoltre, `_id` deve essere univoco per ogni evento (record).
* Lo spazio dei nomi con la priorità più alta è una stringa vuota.

Nel contesto della priorità dello spazio dei nomi, il profilo rifiuterà:

* Qualsiasi evento che contiene due o più identità con la priorità più elevata dello spazio dei nomi. Ad esempio, se GAID non è contrassegnato come spazio dei nomi univoco e sono presenti due identità con uno spazio dei nomi GAID e valori di identità diversi, l’evento non verrà memorizzato in Profilo.
* Qualsiasi evento in cui lo spazio dei nomi con la priorità più elevata è una stringa vuota.

**Risoluzione dei problemi**

Se i dati vengono inviati al data lake, ma non al profilo, e ritieni che ciò sia dovuto all’invio di due o più identità con la priorità più elevata dello spazio dei nomi in un singolo evento, puoi eseguire la seguente query per verificare che siano presenti due valori di identità diversi inviati sullo stesso spazio dei nomi:

>[!TIP]
>
>Nelle seguenti query è necessario:
>
>* Sostituire `_testimsorg.identification.core.email` con il percorso che invia l&#39;identità.
>* Sostituisci `Email` con lo spazio dei nomi con la priorità più alta. Questo è lo stesso spazio dei nomi che non viene acquisito.
>* Sostituire `dataset_name` con il set di dati da ricercare.

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

Puoi anche eseguire la seguente query per verificare se l’acquisizione nel profilo non avviene a causa di uno spazio dei nomi più alto con una stringa vuota:

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE (col.id = '' or _testimsorg.identification.core.email = '') and key = 'Email' 
```

Queste due query presuppongono che:

* Un’identità viene inviata da identityMap e un’altra identità da un descrittore di identità. **NOTA**: negli schemi Experience Data Model (XDM), il descrittore di identità è il campo contrassegnato come identità.
* Il CRMID viene inviato tramite identityMap. Se il CRMID viene inviato come campo, rimuovere `key='Email'` dalla clausola WHERE.

## Problemi relativi al comportamento del grafico {#graph-behavior-related-issues}

Questa sezione illustra i problemi comuni che potresti incontrare sul funzionamento del grafo delle identità.

### ExperienceEvents non autenticati vengono collegati al profilo autenticato errato

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

1. Il simbolo di identità (namespaceCode) dello spazio dei nomi del cookie (ad esempio ECID) e dello spazio dei nomi della persona (ad esempio CRMID) che sono stati inviati.
1.1. Per le implementazioni dell’SDK per web, in genere si tratta degli spazi dei nomi inclusi in identityMap.
1.2. Per le implementazioni del connettore di origine di Analytics, si tratta dell’identificatore del cookie incluso in identityMap. L’identificatore della persona è un campo eVar contrassegnato come identità.
2. Set di dati in cui è stato inviato l’evento (dataset_name).
3. Il valore di identità dello spazio dei nomi del cookie da cercare (identity_value).

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

Ora che hai identificato i valori dei cookie collegati a più ID persona, estrane uno dai risultati e utilizzalo nella seguente query per ottenere una visualizzazione cronologica di quando il valore del cookie è stato collegato a un identificatore persona diverso:

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
* È inoltre possibile leggere la [guida all&#39;implementazione](./implementation-guide.md#appendix) per esempi di strutture di grafico non supportate. Esistono due scenari possibili:
   * Non esiste un singolo spazio dei nomi in tutti i profili.
   * Si verifica uno scenario [&quot;ID pendente&quot;](./implementation-guide.md#dangling-loginid-scenario). In questo scenario, il servizio Identity non è in grado di determinare se l’ID penzolante è associato a una qualsiasi delle entità persona nei grafici.

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

## Domande frequenti {#faq}

Questa sezione illustra un elenco di risposte alle domande più frequenti sulle regole di collegamento del grafico delle identità.

## Algoritmo di ottimizzazione identità {#identity-optimization-algorithm}

Leggi questa sezione per le risposte alle domande frequenti sull&#39;[algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md).

### Ho un CRMID per ciascuna delle mie unità aziendali (CRMID B2C, CRMID B2B), ma non ho uno spazio dei nomi univoco tra tutti i miei profili. Cosa succede se contrassegno B2C CRMID e B2B CRMID come univoci e abilito le impostazioni di identità?

Questo scenario non è supportato. Pertanto, è possibile che i grafici si riducano nei casi in cui un utente utilizza il proprio CRMID B2C per accedere e un altro utente utilizza il proprio CRMID B2B per accedere. Per ulteriori informazioni, consulta la sezione sul [requisito dello spazio dei nomi per singola persona](./implementation-guide.md#single-person-namespace-requirement) nella pagina di implementazione.

### L’algoritmo di ottimizzazione delle identità corregge i grafici compressi esistenti?

I grafici compressi esistenti saranno interessati dall’algoritmo del grafico (&quot;fissi&quot;) solo se vengono aggiornati dopo il salvataggio delle nuove impostazioni.

### Se due persone effettuano l&#39;accesso e la disconnessione utilizzando lo stesso dispositivo, cosa succede agli eventi? Tutti gli eventi verranno trasferiti all’ultimo utente autenticato?

* Gli eventi anonimi (eventi con ECID come identità primaria in Real-Time Customer Profile) verranno trasferiti all’ultimo utente autenticato. Questo perché l’ECID sarà collegato al CRMID dell’ultimo utente autenticato (su Identity Service).
* Tutti gli eventi autenticati (eventi con CRMID definito come identità primaria) rimarranno con la persona.

Per ulteriori informazioni, leggere la guida in [determinazione dell&#39;identità primaria per gli eventi esperienza](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events).

### Che impatto avrà sui percorsi in Adobe Journey Optimizer il trasferimento dell’ECID da una persona a un’altra?

Il CRMID dell’ultimo utente autenticato verrà collegato all’ECID (dispositivo condiviso). Gli ECID possono essere riassegnati da una persona all’altra in base al comportamento dell’utente. L’impatto dipenderà da come verrà costruito il percorso, pertanto è importante che i clienti testino il percorso in un ambiente sandbox di sviluppo per convalidarne il comportamento.

I punti chiave da evidenziare sono i seguenti:

* Una volta che un profilo entra in un percorso, la riassegnazione di ECID non fa sì che il profilo esca dal percorso.
   * Le uscite dal percorso non vengono attivate dalle modifiche apportate al grafico.
* Se un profilo non è più associato a un ECID, ciò può comportare la modifica del percorso di percorso in presenza di una condizione che utilizza la qualificazione del pubblico.
   * La rimozione di ECID può modificare gli eventi associati a un profilo, il che potrebbe comportare modifiche nella qualifica del pubblico.
* Il reinserimento di un percorso dipende dalle proprietà del percorso.
   * Se disattivi il reinserimento di un percorso, quando un profilo esce da quel percorso, lo stesso profilo non viene reinserito per 91 giorni (in base al timeout globale del percorso).
* Se un percorso inizia con uno spazio dei nomi ECID, il profilo che entra e il profilo che riceve l’azione (ad es. e-mail, offerta) può variare a seconda di come è progettato il percorso.
   * Ad esempio, se esiste una condizione di attesa tra le azioni e i trasferimenti ECID durante il periodo di attesa, è possibile eseguire il targeting di un profilo diverso.
   * Con questa funzione, gli ECID non sono più sempre associati a un profilo.
   * Si consiglia di iniziare i percorsi con gli spazi dei nomi delle persone (CRMID).

>[!TIP]
>
>I percorsi devono cercare un profilo con spazi dei nomi univoci perché uno spazio dei nomi non univoco può essere riassegnato a un altro utente.
>
>* Gli ECID e gli spazi dei nomi e-mail/telefono non univoci potevano essere spostati da una persona all’altra.
>* Se un percorso presenta una condizione di attesa e questi spazi dei nomi non univoci vengono utilizzati per ricercare un profilo in un percorso, il messaggio di percorso può essere inviato alla persona errata.

## Priorità dello spazio dei nomi

Leggi questa sezione per le risposte alle domande frequenti sulla [priorità dello spazio dei nomi](./namespace-priority.md).

### Ho abilitato le impostazioni di identità. Cosa succede alle mie impostazioni se voglio aggiungere uno spazio dei nomi personalizzato dopo che le impostazioni sono state abilitate?

Esistono due &quot;bucket&quot; di spazi dei nomi: spazi dei nomi delle persone e spazi dei nomi dispositivo/cookie. Il nuovo spazio dei nomi personalizzato creato avrà la priorità più bassa in ogni &quot;bucket&quot;, in modo che questo nuovo spazio dei nomi personalizzato non influisca sull’acquisizione dei dati esistenti.

### Se Real-Time Customer Profile non utilizza più il flag &quot;primary&quot; in identityMap, è ancora necessario inviare questo valore?

Sì, il flag &quot;primary&quot; su identityMap viene utilizzato da altri servizi. Per ulteriori informazioni, leggere la guida sulle [implicazioni della priorità dello spazio dei nomi su altri servizi Experience Platform](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services).

### La priorità dello spazio dei nomi si applica ai set di dati dei record Profilo in Real-Time Customer Profile?

No. La priorità dello spazio dei nomi si applica solo ai set di dati Experience Event che utilizzano la classe XDM ExperienceEvent.

### Come funziona questa funzione insieme ai guardrail del grafo delle identità di 50 identità per grafo? La priorità dello spazio dei nomi influisce su questo guardrail definito dal sistema?

L’algoritmo di ottimizzazione dell’identità verrà applicato per primo per garantire la rappresentazione dell’entità della persona. In seguito, se il grafo tenta di superare il [guardrail del grafo delle identità](../guardrails.md) (50 identità per grafo), verrà applicata questa logica. La priorità dello spazio dei nomi non influisce sulla logica di eliminazione del guardrail identità/grafico 50.

## Test

Leggi questa sezione per le risposte alle domande frequenti sulle funzionalità di test e debug nelle regole di collegamento del grafico delle identità.

### Quali sono alcuni degli scenari che dovrei testare in un ambiente sandbox di sviluppo?

In generale, il test su una sandbox di sviluppo dovrebbe simulare i casi d’uso che intendi eseguire sulla sandbox di produzione. Per alcune aree chiave da convalidare durante l’esecuzione di test completi, consulta la tabella seguente:

| Test case | Passaggi del test | Risultato previsto |
| --- | --- | --- |
| Rappresentazione accurata dell’entità della persona | <ul><li>Simulazione di navigazione anonima</li><li>Imita l’accesso di due persone (John, Jane) utilizzando lo stesso dispositivo</li></ul> | <ul><li>Sia John che Jane devono essere associati ai loro attributi e agli eventi autenticati.</li><li>L’ultimo utente autenticato deve essere associato agli eventi di navigazione anonimi.</li></ul> |
| Segmentazione | Creare quattro definizioni di segmenti (**NOTA**: ogni coppia di definizioni di segmenti deve avere una valutata utilizzando il batch e l&#39;altra lo streaming.) <ul><li>Definizione del segmento A: qualificazione del segmento basata sugli eventi e/o attributi autenticati di John.</li><li>Definizione del segmento B: qualificazione del segmento basata sugli eventi e/o attributi autenticati di Jane.</li></ul> | Indipendentemente dagli scenari di dispositivi condivisi, John e Jane dovrebbero sempre qualificarsi per i rispettivi segmenti. |
| Qualificazione del pubblico / percorsi unitari su Adobe Journey Optimizer | <ul><li>Crea un percorso che inizia con un’attività di qualificazione del pubblico (ad esempio la segmentazione in streaming creata in precedenza).</li><li>Crea un percorso che inizia con un evento unitario. Questo evento unitario deve essere un evento autenticato.</li><li>È necessario disattivare il reinserimento durante la creazione di questi percorsi.</li></ul> | <ul><li>Indipendentemente dagli scenari di dispositivi condivisi, John e Jane dovrebbero attivare i rispettivi percorsi in cui dovrebbero entrare.</li><li>John e Jane non devono rientrare nel percorso quando l’ECID viene trasferito nuovamente loro.</li></ul> |

{style="table-layout:auto"}

### Come posso verificare che questa funzione funzioni come previsto?

Utilizza lo strumento di simulazione del grafico [](./graph-simulation.md) per verificare che la funzione funzioni a un singolo livello di grafico.

Per convalidare la funzionalità a livello di sandbox, fai riferimento alla sezione [!UICONTROL Conteggio dei grafici con più spazi dei nomi] nel dashboard delle identità.