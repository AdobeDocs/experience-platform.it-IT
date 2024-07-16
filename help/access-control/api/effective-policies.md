---
keywords: Experience Platform;home;argomenti popolari;criteri efficaci;access control api
solution: Experience Platform
title: Endpoint API per criteri effettivi
description: Scopri come visualizzare criteri di accesso efficaci utilizzando l’API di controllo degli accessi per Adobe Experience Platform.
role: Developer
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 2%

---

# Endpoint &quot;effective policies&quot;

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo &quot;amministratore organizzazione&quot; per l’organizzazione richiesta.

Per visualizzare i criteri di controllo di accesso effettivi per l&#39;utente corrente, effettuare una richiesta POST all&#39;endpoint `/acl/effective-policies` nell&#39;API [!DNL Access Control]. Le autorizzazioni e i tipi di risorse che desideri recuperare devono essere forniti nel payload della richiesta sotto forma di un array. Questo è dimostrato nella chiamata API di esempio di seguito.

**Formato API**

```http
POST /acl/effective-policies
```

**Richiesta**

Le richieste seguenti recuperano informazioni sull&#39;autorizzazione &quot;[!UICONTROL Gestisci set di dati]&quot; e l&#39;accesso al tipo di risorsa &quot;[!UICONTROL schemi]&quot; per l&#39;utente corrente.

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
>Per un elenco completo delle autorizzazioni e dei tipi di risorse che possono essere forniti nell&#39;array di payload, vedere la sezione dell&#39;appendice relativa alle [autorizzazioni accettate e ai tipi di risorse](#accepted-permissions-and-resource-types).

**Risposta**

In caso di esito positivo, la risposta restituisce informazioni sulle autorizzazioni e sui tipi di risorse forniti nella richiesta. La risposta include le autorizzazioni attive di cui dispone l’utente corrente per i tipi di risorse specificati nella richiesta. Se le autorizzazioni incluse nel payload della richiesta sono attive per l&#39;utente corrente, l&#39;API restituisce l&#39;autorizzazione con un astrisk (`*`) per indicare che l&#39;autorizzazione è attiva. Tutte le autorizzazioni fornite nella richiesta che non sono attive per l’utente vengono omesse dal payload di risposta.

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

In questo documento viene descritto come effettuare chiamate all&#39;API [!DNL Access Control] per restituire informazioni sulle autorizzazioni attive e sui criteri di accesso correlati per i tipi di risorse. Per ulteriori informazioni sul controllo degli accessi per [!DNL Experience Platform], vedere la [panoramica sul controllo degli accessi](../home.md).

## Appendice

Questa sezione fornisce informazioni supplementari per l&#39;utilizzo dell&#39;API [!DNL Access Control].

### Autorizzazioni accettate e tipi di risorse

Di seguito è riportato un elenco di autorizzazioni e tipi di risorse da includere nel payload di una richiesta POST all&#39;endpoint `/acl/active-permissions`.

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
