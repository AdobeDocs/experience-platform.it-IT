---
title: Endpoint API di scadenza set di dati
description: L’endpoint /ttl nell’API di igiene dei dati consente di pianificare in modo programmatico le scadenze dei set di dati in Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 2%

---

# Endpoint di scadenza del set di dati

Utilizza l&#39;endpoint `/ttl` nell&#39;API di igiene dei dati per pianificare l&#39;eliminazione dei set di dati in Adobe Experience Platform.

La scadenza di un set di dati è un’operazione di eliminazione ritardata. Il set di dati non è protetto nel frattempo e può essere eliminato in altro modo prima della scadenza pianificata.

>[!NOTE]
>
>Sebbene la scadenza sia specificata come un momento specifico nel tempo, possono trascorrere fino a 24 ore dalla scadenza prima che venga avviata l’effettiva cancellazione. Una volta avviata l’eliminazione, possono essere necessari fino a sette giorni prima che tutte le tracce del set di dati siano state rimosse dai sistemi Experience Platform.

Prima dell’inizio dell’eliminazione, puoi annullare la scadenza o modificarne l’ora pianificata. Per riaprire una scadenza annullata, impostare una nuova scadenza.

Una volta avviata l&#39;eliminazione, il processo di scadenza viene contrassegnato come `executing` e non può più essere modificato. Il set di dati può essere recuperabile per un massimo di sette giorni, ma solo tramite una richiesta manuale del servizio Adobe. Durante l’eliminazione, il data lake, Identity Service e Real-Time Customer Profile rimuovono ciascuno i contenuti del set di dati separatamente. Al termine dell&#39;eliminazione, la scadenza viene contrassegnata come `completed`.

>[!WARNING]
>
>Se un set di dati è impostato per la scadenza, è necessario modificare manualmente i flussi di dati che potrebbero acquisire dati in tale set di dati in modo che i flussi di lavoro a valle non vengano influenzati negativamente.

Advanced Data Lifecycle Management supporta le eliminazioni dei set di dati tramite l&#39;endpoint di scadenza del set di dati e le eliminazioni degli ID (dati a livello di riga) tramite identità primarie tramite l&#39;[endpoint dell&#39;ordine di lavoro](./workorder.md). Puoi anche gestire [scadenze set di dati](../ui/dataset-expiration.md) e [eliminazioni record](../ui/record-delete.md) tramite l&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni, consulta la documentazione collegata.

>[!NOTE]
>
>Il ciclo di vita dei dati non supporta l’eliminazione in batch.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, consulta la [guida API](./overview.md) per informazioni sulle intestazioni richieste per operazioni CRUD, messaggi di errore, raccolte Postman e come leggere chiamate API di esempio.

>[!IMPORTANT]
>
>Quando effettui chiamate all’API di igiene dei dati, devi utilizzare l’intestazione -H `x-sandbox-name: {SANDBOX_NAME}`.

## Elenca scadenze set di dati {#list}

È possibile elencare tutte le scadenze dei set di dati configurate per l&#39;organizzazione effettuando una richiesta GET all&#39;endpoint `/ttl`.

Filtra i risultati utilizzando i parametri di query per restituire solo le scadenze che soddisfano i criteri. Ogni risultato include lo stato e i dettagli di configurazione per ogni scadenza del set di dati.

**Formato API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETERS}` | Elenco di parametri di query facoltativi, con più parametri separati da `&` caratteri. I parametri comuni includono `limit` e `page` a scopo di impaginazione. Per un elenco completo dei parametri di query supportati, fare riferimento alla [sezione dell&#39;appendice](#query-params) un elenco completo dei parametri di query supportati. I parametri più comunemente utilizzati sono riportati di seguito e anche nell’appendice. |
| `author` | Filtra in base all’utente che ha aggiornato o creato la scadenza del set di dati più di recente. Supporta modelli di tipo SQL (ad esempio, `LIKE %john%`). |
| `datasetId` | Filtra le scadenze per un ID set di dati specifico. |
| `datasetName` | Filtro senza distinzione tra maiuscole e minuscole per le corrispondenze nei nomi dei set di dati. |
| `status` | Filtra in base a un elenco di stati separati da virgole: `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filtra per le scadenze con una data di scadenza specifica. |
| `limit` | Specifica il numero massimo di risultati da restituire (1-100, valore predefinito: 25). |
| `page` | Impaginare i risultati con un indice basato su zero (dimensioni pagina predefinite: 50, max: 100). |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera tutte le scadenze del set di dati aggiornate prima del 1° agosto 2021 e aggiornate da ultimo da un utente il cui nome corrisponde a &quot;Jane Doe&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta elenca le scadenze risultanti del set di dati. L&#39;esempio seguente è stato troncato per motivi di spazio.

