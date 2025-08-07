---
title: Registra ordini di lavoro di eliminazione
description: Scopri come utilizzare l’endpoint /workorder nell’API di igiene dei dati per gestire gli ordini di lavoro di eliminazione dei record in Adobe Experience Platform. Questa guida descrive le quote, le timeline di elaborazione e l’utilizzo delle API.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 4f4b668c2b29228499dc28b2c6c54656e98aaeab
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# Registra ordini di lavoro di eliminazione {#work-order-endpoint}

Utilizza l&#39;endpoint `/workorder` nell&#39;API di igiene dei dati per creare, visualizzare e gestire gli ordini di lavoro di eliminazione dei record in Adobe Experience Platform. Gli ordini di lavoro consentono di controllare, monitorare e tenere traccia della rimozione dei dati tra i set di dati per mantenere la qualità dei dati e supportare gli standard di governance dei dati della tua organizzazione.

>[!IMPORTANT]
>
>Gli ordini di lavoro di eliminazione dei record servono per la pulizia dei dati, la rimozione di dati anonimi o la minimizzazione dei dati. **Non utilizzare gli ordini di lavoro di eliminazione record per le richieste di diritti dell&#39;interessato in base alle normative sulla privacy come il RGPD.** Per i casi di utilizzo di conformità, utilizzare [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Introduzione

Prima di iniziare, consulta la [panoramica](./overview.md) per scoprire le intestazioni richieste, come leggere le chiamate API di esempio e dove trovare la relativa documentazione.

## Quote e timeline di elaborazione {#quotas}

Registra gli ordini di lavoro di eliminazione sono soggetti ai limiti di invio giornalieri e mensili degli identificatori, determinati dal diritto di licenza della tua organizzazione. Questi limiti si applicano sia alle richieste di cancellazione dei record basate su API che su UI.

>[!NOTE]
>
>Puoi inviare fino a **1.000.000 identificatori al giorno**, ma solo se lo consente la quota mensile rimanente. Se il limite mensile è inferiore a 1 milione, le richieste giornaliere non possono superare tale limite.

### Diritto invio mensile per prodotto {#quota-limits}

La tabella seguente mostra i limiti di invio degli identificatori per prodotto e livello di adesione. Per ogni prodotto, il limite mensile è il minore tra due valori: un limite fisso di identificazione o una soglia basata su percentuale associata al volume di dati concesso in licenza.

| Prodotto | Descrizione diritto | Limite mensile (scegliendo il valore minore) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 2.000.000 identificatori o il 5% del pubblico indirizzabile |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 15.000.000 identificatori o il 10% del pubblico indirizzabile |
| Customer Journey Analytics | Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 2.000.000 identificatori o 100 identificatori per milione di righe CJA di diritto |
| Customer Journey Analytics | Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 15.000.000 identificatori o 200 identificatori per milione di righe CJA di diritto |

>[!NOTE]
>
>La maggior parte delle organizzazioni avrà limiti mensili inferiori in base al proprio pubblico indirizzabile effettivo o ai diritti di riga di CJA.

>[!NOTE]
>
>Le quote vengono reimpostate il primo giorno di ogni mese di calendario. La quota non utilizzata **non** viene riportata.

>[!NOTE]
>
>L&#39;utilizzo della quota si basa sul diritto mensile concesso in licenza dalla tua organizzazione per **identificatori inviati**. Le quote non vengono applicate dai guardrail di sistema, ma possono essere monitorate e riviste.\
>La capacità dell&#39;ordine di lavoro di eliminazione del record è un **servizio condiviso**. Il limite mensile riflette il diritto più alto tra Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics ed eventuali componenti aggiuntivi Shield applicabili.

### Elaborazione dei timeline per l’invio degli identificatori {#sla-processing-timelines}

Dopo la sottomissione, gli ordini di lavorazione di eliminazione dei record vengono messi in coda ed elaborati in base al livello di adesione.

