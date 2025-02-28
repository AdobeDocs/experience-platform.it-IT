---
title: Gestire la conservazione dei set di dati di Experience Event nel Data Lake tramite TTL
description: Scopri come valutare, impostare e gestire la conservazione dei set di dati di Experience Event nel data lake utilizzando le configurazioni Time-To-Live (TTL) con le API di Adobe Experience Platform. Questa guida spiega come la scadenza a livello di riga TTL supporti le regole di conservazione dei dati, ottimizzi l'efficienza dello storage e garantisca un'efficace gestione del ciclo di vita dei dati. Inoltre, fornisce casi d’uso e best practice per aiutarti ad applicare il TTL in modo efficace.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: affaeb0869423292a44eb7ada8343482bb163ca6
workflow-type: tm+mt
source-wordcount: '2196'
ht-degree: 1%

---

# Gestire la conservazione dei set di dati di Experience Event nel data lake utilizzando TTL

Una gestione efficiente dei dati è fondamentale per garantire prestazioni ottimali, controllo dei costi e integrità dei dati. Utilizza il TTL (Experience Event Dataset Retention Time-To-Live) per applicare la scadenza a livello di riga, rimuovendo automaticamente i record obsoleti dai set di dati nel data lake e garantendo al contempo un’efficienza di archiviazione e una rilevanza dei dati ottimali.

Questa guida spiega come valutare, impostare e gestire il TTL utilizzando l’API Catalog Service. Scoprirai quando e perché applicare il TTL, come configurare e aggiornare i valori TTL utilizzando le chiamate API e le best practice per garantire un’implementazione efficace.

>[!IMPORTANT]
>
> TTL è progettato per ottimizzare la gestione del ciclo di vita dei dati e l&#39;efficienza dello storage. Non è uno strumento di conformità e non dovrebbe essere utilizzato per i requisiti normativi. La conformità richiede spesso strategie di governance dei dati più ampie.

## Perché utilizzare TTL per la gestione dei dati a livello di riga

Con la crescita dei dataset, la gestione efficiente dei dati diventa sempre più importante per preservare le prestazioni, controllare i costi e mantenere i dati pertinenti. La scadenza dei dati a livello di riga basata su TTL automatizza la pulizia dei dati rimuovendo i record obsoleti senza interventi manuali per ottimizzare lo storage e migliorare l&#39;efficienza del sistema.

Il TTL è utile per gestire dati sensibili al tempo che perdono rilevanza nel tempo. Prendi in considerazione l’implementazione del TTL se devi:

- Riduzione dei costi di storage attraverso la rimozione automatica dei record obsoleti.
- Migliora le prestazioni delle query riducendo al minimo i dati irrilevanti.
- Mantenere l’igiene dei dati conservando solo le informazioni pertinenti.
- Ottimizzazione della conservazione dei dati per supportare gli obiettivi aziendali.

>[!NOTE]
>
>La conservazione dei set di dati di Experience Event si applica ai dati evento memorizzati nel data lake. Se gestisci la conservazione in Real-Time Customer Data Platform, puoi utilizzare [Scadenza evento esperienza](../../profile/event-expirations.md) e [Scadenza profilo pseudonimo](../../profile/pseudonymous-profiles.md) insieme alle impostazioni di conservazione del data lake.
>
>Le configurazioni TTL consentono di ottimizzare lo storage in base ai diritti. Anche se i dati dell’archivio profili (utilizzati in Real-Time CDP) possono essere considerati obsoleti e rimossi dopo 30 giorni, gli stessi dati evento nel data lake possono rimanere disponibili per 12-13 mesi (o più in base all’adesione) per i casi di utilizzo di Analytics e Data Distiller.

### Esempio di settore {#industry-example}

Ad esempio, considera un servizio di streaming video che tiene traccia delle interazioni degli utenti, come visualizzazioni video, ricerche e consigli. Anche se i dati di coinvolgimento recenti sono fondamentali per la personalizzazione, i registri di attività più datati (ad esempio, le interazioni di più di un anno fa) perdono rilevanza. Utilizzando la scadenza a livello di riga, Platform rimuove automaticamente i registri obsoleti, garantendo che solo i dati correnti e significativi vengano utilizzati per le analisi e i consigli.

