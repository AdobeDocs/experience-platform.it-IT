---
description: Scopri come impostare un criterio di aggregazione per determinare come raggruppare e raggruppare in batch le richieste HTTP nella destinazione.
title: Criterio di aggregazione
exl-id: 2dfa8815-2d69-4a22-8938-8ea41be8b9c5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 2%

---

# Criterio di aggregazione

Per garantire la massima efficienza durante l’esportazione dei dati nell’endpoint API, puoi utilizzare varie impostazioni per aggregare i profili esportati in batch più o meno grandi, raggrupparli per identità e altri casi d’uso. Questo ti consente anche di adattare le esportazioni di dati a qualsiasi limite a valle dell’endpoint API (limitazione di frequenza, numero di identità per chiamata API, ecc.).

Utilizza l’aggregazione configurabile per approfondire le impostazioni fornite da Destination SDK oppure utilizza l’aggregazione della massima diligenza per dire a Destination SDK di raggruppare le chiamate API nel miglior modo possibile.

Quando crei una destinazione in tempo reale (streaming) con Destination SDK, puoi configurare il modo in cui i profili esportati devono essere combinati nelle esportazioni risultanti. Questo comportamento è determinato dalle impostazioni dei criteri di aggregazione.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

È possibile configurare le impostazioni dei criteri di aggregazione tramite l&#39;endpoint `/authoring/destinations`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

In questo articolo vengono descritte tutte le impostazioni dei criteri di aggregazione supportate che è possibile utilizzare per la destinazione.

Dopo aver letto questo documento, consulta la documentazione su [utilizzo dei modelli](../../functionality/destination-server/message-format.md#using-templating) e gli [esempi chiave di aggregazione](../../functionality/destination-server/message-format.md#template-aggregation-key) per scoprire come includere i criteri di aggregazione nel modello di trasformazione dei messaggi in base ai criteri di aggregazione selezionati.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | No |

## Aggregazione ottimale {#best-effort-aggregation}

L’aggregazione basata sullo sforzo migliore funziona meglio per le destinazioni che preferiscono meno profili per richiesta e che accettano più richieste con meno dati rispetto a meno richieste con più dati.

L’esempio di configurazione seguente mostra una configurazione dell’aggregazione ottimale. Per un esempio di aggregazione configurabile, vedere la sezione [aggregazione configurabile](#configurable-aggregation). I parametri applicabili all’aggregazione della migliore sforzo sono documentati nella tabella seguente.

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
| `aggregationType` | Stringa | Indica il tipo di criterio di aggregazione da utilizzare nella destinazione. Tipi di aggregazione supportati: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Intero | Experience Platform può aggregare più profili esportati in una singola chiamata HTTP. <br><br>Questo valore indica il numero massimo di profili che l&#39;endpoint deve ricevere in una singola chiamata HTTP. Tieni presente che si tratta di un’aggregazione ottimale. Ad esempio, se specifichi il valore 100, Experience Platform potrebbe inviare a una chiamata un numero qualsiasi di profili inferiore a 100. <br><br> Se il server non accetta più utenti per richiesta, impostare questo valore su `1`. |
| `bestEffortAggregation.splitUserById` | Booleano | Utilizza questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per uno spazio dei nomi identità specificato. |

{style="table-layout:auto"}

>[!TIP]
>
>Utilizza l’aggregazione della massima sforzo se l’endpoint API accetta meno di 100 profili per chiamata API.

## Aggregazione configurato {#configurable-aggregation}

L’aggregazione configurabile funziona meglio se si preferisce gestire batch di grandi dimensioni con migliaia di profili nella stessa chiamata. Questa opzione consente inoltre di aggregare i profili esportati in base a regole di aggregazione complesse.

L’esempio di configurazione seguente mostra una configurazione dell’aggregazione configurabile. Per un esempio dell&#39;aggregazione della migliore sforzo, vedere la sezione [aggregazione della migliore sforzo](#best-effort-aggregation). I parametri applicabili all’aggregazione configurabile sono indicati nella tabella seguente.

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
| `aggregationType` | Stringa | Indica il tipo di criterio di aggregazione da utilizzare nella destinazione. Tipi di aggregazione supportati: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booleano | Utilizza questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per uno spazio dei nomi identità specificato. |
| `configurableAggregation.maxBatchAgeInSecs` | Intero | Utilizzato in combinazione con `maxNumEventsInBatch`, questo parametro determina il tempo di attesa di Experience Platform per l&#39;invio di una chiamata API all&#39;endpoint. <ul><li>Valore minimo (secondi): 1.800</li><li>Valore massimo (secondi): 3.600</li></ul> Ad esempio, se utilizzi il valore massimo per entrambi i parametri, Experience Platform attenderà 3.600 secondi O fino a quando non saranno presenti 10000 profili qualificati prima di effettuare la chiamata API, a seconda di quale evento si verifica per primo. |
| `configurableAggregation.maxNumEventsInBatch` | Intero | Utilizzato insieme a `maxBatchAgeInSecs`, questo parametro determina il numero di profili qualificati da aggregare in una chiamata API. <ul><li>Valore minimo: 1.000</li><li>Valore massimo: 10.000</li></ul> Ad esempio, se utilizzi il valore massimo per entrambi i parametri, Experience Platform attenderà 3.600 secondi O fino a quando non saranno presenti 10.000 profili qualificati prima di effettuare la chiamata API, a seconda di quale evento si verifica per primo. |
| `configurableAggregation.aggregationKey` | - | Consente di aggregare i profili esportati mappati sulla destinazione in base ai parametri descritti di seguito. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Imposta questo parametro su `true` se vuoi raggruppare i profili esportati nella tua destinazione in base all&#39;ID pubblico. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Imposta questo parametro e `includeSegmentId` su `true` se vuoi raggruppare i profili esportati nella tua destinazione in base all&#39;ID pubblico e allo stato del pubblico. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booleano | Impostare questo parametro su `true` se si desidera raggruppare i profili esportati nella destinazione in base allo spazio dei nomi delle identità. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Imposta questo parametro su `true` se vuoi che i profili esportati siano aggregati in gruppi in base a una singola identità (GAID, IDFA, numeri di telefono, e-mail, ecc.). |
| `configurableAggregation.aggregationKey.groups` | Array | Crea elenchi di gruppi di identità per raggruppare i profili esportati nella destinazione in base a gruppi di spazi dei nomi di identità. Ad esempio, puoi combinare profili contenenti gli identificatori mobili IDFA e GAID in una chiamata alla destinazione e invia e-mail a un’altra utilizzando la configurazione mostrata nell’esempio precedente. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, sarai in grado di comprendere meglio come configurare i criteri di aggregazione per la tua destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione autenticazione cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
