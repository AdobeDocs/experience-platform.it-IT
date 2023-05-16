---
description: Scopri come impostare un criterio di aggregazione per determinare in che modo raggruppare e gestire le richieste HTTP nella destinazione.
title: Criteri di aggregazione
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# Criteri di aggregazione

Per garantire la massima efficienza durante l’esportazione dei dati nell’endpoint API, puoi utilizzare varie impostazioni per aggregare i profili esportati in batch più grandi o più piccoli, raggrupparli per identità e altri casi d’uso. Ciò ti consente anche di adattare le esportazioni di dati a qualsiasi limitazione a valle dell’endpoint API (limitazione della velocità, numero di identità per chiamata API, ecc.).

Utilizza l’aggregazione configurabile per immergerti nelle impostazioni fornite da Destination SDK o utilizza l’aggregazione del massimo sforzo per dire a Destination SDK di eseguire al meglio il batch delle chiamate API.

Quando crei una destinazione in tempo reale (streaming) con Destination SDK, puoi configurare in che modo i profili esportati devono essere combinati nelle esportazioni risultanti. Questo comportamento è determinato dalle impostazioni del criterio di aggregazione.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta la guida su come [utilizza Destination SDK per configurare una destinazione streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puoi configurare le impostazioni dei criteri di aggregazione tramite `/authoring/destinations` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le impostazioni dei criteri di aggregazione supportate che puoi utilizzare per la destinazione.

Dopo aver letto questo documento, consulta la documentazione su [utilizzo di modelli](../../functionality/destination-server/message-format.md#using-templating) e [esempi chiave di aggregazione](../../functionality/destination-server/message-format.md#template-aggregation-key) per comprendere come includere il criterio di aggregazione nel modello di trasformazione del messaggio in base al criterio di aggregazione selezionato.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | No |

## Aggregazione degli sforzi migliori {#best-effort-aggregation}

L’aggregazione più efficiente funziona meglio per le destinazioni che preferiscono un minor numero di profili per richiesta e preferiscono più richieste con meno dati rispetto a meno richieste con più dati.

La configurazione di esempio riportata di seguito mostra una configurazione di aggregazione più efficiente. Per un esempio di aggregazione configurabile, consulta la sezione [aggregazione configurabile](#configurable-aggregation) sezione . I parametri applicabili all’aggregazione dello sforzo migliore sono indicati nella tabella seguente.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `aggregationType` | Stringa | Indica il tipo di criterio di aggregazione che la destinazione deve utilizzare. Tipi di aggregazione supportati: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Intero | Experience Platform può aggregare più profili esportati in una singola chiamata HTTP. <br><br>Questo valore indica il numero massimo di profili che l’endpoint deve ricevere in una singola chiamata HTTP. Tieni presente che si tratta di un’aggregazione dello sforzo migliore. Ad esempio, se specifichi il valore 100, Platform potrebbe inviare un numero qualsiasi di profili inferiore a 100 in una chiamata . <br><br> Se il server non accetta più utenti per richiesta, imposta questo valore su `1`. |
| `bestEffortAggregation.splitUserById` | Booleano | Usa questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per uno spazio dei nomi di identità specificato. |

{style="table-layout:auto"}

>[!TIP]
>
>Utilizza l’aggregazione del tuo impegno migliore se l’endpoint API accetta meno di 100 profili per chiamata API.

## Aggregazione configurabile {#configurable-aggregation}

L’aggregazione configurabile funziona meglio se preferisci effettuare batch di grandi dimensioni con migliaia di profili sulla stessa chiamata. Questa opzione ti consente inoltre di aggregare i profili esportati in base a regole di aggregazione complesse.

L’esempio di configurazione seguente mostra una configurazione di aggregazione configurabile. Per un esempio di aggregazione dello sforzo ottimale, consulta la sezione [aggregazione dello sforzo migliore](#best-effort-aggregation) sezione . I parametri applicabili all’aggregazione configurabile sono indicati nella tabella seguente.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `aggregationType` | Stringa | Indica il tipo di criterio di aggregazione che la destinazione deve utilizzare. Tipi di aggregazione supportati: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booleano | Usa questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per uno spazio dei nomi di identità specificato. |
| `configurableAggregation.maxBatchAgeInSecs` | Intero | Utilizzato in combinazione con `maxNumEventsInBatch`, questo parametro determina per quanto tempo Experience Platform deve aspettare fino all’invio di una chiamata API all’endpoint. <ul><li>Valore minimo (secondi): 1800</li><li>Valore massimo (secondi): 3600</li></ul> Ad esempio, se utilizzi il valore massimo per entrambi i parametri, Experience Platform attenderà 3600 secondi OR fino a quando non saranno presenti 10000 profili qualificati prima di effettuare la chiamata API, a seconda di quale si verifica per primo. |
| `configurableAggregation.maxNumEventsInBatch` | Intero | Utilizzato in combinazione con `maxBatchAgeInSecs`, questo parametro determina quanti profili qualificati devono essere aggregati in una chiamata API. <ul><li>Valore minimo: 1000</li><li>Valore massimo: 10000</li></ul> Ad esempio, se utilizzi il valore massimo per entrambi i parametri, Experience Platform attenderà 3600 secondi OR fino a quando non saranno presenti 10000 profili qualificati prima di effettuare la chiamata API, a seconda di quale si verifica per primo. |
| `configurableAggregation.aggregationKey` | - | Consente di aggregare i profili esportati mappati sulla destinazione in base ai parametri descritti di seguito. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Imposta questo parametro su `true` se desideri raggruppare i profili esportati nella destinazione per ID segmento. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Imposta sia questo parametro sia `includeSegmentId` a `true`, se desideri raggruppare i profili esportati nella destinazione per ID segmento e stato del segmento. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booleano | Imposta questo parametro su `true` per raggruppare i profili esportati nella destinazione in base allo spazio dei nomi identità. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Imposta questo parametro su `true` se desideri che i profili esportati siano aggregati in gruppi in base a una singola identità (GAID, IDFA, numeri di telefono, e-mail, ecc.). |
| `configurableAggregation.aggregationKey.groups` | Array | Crea elenchi di gruppi di identità se desideri raggruppare i profili esportati nella destinazione per gruppi di namespace di identità. Ad esempio, puoi combinare profili che contengono gli identificatori mobili IDFA e GAID in una chiamata alla tua destinazione ed e-mail in un&#39;altra utilizzando la configurazione mostrata nell&#39;esempio precedente. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di come configurare i criteri di aggregazione per la tua destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione dell’autenticazione cliente](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)