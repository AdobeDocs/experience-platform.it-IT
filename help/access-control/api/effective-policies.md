---
keywords: Experience Platform;home;argomenti popolari;criteri efficaci;api di controllo accessi
solution: Experience Platform
title: Endpoint API per criteri efficaci
description: Scopri come visualizzare i criteri di accesso effettivi utilizzando l’API di controllo accessi per Adobe Experience Platform.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 2%

---

# Endpoint criteri efficaci

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo di amministratore organizzazione per l’organizzazione richiesta.

Per visualizzare i criteri di controllo degli accessi efficaci per l’utente corrente, invia una richiesta POST al `/acl/effective-policies` punto finale [!DNL Access Control] API. Le autorizzazioni e i tipi di risorse che si desidera recuperare devono essere forniti nel payload della richiesta sotto forma di array. Questo è dimostrato nell’esempio di chiamata API di seguito.

**Formato API**

```http
POST /acl/effective-policies
```

**Richiesta**

Le seguenti richieste recuperano informazioni sul &quot;[!UICONTROL Gestire i set di dati]&quot; autorizzazione e accesso al &quot;[!UICONTROL schemi]&quot; tipo di risorsa per l&#39;utente corrente.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Per un elenco completo delle autorizzazioni e dei tipi di risorse che possono essere forniti nell’array di payload, consulta la sezione appendice su [autorizzazioni accettate e tipi di risorse](#accepted-permissions-and-resource-types).

**Risposta**

Una risposta corretta restituisce informazioni sulle autorizzazioni e sui tipi di risorse forniti nella richiesta. La risposta include le autorizzazioni attive dell&#39;utente corrente per i tipi di risorse specificati nella richiesta. Se le autorizzazioni incluse nel payload della richiesta sono attive per l’utente corrente, l’API restituisce l’autorizzazione con un asterisco (`*`) per indicare che l’autorizzazione è attiva. Eventuali autorizzazioni fornite nella richiesta che non sono attive per l’utente vengono omesse dal payload della risposta.

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

Questo documento illustra come effettuare chiamate al [!DNL Access Control] API per restituire informazioni sulle autorizzazioni attive e i relativi criteri di accesso per i tipi di risorse. Per ulteriori informazioni sul controllo degli accessi per [!DNL Experience Platform], vedi [panoramica sul controllo degli accessi](../home.md).

## Appendice

Questa sezione fornisce informazioni supplementari per l’utilizzo del [!DNL Access Control] API.

### Autorizzazioni accettate e tipi di risorse

Di seguito è riportato un elenco di autorizzazioni e tipi di risorse che è possibile includere nel payload di una richiesta di POST per `/acl/active-permissions` punto finale.

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
