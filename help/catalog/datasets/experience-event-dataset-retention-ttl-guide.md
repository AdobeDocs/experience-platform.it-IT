---
title: Gestire la conservazione dei set di dati di Experience Event nel Data Lake tramite TTL
description: Scopri come valutare, impostare e gestire la conservazione dei set di dati di Experience Event nel data lake utilizzando le configurazioni Time-To-Live (TTL) con le API di Adobe Experience Platform. Questa guida spiega come la scadenza a livello di riga TTL supporti le regole di conservazione dei dati, ottimizzi l'efficienza dello storage e garantisca un'efficace gestione del ciclo di vita dei dati. Inoltre, fornisce casi d’uso e best practice per aiutarti ad applicare il TTL in modo efficace.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: a4662d1042122fa9c3260c0e53c50bd78935cf31
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 0%

---

# Gestire la conservazione dei set di dati di Experience Event nel data lake utilizzando TTL

Una gestione efficiente dei dati è fondamentale per garantire prestazioni ottimali, controllo dei costi e integrità dei dati. Utilizza il TTL (Experience Event Dataset Retention Time-To-Live) per applicare la scadenza a livello di riga, rimuovendo automaticamente i record obsoleti dai set di dati nel data lake e garantendo al contempo un’efficienza di archiviazione e una rilevanza dei dati ottimali.

Questa guida spiega come valutare, impostare e gestire il TTL utilizzando l’API Catalog Service. Scoprirai quando e perché applicare il TTL, come configurare e aggiornare i valori TTL utilizzando le chiamate API e le best practice per garantire un’implementazione efficace.

>[!IMPORTANT]
>
>TTL è progettato per ottimizzare la gestione del ciclo di vita dei dati e l&#39;efficienza dello storage. Non è uno strumento di conformità e non dovrebbe essere utilizzato per i requisiti normativi. La conformità richiede spesso strategie di governance dei dati più ampie.

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

Utilizza le configurazioni TTL per ottimizzare lo storage in base ai diritti. Anche se i dati dell’archivio profili (utilizzati in Real-Time CDP) possono essere considerati obsoleti e rimossi dopo 30 giorni, gli stessi dati evento nel data lake possono rimanere disponibili per 12-13 mesi (o più in base all’adesione) per i casi di utilizzo di Analytics e Data Distiller.

>[!TIP]
>
>I diritti si riferiscono alle quote di archiviazione e conservazione definite dall’abbonamento Adobe e dai contratti di licenza.

### Esempio di settore {#industry-example}

Ad esempio, considera un servizio di streaming video che tiene traccia delle interazioni degli utenti, come visualizzazioni video, ricerche e consigli. Anche se i dati di coinvolgimento recenti sono fondamentali per la personalizzazione, i registri di attività più datati (ad esempio, le interazioni di più di un anno fa) perdono rilevanza. Utilizzando la scadenza a livello di riga, Experience Platform rimuove automaticamente i registri obsoleti, garantendo che solo i dati correnti e significativi vengano utilizzati per le analisi e i consigli.

## Valuta idoneità TTL {#evaluate-ttl-suitability}

Prima di applicare un criterio di conservazione, valuta se il set di dati è un buon candidato per la scadenza a livello di riga. Considera quanto segue:

- Rilevanza dei dati nel tempo: i dati meno recenti forniscono valore o diventano obsoleti?
- Impatto sui processi a valle: la rimozione dei dati influisce su reporting, analisi o integrazioni?
- Costo dello storage rispetto al valore di conservazione: il valore dei dati meno recenti giustifica il costo dello storage?

Se i record storici sono essenziali per l’analisi a lungo termine o le operazioni aziendali, il TTL potrebbe non essere l’approccio corretto. L’analisi di questi fattori garantisce l’allineamento del TTL alle esigenze di conservazione dei dati senza influire negativamente sulla disponibilità dei dati.

## Best practice per l’impostazione del valore TTL {#best-practices}

Seleziona il valore TTL corretto per garantire che i criteri di conservazione dei set di dati di Experience Event bilancino la conservazione dei dati, l’efficienza dello storage e le esigenze di analisi. Un valore TTL troppo breve può causare la perdita di dati, mentre un valore troppo lungo può aumentare i costi di storage e l&#39;accumulo di dati non necessari. Assicurati che il TTL sia allineato allo scopo del set di dati tenendo in considerazione la frequenza con cui viene effettuato l’accesso ai dati e il tempo in cui rimangono rilevanti.