## Valuta idoneità TTL

Prima di applicare un criterio di conservazione, valuta se il set di dati è un buon candidato per la scadenza a livello di riga. Considera quanto segue:

- Rilevanza dei dati nel tempo: i dati meno recenti forniscono valore o diventano obsoleti?
- Impatto sui processi a valle: la rimozione dei dati influisce su reporting, analisi o integrazioni?
- Costo dello storage rispetto al valore di conservazione: il valore dei dati meno recenti giustifica il costo dello storage?

Se i record storici sono essenziali per l’analisi a lungo termine o le operazioni aziendali, il TTL potrebbe non essere l’approccio corretto. L’analisi di questi fattori garantisce l’allineamento del TTL alle esigenze di conservazione dei dati senza influire negativamente sulla disponibilità dei dati.

## Pianificare le query

Prima di applicare il TTL, utilizza le query per analizzare le dimensioni e la rilevanza del set di dati. L’esecuzione di query mirate consente di determinare la quantità di dati da mantenere o rimuovere in diverse configurazioni TTL.

Ad esempio, la query SQL seguente conta il numero di record creati negli ultimi 30 giorni:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

L’esecuzione di query simili per intervalli di tempo diversi consente di convalidare le impostazioni TTL e di garantire il bilanciamento tra l’efficienza dello storage e l’accessibilità dei dati.

## Introduzione alla gestione TTL