>[!IMPORTANT]
>
>Il `ttlId` nella risposta è anche indicato come `{DATASET_EXPIRATION_ID}`. Entrambi fanno riferimento all’identificatore univoco per la scadenza del set di dati.

```json
{
  "results": [
    {
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Proprietà | Descrizione |
| --- | --- |
| `results` | Array delle configurazioni di scadenza dei set di dati. |
| `ttlId` | L’identificatore univoco per la configurazione della scadenza del set di dati. |
| `datasetId` | L’identificatore univoco del set di dati associato a questa configurazione. |
| `datasetName` | Nome del set di dati. |
| `sandboxName` | La sandbox in cui è configurata la scadenza di questo set di dati. |
| `displayName` | Nome leggibile per la configurazione di scadenza. |
| `description` | Una descrizione della configurazione di scadenza. |
| `imsOrg` | L’identificatore univoco dell’organizzazione. |
| `status` | Lo stato corrente della scadenza. Uno di: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La data e l’ora di scadenza pianificata (formato ISO 8601). |
| `updatedAt` | La marca temporale dell’ultimo aggiornamento a questa configurazione. |
| `updatedBy` | L’identificatore e l’e-mail dell’utente o del servizio che ha aggiornato per ultimo la configurazione. |
| `current_page` | Indice della pagina dei risultati corrente (basato su zero). |
| `total_pages` | Numero totale di pagine di risultati disponibili. |
| `total_count` | Numero totale di record di configurazione della scadenza del set di dati restituiti. |

{style="table-layout:auto"}

## Cercare una scadenza del set di dati {#lookup}

Recupera i dettagli per una specifica configurazione di scadenza del set di dati effettuando una richiesta GET con l’ID di scadenza del set di dati o l’ID del set di dati come parametro del percorso.

>[!IMPORTANT]
>
>È possibile fornire un ID di scadenza del set di dati (ad esempio, `SD-xxxxxx-xxxx`) o un ID del set di dati nel percorso. `ttlId` nella risposta è l&#39;identificatore univoco per la scadenza del set di dati.

**Formato API**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Parametro | Descrizione |
| --- | --- |
| `{ID}` | L’identificatore univoco per la configurazione della scadenza del set di dati. Puoi fornire un ID di scadenza del set di dati o un ID del set di dati. |
| `include` | (Facoltativo) Se è impostato su `history`, la risposta include un array `history` con eventi di modifica per la configurazione. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente cerca i dettagli di scadenza per il set di dati `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della scadenza del set di dati.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | L’identificatore univoco per la configurazione della scadenza del set di dati. |
| `datasetId` | L’identificatore univoco del set di dati. |
| `datasetName` | Nome del set di dati. |
| `sandboxName` | La sandbox in cui è configurata la scadenza del set di dati. |
| `displayName` | Nome leggibile per la configurazione di scadenza del set di dati. |
| `description` | Una descrizione della configurazione della scadenza del set di dati. |
| `imsOrg` | L’identificatore organizzazione univoco associato a questa configurazione. |
| `status` | Lo stato corrente della configurazione di scadenza del set di dati.<br>Uno di: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La marca temporale di scadenza pianificata per il set di dati (formato ISO 8601). |
| `updatedAt` | Timestamp dell’aggiornamento più recente. |
| `updatedBy` | L’identificatore e l’e-mail dell’utente o del servizio che ha aggiornato per ultimo la scadenza del set di dati. |

{style="table-layout:auto"}

### Tag di scadenza del catalogo