La tabella seguente fornisce consigli comuni su TTL in base al tipo di set di dati e ai pattern di utilizzo:

| Tipo di set di dati | TTL consigliato | Casi d’uso tipici |
|-----------------------------|------------------------|-------------------|
| Set di dati ad accesso frequente | 30-90 giorni | Registri di coinvolgimento degli utenti, dati di clickstream sul sito web, dati sulle prestazioni delle campagne a breve termine. |
| Set di dati di archiviazione | 1 anno o più | Registri delle transazioni finanziarie, dati sulla conformità, analisi delle tendenze a lungo termine, set di dati di formazione per l’apprendimento automatico. |
| Set di dati gestiti dall’app | Fino a 13 mesi | I set di dati gestiti dal sistema hanno restrizioni TTL predefinite, che vengono applicate automaticamente per rispettare i limiti imposti dal sistema. |
| Set di dati gestiti dal cliente | 30 giorni - TTL massimo | Set di dati creati tramite l’interfaccia utente, le API o Data Distiller. Il TTL deve essere di almeno 30 giorni ed entro il TTL massimo definito. |

Rivedere periodicamente le impostazioni TTL per assicurarsi che continuino ad essere allineate alle regole di storage, alle esigenze analitiche e ai requisiti aziendali.

### Considerazioni chiave durante l’impostazione del valore TTL {#key-considerations}

Segui queste best practice per garantire che le impostazioni TTL siano allineate alla strategia di conservazione dei dati:

- Controlla regolarmente le modifiche TTL. Ogni aggiornamento TTL attiva un evento di audit. Utilizza i registri di audit per tenere traccia delle modifiche TTL a scopo di conformità, governance dei dati e risoluzione dei problemi.
- Disattiva TTL se i dati devono essere conservati per un tempo indefinito. Per disabilitare il TTL, impostare `ttlValue` su `null`. Ciò impedisce la scadenza automatica e mantiene tutti i record in modo permanente. Prima di apportare questa modifica, è necessario considerare le implicazioni relative allo storage.

## Limitazioni del TTL {#limitations}

Tieni presente le seguenti limitazioni quando utilizzi TTL:

- **La conservazione del set di dati Experience Event tramite TTL si applica alla scadenza a livello di riga**, non all&#39;eliminazione del set di dati. TTL rimuove i record in base a un periodo di conservazione definito, ma non elimina interi set di dati. Per rimuovere un set di dati, utilizzare l&#39;endpoint di scadenza [del set di dati](../../hygiene/api/dataset-expiration.md) o l&#39;eliminazione manuale.
- **La configurazione TTL rimane attiva fino a quando non viene disabilitata in modo esplicito**. La configurazione rimane attiva finché non la disattivi. La disabilitazione di TTL interrompe la scadenza e garantisce che tutti i record nel set di dati vengano mantenuti.
- **TTL non è uno strumento di conformità**. Mentre TTL ottimizza lo storage e la gestione del ciclo di vita, è necessario implementare strategie di governance più ampie per garantire la conformità alle normative.

## Analizzare la dimensione e la rilevanza del set di dati prima di applicare il TTL {#analyze-dataset-size}

Prima di applicare il TTL, utilizza le query per analizzare le dimensioni e la rilevanza del set di dati. Esegui query mirate (come il conteggio dei record all’interno di intervalli di date specifici) per visualizzare in anteprima l’impatto di vari valori TTL. Quindi utilizza queste informazioni per scegliere un periodo di conservazione ottimale che bilanci l’utilità dei dati e la convenienza economica.

