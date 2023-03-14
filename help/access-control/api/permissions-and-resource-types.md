---
keywords: Experience Platform;home;argomenti popolari;autorizzazioni di controllo di accesso;tipi di risorse di controllo di accesso;api di controllo di accesso
solution: Experience Platform
title: Endpoint API di riferimento
description: L’endpoint di riferimento nell’API di controllo degli accessi consente di visualizzare i nomi delle autorizzazioni e dei tipi di risorse disponibili, che possono quindi essere utilizzati per visualizzare criteri di controllo degli accessi efficaci per l’utente corrente.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# Endpoint di riferimento

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo &quot;amministratore organizzazione&quot; per l’organizzazione richiesta.

Per elencare i nomi di tutte le autorizzazioni e di tutti i tipi di risorse, devi effettuare una richiesta GET al `/acl/reference` endpoint. Questi nomi possono quindi essere utilizzati nelle chiamate API a [visualizzare criteri di controllo dell&#39;accesso effettivi](./effective-policies.md) per l&#39;utente corrente.

Un’autorizzazione è un criterio gestito tramite Adobe Admin Console e mappato a zero o più criteri di tipo risorsa. Un tipo di risorsa è un criterio che abilita le funzionalità di lettura, scrittura e/o eliminazione per un tipo specifico di [!DNL Platform] risorse (come set di dati o schemi).

**Formato API**

```http
GET /acl/reference
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

Una risposta corretta restituisce un `permissions` oggetto e un `resource-types` oggetto, ciascuno contenente un elenco completo di nomi rispettivamente per le autorizzazioni di accesso o per i tipi di risorse.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
