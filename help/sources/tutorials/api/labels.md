---
title: Applicare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati delle origini utilizzando l’API
description: Scopri come utilizzare l’API del servizio Flusso per applicare le etichette di accesso e gestire l’accesso degli utenti ai flussi di dati delle origini.
exl-id: 572d6838-3e4c-4fd5-89fa-32cad6280325
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# Applicare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati delle origini utilizzando l’API

Puoi utilizzare le funzionalità fornite da [controllo dell&#39;accesso basato su attributi](../../../access-control/abac/overview.md) in Real-Time CDP per applicare le etichette ai flussi di dati di origine. Con questa funzione, puoi garantire che solo un sottoinsieme di utenti dell’organizzazione abbia accesso a flussi di dati di origini specifici.

Quando aggiungi un’etichetta di accesso a un particolare flusso di dati, solo gli utenti che hanno accesso a un ruolo a cui è assegnata tale etichetta possono visualizzare e modificare tale flusso di dati. Se un flusso di dati di origine non è contrassegnato con alcuna etichetta, è visibile a tutti gli utenti appartenenti alla tua organizzazione. Ad esempio, se applichi l’etichetta C12 a un flusso di dati, gli utenti assegnati a un ruolo che non dispone dell’etichetta C12 non potranno visualizzare e modificare il flusso di dati con l’etichetta C12.

Leggi questa guida per informazioni su come applicare etichette di accesso ai flussi di dati di origine utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Prima di utilizzare le etichette di controllo degli accessi, è necessario conoscere le funzionalità del controllo degli accessi basato su attributi. Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sul controllo degli accessi basato su attributi](../../../access-control/abac/overview.md)
* [Guida end-to-end al controllo degli accessi basato su attributi](../../../access-control/abac/end-to-end-guide.md)
* [Guida API per il controllo degli accessi basato su attributi](../../../access-control/abac/api/overview.md)
* [Glossario delle etichette di utilizzo dei dati](../../../data-governance/labels/reference.md)

## Applica etichette di accesso ai flussi di dati di origine

>[!NOTE]
>
>* Non è possibile applicare etichette a un’esecuzione di flusso. Tuttavia, le esecuzioni di flusso ereditano le etichette applicate al flusso di dati principale.
>
>* Se non disponi dell’accesso di visualizzazione a un flusso di dati, non potrai visualizzare anche le relative esecuzioni di flusso.

Per aggiungere un&#39;etichetta a un flusso di dati, effettua una richiesta PATCH all&#39;endpoint `/flows` e fornisci l&#39;ID del flusso di dati da aggiornare.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{FLOW_ID}` | ID del flusso di dati che desideri aggiornare. |

**Richiesta**

>[!TIP]
>
>Per effettuare una richiesta PATCH, fornisci la versione/etag del flusso di dati che desideri aggiornare come parametro di intestazione `if-match`.

La richiesta seguente aggiunge l&#39;etichetta C12 al flusso di dati con ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Parte del flusso di dati da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare la proprietà. |



**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. È possibile verificare l&#39;aggiornamento effettuando una richiesta GET all&#39;API [!DNL Flow Service] e fornendo il proprio ID di flusso.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Dopo aver configurato correttamente le etichette di accesso al flusso di dati, qualsiasi utente che non ha accesso a tale etichetta non sarà più in grado di recuperare il flusso di dati. Ad esempio, se un utente che non dispone del provisioning con l&#39;etichetta C12 effettua una richiesta GET per recuperare un flusso di dati con ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`, riceverà la seguente risposta:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

Analogamente, gli utenti che non hanno accesso all’etichetta C12 non saranno in grado di effettuare richieste PATCH o DELETE rispetto al flusso di dati aggiornato e riceveranno la seguente risposta:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Passaggi successivi

Ora sai come applicare le etichette di accesso ai flussi di dati di origine. Ora puoi garantire che solo un gruppo specifico di utenti dell’organizzazione possa accedere a determinati flussi di dati di origini. Per ulteriori informazioni, consulta la seguente documentazione:

* [Applicare le etichette di accesso ai flussi di dati di origine nell’interfaccia utente](../ui/labels.md)
* [Panoramica sul controllo degli accessi](../../../access-control/home.md)