Prima di poter valutare, impostare e gestire la conservazione dei set di dati di Experience Event utilizzando l’API Catalog Service, è necessario comprendere come formattare correttamente le richieste. Ciò include la conoscenza dei percorsi API, la fornitura delle intestazioni richieste e la formattazione dei payload di richiesta. Per informazioni essenziali, fare riferimento alla [guida introduttiva all&#39;API Catalog Service](../api/getting-started.md).

>[!NOTE]
>
>Questo documento descrive la scadenza a livello di riga, che elimina singole righe scadute all’interno di un set di dati mantenendo intatto il set di dati stesso. Non si applica alla scadenza del set di dati, che rimuove interi set di dati ed è gestito da una funzione separata. Per informazioni sulla scadenza a livello di set di dati, consulta la [documentazione API relativa alla scadenza del set di dati](../../hygiene/api/dataset-expiration.md).

### Controllare le impostazioni TTL correnti

Per iniziare la gestione TTL, controlla innanzitutto le impostazioni TTL correnti. Effettuare una richiesta GET all&#39;endpoint `/ttl/{datasetId}` per recuperare le impostazioni TTL predefinite, massime e minime per un set di dati. Questo passaggio è necessario perché le regole TTL possono variare in base al tipo di set di dati.

>[!TIP]
>
>L&#39;URL di Platform Gateway e il percorso di base per l&#39;API del servizio catalogo sono: `https://platform.adobe.io/data/foundation/catalog`.

**Formato API**

```http
GET /ttl/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Stringa generata dal sistema che identifica in modo univoco un set di dati. Per trovare un ID di set di dati, utilizza l&#39;endpoint `/datasets`. Per istruzioni su come filtrare le risposte per i set di dati rilevanti, consulta la [guida API per oggetti catalogo ](../api/list-objects.md). |

**Richiesta**

La richiesta seguente recupera le impostazioni TTL dell’organizzazione per un particolare set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la configurazione TTL per il set di dati, inclusi i valori TTL predefiniti, massimi e minimi per l’archiviazione `adobe_lakeHouse` e `adobe_unifiedProfile`.

+++Seleziona per visualizzare la risposta

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P30D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Proprietà | Descrizione |
|--------------|-------------|
| `defaultValue` | Periodo TTL predefinito applicato se non è impostato alcun TTL personalizzato. |
| `maxValue` | Il TTL più lungo consentito per il set di dati. Se null, non esiste alcun limite massimo. |
| `minValue` | Il TTL più breve consentito per garantire la conformità con i criteri di sistema. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Impostare il TTL per un set di dati {#set-ttl}

>[!IMPORTANT]
>
>La scadenza delle righe può essere applicata solo ai set di dati evento che utilizzano uno schema di serie temporali. Prima di impostare il TTL, verifica che lo schema del set di dati estenda `https://ns.adobe.com/xdm/data/time-series` per verificare che la richiesta API abbia esito positivo. Utilizzare l&#39;API Schema Registry per recuperare i dettagli dello schema e verificare la proprietà `meta:extends`. Per informazioni su come eseguire questa operazione, consulta la [documentazione dell&#39;endpoint schema](../../xdm/api/schemas.md#lookup).

Per configurare Conservazione set di dati di Experience Event per il set di dati, imposta un nuovo valore TTL effettuando una richiesta PATCH all&#39;endpoint `/v2/datasets/{ID}`.

**Formato API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati per cui desideri aggiornare il valore TTL. |

**Richiesta**

Nell&#39;esempio di richiesta seguente, `ttlValue` è impostato su `P3M`. In questo modo i record più vecchi di tre mesi verranno eliminati automaticamente. È possibile modificare il periodo di conservazione in base alle esigenze aziendali utilizzando valori quali `P6M` per sei mesi o `P12M` per un anno.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

**Risposta**

In caso di esito positivo, la risposta mostra la configurazione TTL per il set di dati. Include dettagli sulle impostazioni di scadenza a livello di riga per l&#39;archiviazione `adobe_lakeHouse` e `adobe_unifiedProfile`.

+++Seleziona per visualizzare la risposta

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Proprietà | Descrizione |
|----------------------------------|-------------|
| `extensions` | Contenitore per metadati aggiuntivi correlati al set di dati. |
| `extensions.adobe_lakeHouse` | Specifica le impostazioni relative all&#39;architettura di archiviazione, incluse le configurazioni di scadenza a livello di riga |
| `rowExpiration` | L’oggetto contiene impostazioni TTL che definiscono il periodo di conservazione per il set di dati. |
| `rowExpiration.ttlValue` | Definisce la durata prima della rimozione automatica dei record nel set di dati. Utilizza il formato del periodo ISO-8601 (ad esempio, `P3M` per 3 mesi o `P30D` per una settimana). |
| `rowExpiration.valueStatus` | La stringa indica se l’impostazione TTL è un valore di sistema predefinito o un valore personalizzato impostato da un utente. I valori possibili sono: `default`, `custom`. |
| `rowExpiration.setBy` | Specifica chi ha modificato per ultimo l’impostazione TTL. I valori possibili includono: `user` (impostato manualmente) o `service` (assegnato automaticamente). |
| `rowExpiration.updated` | Il timestamp dell’ultimo aggiornamento TTL. Questo valore indica quando è stata apportata l’ultima modifica all’impostazione TTL. |

### Come aggiornare il TTL {#update-ttl}

Estendere o abbreviare il periodo di conservazione in base alle esigenze aziendali modificando il valore TTL. Ad esempio, se consideri la piattaforma di streaming video di cui sopra, la piattaforma può inizialmente impostare il TTL a tre mesi per garantire nuovi dati di coinvolgimento per la personalizzazione. Tuttavia, se la loro analisi mostra che i modelli di interazione più vecchi di tre mesi forniscono ancora informazioni utili, possono estendere il periodo TTL a sei mesi per conservare i record più vecchi per modelli di consigli migliori.

Per modificare un valore TTL esistente, utilizzare il metodo `PATCH` sull&#39;endpoint `/v2/datasets/{DATASET_ID}`.

#### Formato API

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Richiesta**

Nella richiesta seguente, il TTL viene aggiornato a sei mesi (`P6M`) estendendo il periodo di conservazione dei record prima dell&#39;eliminazione automatica.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Risposta**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Best practice per l’impostazione del valore TTL {#best-practices}

La scelta del valore TTL corretto è fondamentale per garantire che i criteri di conservazione dei set di dati di Experience Event bilancino la conservazione dei dati, l’efficienza dello storage e le esigenze di analisi. Un valore TTL troppo breve può causare la perdita di dati, mentre un valore troppo lungo può aumentare i costi di storage e l&#39;accumulo di dati non necessari. Assicurati che il TTL sia allineato allo scopo del set di dati tenendo in considerazione la frequenza con cui viene effettuato l’accesso ai dati e il tempo in cui rimangono rilevanti.

La tabella seguente fornisce consigli comuni su TTL in base al tipo di set di dati e ai pattern di utilizzo:

| Tipo di set di dati | TTL consigliato | Casi d’uso tipici |
|-----------------------------|------------------------|-------------------|
| Set di dati ad accesso frequente | 30-90 giorni | Registri di coinvolgimento degli utenti, dati di clickstream sul sito web, dati sulle prestazioni delle campagne a breve termine. |
| Set di dati di archiviazione | 1 anno o più | Registri delle transazioni finanziarie, dati sulla conformità, analisi delle tendenze a lungo termine, set di dati di formazione per l’apprendimento automatico. |
| Set di dati gestiti dall’app | Fino a 13 mesi | I set di dati gestiti dal sistema hanno restrizioni TTL predefinite, che vengono applicate automaticamente per rispettare i limiti imposti dal sistema. |
| Set di dati gestiti dal cliente | 30 giorni - TTL massimo | Set di dati creati tramite l’interfaccia utente, le API o Data Distiller. Il TTL deve essere di almeno 30 giorni ed entro il TTL massimo definito. |

Rivedere periodicamente le impostazioni TTL per assicurarsi che continuino ad essere allineate alle regole di storage, alle esigenze analitiche e ai requisiti aziendali.

### Considerazioni chiave durante l’impostazione del valore TTL

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Segui queste best practice per garantire che le impostazioni TTL siano allineate alla strategia di conservazione dei dati:

- Controlla regolarmente le modifiche TTL. Ogni aggiornamento TTL attiva un evento di audit. Utilizza i registri di audit per tenere traccia delle modifiche TTL a scopo di conformità, governance dei dati e risoluzione dei problemi.
- Rimuovi TTL se i dati devono essere conservati per un tempo indefinito. Per disabilitare il TTL, impostare `ttlValue` su `null`. Ciò impedisce la scadenza automatica e mantiene tutti i record in modo permanente. Prima di apportare questa modifica, è necessario considerare le implicazioni relative allo storage.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Limitazioni del TTL {#limitations}

Tieni presente le seguenti limitazioni quando utilizzi TTL:

- **La conservazione del set di dati Experience Event tramite TTL si applica alla scadenza a livello di riga**, non all&#39;eliminazione del set di dati. TTL rimuove i record in base a un periodo di conservazione definito, ma non elimina interi set di dati. Per rimuovere un set di dati, utilizzare l&#39;endpoint di scadenza [del set di dati](../../hygiene/api/dataset-expiration.md) o l&#39;eliminazione manuale.
- Impossibile rimuovere **TTL**. Solo aggiornato. Una volta applicato, il TTL non può essere eliminato, ma puoi [modificare il periodo di conservazione](#update-ttl) per estenderlo o ridurlo. Per conservare i dati a tempo indefinito, impostare un TTL sufficientemente lungo anziché tentare di rimuoverlo.
- **TTL non è uno strumento di conformità**. TTL ottimizza lo storage e la gestione del ciclo di vita dei dati, ma non soddisfa i requisiti normativi di conservazione dei dati. Per la conformità, implementa strategie di governance dei dati più ampie.

## Domande frequenti sui criteri di conservazione dei set di dati {#faqs}

Questa sezione fornisce le risposte alle domande più frequenti sui criteri di conservazione dei set di dati in Adobe Experience Platform.

### A quali tipi di set di dati è possibile applicare le regole dei criteri di conservazione?

+++Risposta
Puoi applicare i criteri di conservazione ai set di dati creati utilizzando la classe XDM ExperienceEvent. Per i servizi di profilo, i criteri di conservazione sono applicabili solo ai set di dati Experience Event che sono stati abilitati per il profilo.
+++

### Quando il processo di conservazione del set di dati eliminerà i dati dai servizi del data lake?

+++Risposta
I TTL dei set di dati vengono valutati ed elaborati settimanalmente, eliminando tutti i record scaduti. Un evento è considerato scaduto se è stato acquisito in Platform più di 30 giorni fa (data di acquisizione > 30 giorni) e la sua data evento supera il periodo di conservazione definito (TTL).
+++

### Quando il processo di conservazione del set di dati eliminerà i dati dai servizi profilo?

+++Risposta
Una volta impostati i criteri di conservazione, gli eventi esistenti in Platform vengono immediatamente eliminati se il relativo timestamp dell’evento supera il periodo di conservazione (TTL). I nuovi eventi vengono eliminati dopo che il loro timestamp supera il periodo di conservazione.

Ad esempio, se applichi un criterio di scadenza di 30 giorni il 15 maggio, si verifica quanto segue:

- I nuovi eventi ricevono una scadenza di 30 giorni al momento dell’acquisizione.
- Gli eventi esistenti con una marca temporale precedente al 15 aprile vengono eliminati immediatamente.
- Gli eventi esistenti con una marca temporale successiva al 15 aprile scadono 30 giorni dopo la loro marca temporale (ad esempio, un evento del 18 aprile verrebbe eliminato il 18 maggio).
+++

### È possibile impostare diversi criteri di conservazione per il data lake e i servizi profilo?

+++Risposta
Sì, puoi impostare diversi criteri di conservazione per il data lake e i servizi profilo. Tuttavia, il periodo di conservazione per il profilo non deve essere inferiore a quello impostato per il data lake.
+++

### Come posso verificare l’utilizzo del set di dati corrente?

+++Risposta
Puoi controllare le dimensioni dell&#39;archivio del set di dati più recente per il data lake e gli archivi profilo come metriche separate nell&#39;area di lavoro di inventario [!UICONTROL Set di dati]. Ordinare le colonne per identificare i set di dati più grandi e verificare che siano applicati i criteri di conservazione.

Per l’utilizzo a livello di sandbox, consulta la dashboard Utilizzo licenze. Per informazioni dettagliate, consulta la [documentazione sull&#39;utilizzo delle licenze](../../dashboards/guides/license-usage.md).
+++

### Come posso verificare se il processo di conservazione dei dati ha avuto esito positivo?

+++Risposta
Puoi verificare l&#39;ultimo processo di conservazione dei dati controllandone la marca temporale nell&#39;[interfaccia utente di configurazione conservazione dei set di dati](./user-guide.md#data-retention-policy) o nella pagina Inventario dati.

Il reporting storico sull’utilizzo dei set di dati non è al momento disponibile.
+++

### Posso recuperare i dati eliminati?

+++Risposta
No, una volta applicati i criteri di conservazione, tutti i dati precedenti al periodo di conservazione vengono eliminati definitivamente e non possono essere recuperati.
+++

## Passaggi successivi {#next-steps}

Dopo aver appreso come gestire le impostazioni TTL per la scadenza a livello di riga, consulta la seguente documentazione per comprendere meglio la gestione TTL:

- Processi di conservazione: scopri come pianificare e automatizzare le scadenze dei set di dati nell’interfaccia utente di Platform con la [guida dell’interfaccia utente del ciclo di vita dei dati](../../hygiene/ui/dataset-expiration.md), oppure controlla le configurazioni di conservazione dei set di dati e verifica che i record scaduti vengano eliminati.
- [Guida dell&#39;endpoint API per la scadenza del set di dati](../../hygiene/api/dataset-expiration.md): scopri come eliminare interi set di dati anziché solo le righe. Scopri come pianificare, gestire e automatizzare la scadenza dei set di dati utilizzando l’API per garantire un’efficiente conservazione dei dati.
- [Panoramica sui criteri di utilizzo dei dati](../../data-governance/policies/overview.md): scopri come allineare la strategia di conservazione dei dati con requisiti di conformità più ampi e restrizioni di utilizzo del marketing.