![Flusso di lavoro visivo per l&#39;implementazione di TTL nei set di dati dell&#39;evento esperienza. I passaggi includono: valutare la durata dei dati e l&#39;impatto della rimozione, convalidare le impostazioni TTL con le query, configurare il TTL tramite l&#39;API Catalog Service, monitorare costantemente l&#39;impatto del TTL e apportare le modifiche necessarie.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

L’esecuzione di query mirate consente di determinare la quantità di dati da mantenere o rimuovere in diverse configurazioni TTL. Ad esempio, la query SQL seguente conta il numero di record creati negli ultimi 30 giorni:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

L’esecuzione di query simili per intervalli di tempo diversi consente di convalidare le impostazioni TTL e di garantire il bilanciamento tra l’efficienza dello storage e l’accessibilità dei dati.

## Introduzione alla gestione TTL

Prima di poter valutare, impostare e gestire la conservazione dei set di dati di Experience Event utilizzando l’API Catalog Service, è necessario comprendere come formattare correttamente le richieste. Ciò include la conoscenza dei percorsi API, la fornitura delle intestazioni richieste e la formattazione dei payload di richiesta. Per informazioni essenziali, fare riferimento alla [guida introduttiva all&#39;API Catalog Service](../api/getting-started.md).

>[!NOTE]
>
>Questo documento descrive la scadenza a livello di riga, che elimina singole righe scadute all’interno di un set di dati mantenendo intatto il set di dati stesso. Non si applica alla scadenza del set di dati, che rimuove interi set di dati ed è gestito da una funzione separata. Per informazioni sulla scadenza a livello di set di dati, consulta la [documentazione API relativa alla scadenza del set di dati](../../hygiene/api/dataset-expiration.md).

### Verifica i vincoli TTL {#check-ttl-constraints}

Utilizza l’endpoint API di igiene dei dati `/ttl/{DATASET_ID}` per pianificare le configurazioni TTL. Questo endpoint restituisce i valori TTL minimi e massimi supportati per l&#39;organizzazione, insieme a un valore consigliato (`defaultValue`) per il tipo di set di dati.

Per ulteriori informazioni, consulta la documentazione dell&#39;[API di igiene dei dati](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) di Adobe Developer.

Per [controllare il TTL attualmente applicato a un set di dati](#check-applied-ttl-values), effettuare una richiesta GET all&#39;endpoint [ &lbrace;API](https://developer.adobe.com/experience-platform-apis/references/catalog/) di Catalog Service `/dataSets/{DATASET_ID}`.

>[!TIP]
>
>L&#39;URL del gateway Experience Platform e il percorso di base per l&#39;API del servizio catalogo sono: `https://platform.adobe.io/data/foundation/catalog`. Percorso di base per l&#39;API di igiene dei dati: `https://platform.adobe.io/data/core/hygiene`

**Formato API**

```http
GET /ttl/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Stringa generata dal sistema che identifica in modo univoco un set di dati. Per trovare un ID di set di dati, utilizza l&#39;endpoint `/datasets`. Per istruzioni su come filtrare le risposte per i set di dati rilevanti, consulta la [guida API per oggetti catalogo ](../api/list-objects.md). |

**Richiesta**

La richiesta seguente recupera i vincoli TTL dell’organizzazione per un particolare set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i valori TTL consigliati, massimi e minimi in base ai diritti dell&#39;organizzazione, insieme a un valore TTL (`defaultValue`) suggerito per il set di dati. `defaultValue` è una durata TTL consigliata, fornita solo a scopo informativo. Non viene applicato a meno che non sia stato esplicitamente configurato da te. La risposta non include eventuali valori TTL personalizzati già impostati. Per visualizzare il TTL corrente per un set di dati, utilizzare l&#39;endpoint GET `/catalog/dataSets/{DATASET_ID}`.

+++Seleziona per visualizzare la risposta

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Proprietà | Descrizione |
|--------------|-------------|
| `defaultValue` | Valore TTL consigliato per il set di dati. Questo valore è **non** applicato automaticamente. Per rendere effettivo il valore TTL, è necessario impostarlo esplicitamente. |
| `maxValue` | La durata TTL massima consentita dall’adesione della tua organizzazione. In genere, la durata è di 10 anni (`P10Y`). |
| `minValue` | La durata TTL minima consentita dall’adesione della tua organizzazione. In genere, la durata è di 30 giorni (`P30D`). |

### Controllare i valori TTL applicati {#check-applied-ttl-values}

Per verificare il valore TTL corrente applicato a un set di dati, utilizza la seguente chiamata API:

```http
GET /dataSets/{DATASET_ID}
```

Questa chiamata restituisce l&#39;attuale `ttlValue` (se impostato) nella sezione `extensions.adobe_lakeHouse.rowExpiration`.

**Richiesta**

La richiesta seguente recupera il valore TTL dell’organizzazione per un particolare set di dati.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include l&#39;oggetto `extensions`, che contiene la configurazione TTL corrente applicata al set di dati. L’esempio di risposta seguente viene troncato per brevità.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### Impostare o aggiornare il TTL per un set di dati {#set-update-ttl}

>[!IMPORTANT]
>
>La scadenza a livello di riga basata su TTL può essere applicata solo ai set di dati evento che utilizzano uno schema di serie temporali. Sono inclusi i set di dati basati sulla classe XDM ExperienceEvent standard e gli schemi personalizzati che estendono lo schema della serie temporale (`https://ns.adobe.com/xdm/data/time-series`).
>
>Prima di applicare il TTL, utilizza l’API Schema Registry per verificare che lo schema del set di dati includa l’estensione corretta controllando la proprietà `meta:extends`. Per istruzioni su come eseguire questa operazione, consulta la [documentazione dell&#39;endpoint schema](../../xdm/api/schemas.md#lookup).

Puoi configurare Conservazione set di dati di Experience Event impostando un nuovo TTL o aggiornando un TTL esistente utilizzando lo stesso metodo API. Utilizza una richiesta PATCH all&#39;endpoint `/v2/datasets/{DATASET_ID}` per applicare o modificare il TTL.

**Formato API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati per cui desideri aggiornare il valore TTL. |

**Richiesta**

Nell&#39;esempio seguente, `ttlValue` è impostato su `P3M`. Ciò significa che i record più vecchi di tre mesi vengono eliminati automaticamente. Regolare il periodo di conservazione in base alle esigenze aziendali (ad esempio, `P6M` per sei mesi o `P12M` per un anno).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Proprietà | Descrizione |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Definisce la durata prima della rimozione automatica dei record nel set di dati. Utilizza il formato del periodo ISO-8601 (ad esempio, `P3M` per 3 mesi o `P30D` per 30 giorni). |

**Risposta**

In caso di esito positivo, la risposta restituisce un riferimento al set di dati aggiornato ma non include esplicitamente le impostazioni TTL. Per confermare la configurazione TTL, effettuare una richiesta di completamento `GET /dataSets/{DATASET_ID}`.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Scenario di esempio {#example-scenario}

Considera una piattaforma di streaming video che inizialmente imposta il TTL a tre mesi per garantire nuovi dati di coinvolgimento per la personalizzazione. Tuttavia, se un’analisi successiva rivela che le interazioni meno recenti forniscono ancora informazioni utili, il TTL può essere esteso a sei mesi con la seguente richiesta:

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Domande frequenti sui criteri di conservazione dei set di dati {#faqs}

Queste domande frequenti riguardano domande pratiche sui processi di conservazione dei set di dati, sugli effetti immediati delle modifiche TTL, sulle opzioni di ripristino e sulle differenze tra i periodi di conservazione dei diversi servizi di Platform.

### A quali tipi di set di dati è possibile applicare le regole dei criteri di conservazione?

+++Risposta
È possibile applicare criteri di conservazione basati su TTL a qualsiasi set di dati che utilizza il comportamento della serie temporale. Ciò include set di dati basati sulla classe XDM ExperienceEvent standard, nonché schemi personalizzati progettati per acquisire dati di serie temporali.

La scadenza a livello di riga richiede le seguenti condizioni tecniche:

- Lo schema deve essere progettato per acquisire dati di serie temporali.
- Lo schema deve includere un campo timestamp utilizzato per valutare la scadenza.
- Il set di dati deve memorizzare dati a livello di evento, in genere utilizzando o estendendo la classe XDM ExperienceEvent.
- Il set di dati deve essere registrato in Catalog Service, in quanto le impostazioni TTL vengono applicate tramite `extensions.adobe_lakeHouse.rowExpiration`.
- I valori TTL devono utilizzare il formato di durata ISO-8601 (ad esempio `P30D`, `P6M`, `P1Y`).
+++

### Quando il processo di conservazione del set di dati eliminerà i dati dai servizi del data lake?

+++Risposta
I TTL dei set di dati vengono valutati ed elaborati ogni 30 giorni, eliminando tutti i record scaduti. Un evento è considerato scaduto se è stato acquisito in Experience Platform più di 30 giorni fa (data di acquisizione > 30 giorni) e la sua data evento supera il periodo di conservazione definito (TTL).
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### È possibile impostare diversi criteri di conservazione per il data lake e i servizi profilo?

+++Risposta

>[!NOTE]
>
>Il periodo di conservazione per il servizio profili può essere aggiornato solo una volta ogni 30 giorni.

Sì, puoi impostare diversi criteri di conservazione per il data lake e i servizi profilo. Il periodo di conservazione per l’archivio profili può essere più breve o più lungo del periodo di conservazione del data lake, a seconda delle esigenze della tua organizzazione.

+++

### Come posso verificare l’utilizzo del set di dati corrente?

+++Risposta
Puoi controllare le dimensioni dell&#39;archivio del set di dati più recente per il data lake e gli archivi profilo come metriche separate nell&#39;area di lavoro di inventario [!UICONTROL Set di dati]. Ordinare le colonne per identificare i set di dati più grandi e verificare che siano applicati i criteri di conservazione.

Per l’utilizzo a livello di sandbox, consulta la dashboard Utilizzo licenze. Per informazioni dettagliate, consulta la [documentazione sull&#39;utilizzo delle licenze](../../dashboards/guides/license-usage.md).
+++

### Come posso verificare se il processo di conservazione dei dati ha avuto esito positivo?

+++Risposta
Puoi verificare l&#39;ultimo processo di conservazione dei dati controllandone la marca temporale nell&#39;[interfaccia utente di configurazione conservazione dei set di dati](./user-guide.md#data-retention-policy) o nella pagina Inventario dati.

In alternativa, puoi effettuare una richiesta GET al seguente endpoint:

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

La risposta include la proprietà `extensions.adobe_lakeHouse.rowExpiration.lastCompleted`, che indica la marca temporale Unix (in millisecondi) di quando è stato completato il processo TTL più recente.

Il reporting storico sull’utilizzo dei set di dati non è al momento disponibile.
+++

### Posso recuperare i dati eliminati?

+++Risposta
No, una volta applicati i criteri di conservazione, tutti i dati precedenti al periodo di conservazione vengono eliminati definitivamente e non possono essere recuperati.
+++

### Qual è il TTL minimo che posso configurare su un set di dati Experience Event di un data lake?

+++Risposta 
Il TTL minimo per un set di dati Experience Event del data lake è di 30 giorni. Il data lake funziona come un sistema di elaborazione di backup e ripristino durante l’acquisizione e l’elaborazione iniziali. Di conseguenza, i dati devono rimanere nel data lake per almeno 30 giorni dopo l’acquisizione, prima che possa scadere.
+++

### Cosa succede se devo conservare alcuni campi del data lake più a lungo di quanto consenta il mio criterio TTL?

+++Risposta 
Utilizza Data Distiller per mantenere campi specifici oltre il TTL del set di dati, mantenendo al contempo i limiti di utilizzo. Crea un processo che scrive regolarmente solo i campi necessari in un set di dati derivato. Questo flusso di lavoro garantisce la conformità con un TTL più breve, preservando al contempo i dati critici per un uso esteso.

Per ulteriori dettagli, vedere la [guida Creare set di dati derivati con SQL](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md).
+++

## Passaggi successivi {#next-steps}

Dopo aver appreso come gestire le impostazioni TTL per la scadenza a livello di riga, consulta la seguente documentazione per comprendere meglio la gestione TTL:

- Processi di conservazione: scopri come pianificare e automatizzare le scadenze dei set di dati nell’interfaccia utente di Experience Platform con la [guida dell’interfaccia utente del ciclo di vita dei dati](../../hygiene/ui/dataset-expiration.md), oppure controlla le configurazioni di conservazione dei set di dati e verifica che i record scaduti vengano eliminati.
- [Guida dell&#39;endpoint API per la scadenza del set di dati](../../hygiene/api/dataset-expiration.md): scopri come eliminare interi set di dati anziché solo le righe. Scopri come pianificare, gestire e automatizzare la scadenza dei set di dati utilizzando l’API per garantire un’efficiente conservazione dei dati.
- [Panoramica sui criteri di utilizzo dei dati](../../data-governance/policies/overview.md): scopri come allineare la strategia di conservazione dei dati con requisiti di conformità più ampi e restrizioni di utilizzo del marketing.
