---
title: Condivisione di pacchetti di estensione privati nell’API di Reactor
description: Scopri come autorizzare altre aziende a condividere pacchetti di estensione privati nell’API di Reactor.
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---


# Condivisione di pacchetti di estensione privati

>[!NOTE]
>
>Gli utenti con l&#39;autorizzazione `develop_extensions` nell&#39;organizzazione del proprietario del pacchetto di estensione possono creare, elencare ed eliminare le autorizzazioni di utilizzo del pacchetto di estensione per tale pacchetto. Gli utenti di un&#39;organizzazione autorizzata che dispongono dell&#39;autorizzazione `manage_properties` possono elencare le autorizzazioni di utilizzo del pacchetto di estensione solo per la propria organizzazione e aggiornare il proprio stato a `accepted` se desiderano utilizzare il pacchetto di estensione o a `rejected` se non desiderano utilizzarlo.

I proprietari dei pacchetti di estensione possono concedere ad altre aziende l’autorizzazione a utilizzare le loro versioni private tramite l’API di Reactor. A ogni azienda approvata viene concessa una licenza d’uso per un pacchetto di estensione e questa autorizzazione è valida per tutte le versioni private attuali e future del pacchetto.

Questa guida fornisce una panoramica di alto livello su come configurare le autorizzazioni di utilizzo dei pacchetti di estensione. Per istruzioni più dettagliate su come gestire le autorizzazioni nell&#39;API di Reactor, incluso un esempio di JSON della struttura di un&#39;autorizzazione, consulta la [guida dell&#39;endpoint di autorizzazione per l&#39;utilizzo del pacchetto di estensione](../endpoints/extension-package-usage-authorizations.md).

## Creare un’autorizzazione {#create-authorization}

Per creare una nuova autorizzazione, è necessario disporre dell&#39;autorizzazione `develop_extensions`. Nell&#39;esempio seguente viene illustrato come creare un&#39;autorizzazione per l&#39;utilizzo di un pacchetto di estensione per un pacchetto di estensione utilizzando `authorized_org_id` dell&#39;azienda che si desidera autorizzare.

**Formato API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` del pacchetto di estensione per il quale si desidera creare un&#39;autorizzazione. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente crea una nuova autorizzazione del pacchetto di estensione per la società specificata.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes.authorized_org_id` | `ID` dell&#39;organizzazione che si desidera autorizzare. |

{style="table-layout:auto"}

Lo stato iniziale dell&#39;autorizzazione si trova nella fase `pending_approval`. Prima di utilizzare il pacchetto di estensione, l’azienda deve approvare l’autorizzazione. Gli utenti dell’azienda possono sfogliare il pacchetto di estensione privato mentre l’autorizzazione è in attesa di approvazione, ma non sono in grado di installarlo e non possono trovarlo nel catalogo delle estensioni.

## Approvare un’autorizzazione {#approve-authorization}

Per approvare un&#39;autorizzazione, è necessario disporre dei diritti `manage_properties`. In qualità di azienda autorizzata, dovrai inviare una richiesta PATCH all’autorizzazione di utilizzo del pacchetto di estensione, inclusa la `ID` dell’autorizzazione e impostare lo stato su `approved`.

**Formato API**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` dell&#39;autorizzazione che si desidera approvare. |

{style="table-layout:auto"}

**Richiesta**

La seguente richiesta PATCH imposta `state` di un&#39;autorizzazione su `approved`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
	          "state": "approved"
	        },
	        "id": ":extension_package_usage_authorization_id",
	        "type": "extension_package_usage_authorizations"
        }
      }
```

Una volta approvata l’autorizzazione, in qualità di azienda autorizzata, puoi installare il pacchetto di estensione sulle proprietà.

>[!NOTE]
>
>Se l’autorizzazione viene rifiutata, l’azienda autorizzata non potrà utilizzare il pacchetto di estensione.

## Eliminare un’autorizzazione {#delete-authorization}

In qualità di proprietario di un pacchetto di estensione, puoi revocare l’autorizzazione in qualsiasi momento eliminando l’autorizzazione di utilizzo del pacchetto di estensione. Ciò impedirà all’azienda autorizzata di visualizzare versioni private del pacchetto di estensione nel catalogo e di installarlo nelle relative proprietà. Tuttavia, le versioni private già installate continueranno a funzionare come previsto dopo l’eliminazione.

**Formato API**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` dell&#39;autorizzazione che si desidera eliminare. |

{style="table-layout:auto"}

**Richiesta**

La seguente richiesta DELETE rimuove i privilegi di autorizzazione per un’azienda.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
