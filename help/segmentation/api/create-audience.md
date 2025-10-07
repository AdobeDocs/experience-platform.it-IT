---
title: Crea endpoint API per pubblico
description: Scopri come creare i metadati per un pubblico esterno utilizzando l’API.
hide: true
hidefromtoc: true
exl-id: e841a5f6-f406-4e1d-9e8a-acb861ba6587
source-git-commit: bf90b09693c7b9b7d3ad6ccc6940d255bf7bf4cb
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 7%

---

# Crea endpoint di pubblico

È possibile utilizzare l&#39;endpoint POST `/audiences` per creare i metadati per un pubblico esterno, in modo che il pubblico sia visibile in Audience Portal. Utilizza questo endpoint se l’acquisizione del pubblico verrà gestita in un servizio separato, ad esempio l’acquisizione batch.

## Introduzione

>[!IMPORTANT]
>
>Gli endpoint in questa guida hanno il prefisso `/core/ais`, invece di `/core/ups`.

Per utilizzare le API di Experience Platform, è necessario aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Experience Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consulta la [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

**Formato API**

>[!IMPORTANT]
>
>**devi** includere il parametro di query `createAudienceMetaOnly=true` come parte della richiesta.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Richiesta**

>[!IMPORTANT]
>
>**devi** includere l&#39;intestazione `Accept: application/vnd.adobe.external.audiences+json; version=2` come parte della richiesta API.

```shell
curl -X POST https://platform.adobe.io/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `name` | Stringa | Il nome del pubblico. |
| `description` | Stringa | Una descrizione facoltativa per il pubblico. |
| `namespace` | Stringa | Lo spazio dei nomi per il pubblico. |
| `originName` | Stringa | Il nome dell’origine del pubblico. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sul pubblico appena creato.

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `name` | Stringa | Il nome del pubblico creato. |
| `audienceId` | Stringa | ID del pubblico creato. |