| Descrizione del prodotto e della licenza | Durata coda | Tempo di elaborazione massimo (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | Fino a 15 giorni | 30 giorni |
| Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | In genere 24 ore | 15 giorni |

Se l’organizzazione richiede limiti più elevati, contatta il rappresentante Adobe per una revisione dell’adesione.

>[!TIP]
>
>Per verificare l&#39;utilizzo o il livello di adesione corrente, vedere la [Guida di riferimento della quota](../api/quota.md).

## Elenca gli ordini di lavoro di eliminazione record {#list}

Recuperare un elenco impaginato di ordini di lavoro di eliminazione record per le operazioni di igiene dei dati nell&#39;organizzazione. Filtra i risultati utilizzando i parametri di query. Ogni record dell&#39;ordine di lavoro include il tipo di azione (ad esempio `identity-delete`), lo stato, il set di dati correlato, i dettagli utente e i metadati di controllo.

**Formato API**

```http
GET /workorder
```

Nella tabella seguente vengono descritti i parametri di query disponibili per elencare gli ordini di lavorazione per l&#39;eliminazione dei record.

| Parametro query | Descrizione |
| --------------- | ------------|
| `search` | Corrispondenza parziale senza distinzione tra maiuscole e minuscole (ricerca con caratteri jolly) nei campi: author, displayName, description o datasetName. Corrisponde anche all’ID di scadenza esatto. |
| `type` | Filtrare i risultati per tipo di ordine di lavoro (ad esempio, `identity-delete`). |
| `status` | Elenco separato da virgole degli stati degli ordini di lavoro. I valori di stato fanno distinzione tra maiuscole e minuscole.<br>Enum: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Individuare l&#39;ultimo utente che ha aggiornato l&#39;ordine di lavoro (o l&#39;autore originale). Accetta pattern letterale o SQL. |
| `displayName` | Corrispondenza senza distinzione tra maiuscole e minuscole per il nome visualizzato dell&#39;ordine di lavoro. |
| `description` | Corrispondenza senza distinzione tra maiuscole e minuscole per la descrizione dell&#39;ordine di lavoro. |
| `workorderId` | Corrispondenza esatta per l&#39;ID ordine di lavoro. |
| `sandboxName` | Corrispondenza esatta per il nome della sandbox utilizzato nella richiesta, oppure utilizzare `*` per includere tutte le sandbox. |
| `fromDate` | Consente di filtrare in base agli ordini di lavorazione creati in questa data o in data successiva. Richiede `toDate` per essere impostato. |
| `toDate` | Consente di filtrare in base agli ordini di lavorazione creati prima o in corrispondenza di questa data. Richiede `fromDate` per essere impostato. |
| `filterDate` | Restituisce solo gli ordini di lavorazione creati, aggiornati o modificati in questa data. |
| `page` | Indice di pagina da restituire (inizia da 0). |
| `limit` | Numero massimo di risultati per pagina (1-100, impostazione predefinita: 25). |
| `orderBy` | Ordinamento dei risultati. Utilizza il prefisso `+` o `-` per l&#39;ordine crescente/decrescente. Esempio: `orderBy=-datasetName`. |
| `properties` | Elenco separato da virgole di campi aggiuntivi da includere per risultato. Facoltativo. |


**Richiesta**

La richiesta seguente recupera tutti gli ordini di lavoro di eliminazione record completati, limitati a due per pagina:

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco impaginato di ordini di lavoro di eliminazione record.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

Nella tabella seguente sono descritte le proprietà della risposta.

| Proprietà | Descrizione |
| --- | --- |
| `results` | Array di record elimina gli oggetti dell&#39;ordine di lavoro. Ogni oggetto contiene i campi riportati di seguito. |
| `workorderId` | Identificatore univoco dell&#39;ordine di lavoro di eliminazione record. |
| `orgId` | L’identificatore univoco dell’organizzazione. |
| `bundleId` | Identificatore univoco del bundle contenente questo ordine di lavoro di eliminazione record. Il bundling consente di raggruppare ed elaborare più ordini di cancellazione da parte dei servizi a valle. |
| `action` | Tipo di azione richiesto nell&#39;ordine di lavoro. |
| `createdAt` | La marca temporale in cui è stato creato l’ordine di lavoro. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di lavoro. |
| `operationCount` | Numero di operazioni incluse nell&#39;ordine di lavorazione. |
| `targetServices` | Elenco dei servizi target per l&#39;ordine di lavoro. |
| `status` | Stato corrente dell&#39;ordine di lavoro. I valori possibili sono: `received`,`validated`, `submitted`, `ingested`, `completed` e `failed`. |
| `createdBy` | L’e-mail e l’identificatore dell’utente che ha creato l’ordine di lavoro. |
| `datasetId` | L’identificatore univoco del set di dati associato all’ordine di lavoro. Se la richiesta si applica a tutti i set di dati, questo campo verrà impostato su ALL. |
| `datasetName` | Nome del set di dati associato all’ordine di lavoro. |
| `displayName` | Etichetta leggibile per l&#39;ordine di lavoro. |
| `description` | Descrizione dello scopo dell&#39;ordine di lavorazione. |
| `total` | Numero totale di ordini di lavoro di eliminazione record corrispondenti alla query. |
| `count` | Numero di ordini di lavoro di eliminazione record nella pagina corrente. |
| `_links` | Paginazione e collegamenti di navigazione. |
| `next` | Oggetto con `href` (stringa) e `templated` (booleano) per la pagina successiva. |
| `page` | Oggetto con `href` (stringa) e `templated` (booleano) per la navigazione delle pagine. |

{style="table-layout:auto"}

## Crea un ordine di lavoro di eliminazione record {#create}

Per eliminare i record associati a una o più identità da un singolo set di dati o da tutti i set di dati, effettuare una richiesta POST all&#39;endpoint `/workorder`.

Gli ordini di lavoro vengono elaborati in modo asincrono e vengono visualizzati nell&#39;elenco degli ordini di lavoro dopo l&#39;invio.

>[!TIP]
>
>Ogni ordine di lavoro di eliminazione record inviato tramite l&#39;API può includere fino a **100.000 identità**. Invia quante più identità per richiesta possibile per massimizzare l’efficienza. Evita invii di volumi ridotti, ad esempio ordini di lavoro con ID singolo.

**Formato API**

```http
POST /workorder
```

>[!NOTE]
>
>Puoi eliminare record solo da set di dati il cui schema XDM associato definisce una mappa di identità primaria o di identità.

>[!NOTE]
>
>Se si tenta di creare un ordine di lavoro di eliminazione record per un set di dati con una scadenza già attiva, la richiesta restituisce HTTP 400 (richiesta non valida). Per scadenza attiva si intende qualsiasi eliminazione pianificata non ancora completata.

**Richiesta**

La richiesta seguente elimina tutti i record associati a indirizzi e-mail specifici da un particolare set di dati.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

Nella tabella seguente vengono descritte le proprietà per la creazione di un ordine di lavoro di eliminazione record.

| Proprietà | Descrizione |
| --- | --- |
| `displayName` | Etichetta leggibile per questo ordine di lavoro di eliminazione record. |
| `description` | Descrizione dell&#39;ordine di lavoro di eliminazione record. |
| `action` | Azione richiesta per l&#39;ordine di lavoro di eliminazione record. Per eliminare i record associati a una determinata identità, utilizzare `delete_identity`. |
| `datasetId` | L’identificatore univoco del set di dati. Utilizzare l&#39;ID del set di dati per un set di dati specifico oppure `ALL` per eseguire il targeting di tutti i set di dati. I set di dati devono avere una mappa di identità primaria o di identità. Se esiste una mappa di identità, questa sarà presente come campo di primo livello denominato `identityMap`.<br>Tieni presente che una riga di set di dati può avere molte identità nella mappa delle identità, ma solo una può essere contrassegnata come principale. `"primary": true` deve essere incluso per forzare `id` a corrispondere a un&#39;identità primaria. |
| `namespacesIdentities` | Matrice di oggetti, ciascuno contenente:<br><ul><li> `namespace`: oggetto con una proprietà `code` che specifica lo spazio dei nomi dell&#39;identità (ad esempio, &quot;email&quot;).</li><li> `IDs`: array di valori di identità da eliminare per questo spazio dei nomi.</li></ul>Gli spazi dei nomi di identità forniscono contesto ai dati di identità. Puoi utilizzare gli spazi dei nomi standard forniti da Experience Platform o crearne di personalizzati. Per ulteriori informazioni, consulta la [documentazione sullo spazio dei nomi delle identità](../../identity-service/features/namespaces.md) e la [specifica API del servizio Identity](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del nuovo ordine di lavoro di eliminazione record.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

Nella tabella seguente sono descritte le proprietà della risposta.

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | Identificatore univoco dell&#39;ordine di lavoro di eliminazione record. Usa questo valore per cercare lo stato o i dettagli dell’eliminazione. |
| `orgId` | L’identificatore univoco dell’organizzazione. |
| `bundleId` | Identificatore univoco del bundle contenente questo ordine di lavoro di eliminazione record. Il bundling consente di raggruppare ed elaborare più ordini di cancellazione da parte dei servizi a valle. |
| `action` | Tipo di azione richiesto nell&#39;ordine di lavoro di eliminazione record. |
| `createdAt` | La marca temporale in cui è stato creato l’ordine di lavoro. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di lavoro. |
| `operationCount` | Numero di operazioni incluse nell&#39;ordine di lavorazione. |
| `targetServices` | Elenco dei servizi di destinazione per l&#39;ordine di lavoro di eliminazione record. |
| `status` | Stato corrente dell&#39;ordine di lavoro di eliminazione del record. |
| `createdBy` | Indirizzo e-mail e identificatore dell&#39;utente che ha creato il record elimina l&#39;ordine di lavoro. |
| `datasetId` | L’identificatore univoco del set di dati. Se la richiesta è per tutti i set di dati, il valore sarà impostato su `ALL`. |
| `datasetName` | Nome del set di dati per questo ordine di lavoro di eliminazione record. |
| `displayName` | Etichetta leggibile per l&#39;ordine di lavoro di eliminazione record. |
| `description` | Descrizione dell&#39;ordine di lavoro di eliminazione record. |

{style="table-layout:auto"}

>[!NOTE]
>
>La proprietà azione per gli ordini di lavoro di eliminazione record è attualmente `identity-delete` nelle risposte API. Se l&#39;API cambia per utilizzare un valore diverso (ad esempio `delete_identity`), la documentazione verrà aggiornata di conseguenza.

## Recuperare i dettagli per un ordine di lavoro di eliminazione record specifico {#lookup}

Recuperare le informazioni per un ordine di lavoro di eliminazione record specifico effettuando una richiesta GET a `/workorder/{WORKORDER_ID}`. La risposta include tipo di azione, stato, set di dati e informazioni utente associati e metadati di audit.

**Formato API**

```http
GET /workorder/{WORKORDER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | Identificatore univoco dell&#39;ordine di lavoro di eliminazione record che si sta cercando. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’ordine di lavoro di eliminazione del record specificato.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

Nella tabella seguente sono descritte le proprietà della risposta.

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | Identificatore univoco dell&#39;ordine di lavoro di eliminazione record. |
| `orgId` | Identificatore univoco della tua organizzazione. |
| `bundleId` | Identificatore univoco del bundle contenente questo ordine di lavoro di eliminazione record. Il bundling consente di raggruppare ed elaborare più ordini di cancellazione da parte dei servizi a valle. |
| `action` | Tipo di azione richiesto nell&#39;ordine di lavoro di eliminazione record. |
| `createdAt` | La marca temporale in cui è stato creato l’ordine di lavoro. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di lavoro. |
| `operationCount` | Numero di operazioni incluse nell&#39;ordine di lavorazione. |
| `targetServices` | Elenco dei servizi di destinazione interessati da questo ordine di lavoro di eliminazione record. |
| `status` | Stato corrente dell&#39;ordine di lavoro di eliminazione record. |
| `createdBy` | Indirizzo e-mail e identificatore dell&#39;utente che ha creato il record elimina l&#39;ordine di lavoro. |
| `datasetId` | L’identificatore univoco del set di dati associato all’ordine di lavoro. |
| `datasetName` | Nome del set di dati associato all’ordine di lavoro. |
| `displayName` | Etichetta leggibile per l&#39;ordine di lavoro di eliminazione record. |
| `description` | Descrizione dell&#39;ordine di lavoro di eliminazione record. |

## Aggiornare un ordine di lavoro di eliminazione record

Aggiornare `name` e `description` per un ordine di lavoro di eliminazione record effettuando una richiesta PUT all&#39;endpoint `/workorder/{WORKORDER_ID}`.

**Formato API**

```http
PUT /workorder/{WORKORDER_ID}
```

Nella tabella seguente viene descritto il parametro per questa richiesta.

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | Identificatore univoco dell&#39;ordine di lavoro di eliminazione record che si desidera aggiornare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

Nella tabella seguente sono descritte le proprietà che è possibile aggiornare.

| Proprietà | Descrizione |
| --- | --- |
| `name` | Etichetta leggibile aggiornata per l&#39;ordine di lavoro di eliminazione record. |
| `description` | Descrizione aggiornata per l&#39;ordine di lavoro di eliminazione record. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce la richiesta dell’ordine di lavoro aggiornato.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Proprietà | Descrizione |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | Identificatore univoco dell&#39;ordine di lavoro di eliminazione record. |
| `orgId` | Identificatore univoco della tua organizzazione. |
| `bundleId` | Identificatore univoco del bundle contenente questo ordine di lavoro di eliminazione record. Il bundling consente di raggruppare ed elaborare più ordini di cancellazione da parte dei servizi a valle. |
| `action` | Tipo di azione richiesto nell&#39;ordine di lavoro di eliminazione record. |
| `createdAt` | La marca temporale in cui è stato creato l’ordine di lavoro. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di lavoro. |
| `operationCount` | Numero di operazioni incluse nell&#39;ordine di lavorazione. |
| `targetServices` | Elenco dei servizi di destinazione interessati da questo ordine di lavoro di eliminazione record. |
| `status` | Stato corrente dell&#39;ordine di lavoro di eliminazione record. I valori possibili sono: `received`,`validated`, `submitted`, `ingested`, `completed` e `failed`. |
| `createdBy` | Indirizzo e-mail e identificatore dell&#39;utente che ha creato il record elimina l&#39;ordine di lavoro. |
| `datasetId` | Identificatore univoco del set di dati associato all&#39;ordine di lavoro di eliminazione record. |
| `datasetName` | Nome del set di dati associato all&#39;ordine di lavoro di eliminazione record. |
| `displayName` | Etichetta leggibile per l&#39;ordine di lavoro di eliminazione record. |
| `description` | Descrizione dell&#39;ordine di lavoro di eliminazione record. |
| `productStatusDetails` | Array che elenca lo stato corrente dei processi a valle della richiesta. Ogni oggetto contiene:<ul><li>`productName`: nome del servizio downstream.</li><li>`productStatus`: lo stato di elaborazione corrente dal servizio downstream.</li><li>`createdAt`: la marca temporale in cui il servizio ha pubblicato lo stato più recente.</li></ul>Questa proprietà è disponibile dopo l’invio dell’ordine di lavoro ai servizi a valle per iniziare l’elaborazione. |

{style="table-layout:auto"}