Quando si utilizza l&#39;[API catalogo](../../catalog/api/getting-started.md) per cercare i dettagli del set di dati, se il set di dati ha una scadenza attiva verrà elencato in `tags.adobe/hygiene/ttl`.

Il seguente JSON mostra una risposta Catalog API troncata per un set di dati con valore di scadenza `32503680000000`. Il tag codifica la scadenza come il numero di millisecondi trascorsi dall’epoca Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Creare una scadenza del set di dati {#create}

Crea una nuova configurazione di scadenza del set di dati per definire quando scadrà un set di dati e se sarà idoneo per l’eliminazione.\
Fornisci l’ID del set di dati, la data di scadenza o la data-ora (nel formato ISO 8601), un nome visualizzato e (facoltativamente) una descrizione.

>[!NOTE]
>
>Il valore di scadenza può essere una data (AAAA-MM-GG) o una data e un&#39;ora (AAAA-MM-GGTHH:MM:SSZ). Se specifichi solo una data, il sistema utilizza la mezzanotte UTC (00:00:00Z) di quel giorno. La scadenza deve essere di almeno 24 ore nel futuro.

Per creare una scadenza del set di dati, invia una richiesta POST come mostrato di seguito.

>[!TIP]
>
>Se ricevi un errore 404, accertati che la richiesta non contenga ulteriori barre. Una barra finale può causare un errore nella richiesta POST.

**Formato API**

```http
POST /ttl
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `datasetId` | **Obbligatorio.** Identificatore univoco del set di dati per applicare la scadenza. |
| `expiry` | **Obbligatorio.** Data e ora di scadenza nel formato ISO 8601. Questo definisce la durata dei dati all’interno del sistema. Se viene fornita solo una data, il valore predefinito è mezzanotte UTC (00:00:00Z). La scadenza **deve essere di almeno 24 ore nel futuro**. <br>**NOTA**:<ul><li>La richiesta non riuscirà se per il set di dati esiste già una scadenza del set di dati.</li></ul> |
| `displayName` | **Obbligatorio.** Nome leggibile per la configurazione di scadenza del set di dati. |
| `description` | Descrizione facoltativa per la configurazione della scadenza del set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e la nuova configurazione di scadenza del set di dati.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | L’identificatore univoco per la configurazione di scadenza del set di dati creato. |
| `datasetId` | L’identificatore univoco del set di dati. |
| `datasetName` | Nome del set di dati. |
| `sandboxName` | La sandbox in cui è configurata la scadenza di questo set di dati. |
| `displayName` | Nome visualizzato per la configurazione di scadenza del set di dati. |
| `description` | Una descrizione della configurazione della scadenza del set di dati. |
| `imsOrg` | L’identificatore organizzazione univoco associato a questa configurazione. |
| `status` | Lo stato corrente della configurazione di scadenza del set di dati.<br>Uno di: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Il timestamp di scadenza pianificato per il set di dati. |
| `updatedAt` | Il timestamp dell’aggiornamento più recente. |
| `updatedBy` | L’identificatore e l’e-mail dell’utente o del servizio che ha aggiornato per ultimo la configurazione di scadenza del set di dati. |

Se per il set di dati esiste già una scadenza, si verifica uno stato HTTP 400 (richiesta non valida). Lo stato HTTP 404 (Non trovato) si verifica se non esiste un set di dati o se non si dispone dell’accesso al set di dati.

## Aggiornare una configurazione di scadenza del set di dati {#update}

Per aggiornare una configurazione di scadenza di un set di dati esistente, effettuare una richiesta PUT a `/ttl/DATASET_EXPIRATION_ID`. È possibile aggiornare solo i campi `displayName`, `description` e `expiry` della configurazione. Gli aggiornamenti sono consentiti solo quando lo stato di scadenza è `pending`.

>[!NOTE]
>
>Il campo `expiry` accetta una data (AAAA-MM-GG) o una data e un&#39;ora (AAAA-MM-GG:MM:SSZ). Se viene fornita solo una data, il sistema utilizza la mezzanotte UTC (00:00:00Z) di quel giorno. La scadenza **deve essere di almeno 24 ore nel futuro**.

**Formato API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | L’identificatore univoco per la configurazione della scadenza del set di dati. **NOTA**: nella risposta viene indicato come `ttlId`. |

**Richiesta**

La richiesta seguente aggiorna la scadenza, il nome visualizzato e la descrizione per la scadenza del set di dati `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`:

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `displayName` | (Facoltativo) Nuovo nome leggibile per la configurazione di scadenza del set di dati. |
| `description` | (Facoltativo) Nuova descrizione per la configurazione della scadenza del set di dati. |
| `expiry` | (Facoltativo) Una nuova data di scadenza o data e ora nel formato ISO 8601. Se viene fornita solo una data, il valore predefinito è mezzanotte UTC. La scadenza deve essere **di almeno 24 ore nel futuro**. |

>[!NOTE]
>
>Almeno uno di questi campi deve essere fornito nella richiesta.

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) e la configurazione di scadenza del set di dati aggiornata.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | L’identificatore univoco della configurazione di scadenza del set di dati aggiornato. |
| `datasetId` | L’identificatore univoco del set di dati. |
| `datasetName` | Nome del set di dati. |
| `sandboxName` | La sandbox in cui è configurata la scadenza di questo set di dati. |
| `displayName` | Nome visualizzato per la configurazione di scadenza del set di dati. |
| `description` | Una descrizione della configurazione della scadenza del set di dati. |
| `imsOrg` | L’ID organizzazione associato a questa configurazione. |
| `status` | Lo stato corrente della configurazione di scadenza del set di dati.<br>Uno di: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Il timestamp di scadenza pianificato per il set di dati. |
| `updatedAt` | Il timestamp dell’aggiornamento più recente. |
| `updatedBy` | L’identificatore e l’e-mail dell’utente o del servizio che ha aggiornato per ultimo la configurazione di scadenza del set di dati. |

{style="table-layout:auto"}

In caso di esito negativo, la risposta restituisce lo stato HTTP 404 (Non trovato) se non esiste una scadenza del set di dati.

## Annullare la scadenza di un set di dati {#delete}

Annullare una configurazione di scadenza di un set di dati in sospeso effettuando una richiesta DELETE a `/ttl/{ID}`.

>[!NOTE]
>
>È possibile annullare solo le scadenze dei set di dati nello stato `pending`. Il tentativo di annullare una scadenza già `executing`, `completed` o `cancelled` restituisce HTTP 400 (richiesta non valida).

**Formato API**

```http
DELETE /ttl/{ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{ID}` | L’identificatore univoco per la configurazione della scadenza del set di dati. Puoi fornire un ID di scadenza del set di dati o un ID del set di dati. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente annulla la scadenza di un set di dati con ID `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) e la configurazione della scadenza del set di dati annullata. L&#39;attributo `status` della scadenza non è impostato su `cancelled`.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Proprietà | Descrizione |
|---|---|
| `ttlId` | L’identificatore univoco della configurazione di scadenza del set di dati eliminato. |
| `datasetId` | L’identificatore univoco del set di dati. |
| `datasetName` | Nome del set di dati. |
| `sandboxName` | La sandbox in cui è configurata la scadenza di questo set di dati. |
| `displayName` | Nome visualizzato per la configurazione di scadenza del set di dati. |
| `description` | Una descrizione della configurazione della scadenza del set di dati. |
| `imsOrg` | L’identificatore organizzazione univoco associato a questa configurazione. |
| `status` | Lo stato corrente della configurazione di scadenza del set di dati.<br>Uno di: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Il timestamp di scadenza pianificato per il set di dati. |
| `updatedAt` | Il timestamp dell’aggiornamento più recente. |
| `updatedBy` | L’identificatore e l’e-mail dell’utente o del servizio che ha aggiornato per ultimo la configurazione di scadenza del set di dati. |

**Esempio di risposta 400 (richiesta non valida)**

Errore 400 durante il tentativo di annullare un set di dati con una configurazione di scadenza `executing`, `completed` o `cancelled`.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Errore 404 durante il tentativo di annullare la scadenza di un set di dati già `completed` o `cancelled`.

## Appendice

### Parametri di query accettati {#query-params}

La tabella seguente illustra i parametri di query disponibili quando [si elencano le scadenze dei set di dati](#list):

>[!NOTE]
>
>I parametri `description`, `displayName` e `datasetName` contengono tutti la possibilità di eseguire ricerche per valori LIKE. Ciò significa che puoi trovare le scadenze pianificate del set di dati denominate: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; cercando la stringa &quot;Name1&quot;.

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `author` | Utilizzare il parametro di query `author` per trovare la persona che ha aggiornato più di recente la scadenza del set di dati. Se non sono stati apportati aggiornamenti dalla sua creazione, corrisponderà al creatore originale della scadenza. Questo parametro corrisponde alle scadenze in cui il campo `created_by` corrisponde alla stringa di ricerca.<br>Se la stringa di ricerca inizia con `LIKE` o `NOT LIKE`, il resto viene trattato come un modello di ricerca SQL. In caso contrario, l&#39;intera stringa di ricerca viene trattata come una stringa letterale che deve corrispondere esattamente all&#39;intero contenuto di un campo `created_by`. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Corrisponde alle scadenze che si applicano a un set di dati specifico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Corrisponde a scadenze il cui nome del set di dati contiene la stringa di ricerca fornita. La corrispondenza non distingue tra maiuscole e minuscole. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Corrisponde a scadenze il cui nome visualizzato contiene la stringa di ricerca fornita. La corrispondenza non distingue tra maiuscole e minuscole. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtra i risultati in base a una data di esecuzione esatta, una data di fine per l’esecuzione o una data di inizio per l’esecuzione. Vengono utilizzati per recuperare dati o record associati all&#39;esecuzione di un&#39;operazione in una data specifica, prima di una data specifica o dopo una data specifica. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Corrisponde alle scadenze che si sono verificate nell’intervallo di 24 ore della data specificata. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Corrisponde alle scadenze che devono essere eseguite, o che sono già state eseguite, durante l’intervallo specificato. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Un numero intero compreso tra 1 e 100 che indica il numero massimo di scadenze da restituire. Impostazione predefinita: 25. | `limit=50` |
| `orderBy` | Il parametro di query `orderBy` specifica l&#39;ordinamento dei risultati restituiti dall&#39;API. Utilizzalo per disporre i dati in base a uno o più campi, in ordine crescente (ASC) o decrescente (DESC). Utilizzare il prefisso + o - per indicare rispettivamente ASC e DESC. Sono accettati i seguenti valori: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Corrisponde alle scadenze dei set di dati il cui ID organizzazione corrisponde a quello del parametro. Il valore predefinito è quello delle intestazioni `x-gw-ims-org-id` e viene ignorato a meno che la richiesta non fornisca un token di servizio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Numero intero che indica la pagina di scadenze da restituire. | `page=3` |
| `sandboxName` | Corrisponde alle scadenze del set di dati il cui nome di sandbox corrisponde esattamente all’argomento. Viene impostato automaticamente sul nome della sandbox nell&#39;intestazione `x-sandbox-name` della richiesta. Utilizza `sandboxName=*` per includere le scadenze dei set di dati da tutte le sandbox. | `sandboxName=dev1` |
| `search` | Corrisponde alle scadenze in cui la stringa specificata corrisponde esattamente all&#39;ID scadenza o è **contenuto** in uno dei campi seguenti:<br><ul><li>autore</li><li>nome visualizzato</li><li>descrizione</li><li>nome visualizzato</li><li>nome set di dati</li></ul> | `search=TESTING` |
| `status` | Elenco di stati separato da virgole. Se inclusa, la risposta corrisponde alle scadenze del set di dati il cui stato corrente è tra quelli elencati. | `status=pending,cancelled` |
| `ttlId` | Corrisponde alla richiesta di scadenza con l’ID specificato. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Corrisponde alle scadenze aggiornate nella finestra di 24 ore della data specificata. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Corrisponde alle scadenze aggiornate nella finestra di 24 ore a partire dall’ora indicata.<br><br>Una scadenza viene considerata aggiornata a ogni modifica, anche quando viene creata, annullata o eseguita. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

