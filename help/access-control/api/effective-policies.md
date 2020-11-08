---
keywords: Experience Platform;home;popular topics;effective policies;access control api
solution: Experience Platform
title: Visualizza criteri efficaci
topic: developer guide
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per diverse funzionalità della piattaforma utilizzando l'Adobe Admin Console. Questo documento funge da guida per la visualizzazione dei criteri effettivi tramite l'API di controllo degli accessi per Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 481f093e52c8533d2919504051af9e63704a0f4a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Visualizza criteri efficaci

Per visualizzare i criteri effettivi per l&#39;utente corrente, effettuate una richiesta di POST all&#39; `/acl/effective-policies` endpoint nell&#39; [!DNL Access Control] API. Le autorizzazioni e i tipi di risorse che si desidera recuperare devono essere forniti nel payload della richiesta sotto forma di array. Questo è dimostrato nella chiamata API di esempio riportata di seguito.

**Formato API**

```http
POST /acl/effective-policies
```

**Richiesta**

Le seguenti richieste recuperano informazioni sull&#39;autorizzazione &quot;[!UICONTROL Manage Datasets]&quot; e l&#39;accesso al tipo di risorsa &quot;[!UICONTROL schemas]&quot; per l&#39;utente corrente.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Per un elenco completo delle autorizzazioni e dei tipi di risorse che possono essere forniti nell&#39;array di payload, consultate la sezione appendice sulle autorizzazioni e i tipi [di risorse](#accepted-permissions-and-resource-types)accettati.

**Risposta**

Una risposta corretta restituisce informazioni sulle autorizzazioni e i tipi di risorse forniti nella richiesta. La risposta include le autorizzazioni attive dell&#39;utente corrente per i tipi di risorse specificati nella richiesta. Se le autorizzazioni incluse nel payload della richiesta sono attive per l&#39;utente corrente, l&#39;API restituisce l&#39;autorizzazione con un asterisco (`*`) per indicare che l&#39;autorizzazione è attiva. Eventuali autorizzazioni fornite nella richiesta che non sono attive per l&#39;utente vengono omesse dal payload della risposta.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Passaggi successivi

In questo documento è stato illustrato come effettuare chiamate all&#39; [!DNL Access Control] API per restituire informazioni sulle autorizzazioni attive e sui criteri correlati per i tipi di risorse. Per ulteriori informazioni sul controllo degli accessi per [!DNL Experience Platform], consultate la panoramica [sul controllo](../home.md)degli accessi.

## Appendice

Questa sezione fornisce informazioni supplementari per l&#39;utilizzo dell&#39; [!DNL Access Control] API.

### Autorizzazioni accettate e tipi di risorse

Di seguito è riportato un elenco di autorizzazioni e tipi di risorse che potete includere nel payload di una richiesta di POST all&#39; `/acl/active-permissions` endpoint.

**Autorizzazioni**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schema-identities
permissions/manage-schema-relationships
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**Tipi di risorse**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
