---
title: Relazioni nell’API di Reactor
description: Scopri come vengono stabilite le relazioni tra le risorse nell’API di Reactor, compresi i requisiti di relazione per ogni risorsa.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 99%

---

# Relazioni nell’API di Reactor

Le risorse nell’API di Reactor sono spesso correlate tra loro. Questo documento fornisce una panoramica dell’impostazione delle relazioni tra le risorse nell’API e dei requisiti di relazione per ciascun tipo di risorsa.

A seconda del tipo di risorsa, alcune relazioni sono obbligatorie. Una relazione obbligatoria implica che la risorsa padre non può esistere senza la relazione. Tutte le altre relazioni sono facoltative.

Sia le relazioni obbligatorie che quelle facoltative vengono stabilite automaticamente dal sistema quando vengono create le relative risorse, oppure devono essere create manualmente. Nel caso di creazione manuale, esistono due metodi possibili a seconda della risorsa in questione:

* [Creare tramite payload](#payload)
* [Creare tramite URL](#url) (solo per le librerie)

Per un elenco delle relazioni compatibili per ciascun tipo di risorsa e per i metodi necessari per stabilire le relazioni applicabili, consulta la sezione sui [requisiti delle relazioni](#requirements).

## Creare una relazione tramite payload {#payload}

Alcune relazioni devono essere stabilite manualmente al momento della creazione iniziale di una risorsa. A questo scopo, devi fornire un oggetto `relationship` nel payload della richiesta al momento della creazione della risorsa principale. Esempi di queste relazioni includono:

* [Creazione di un elemento dati](../endpoints/data-elements.md#create) con le estensioni richieste
* [Creazione di un ambiente](../endpoints/environments.md#create) con la relazione host richiesta

**Formato API**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{PROPERTY_ID}` | ID della proprietà a cui appartiene la risorsa. |
| `{RESOURCE_TYPE}` | Tipo di risorsa da creare. |

{style="table-layout:auto"}

**Richiesta**

La seguente richiesta crea un nuovo `rule_component`, stabilendo relazioni con `rules` e una `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `relationships` | Oggetto che deve essere fornito durante la creazione di relazioni tramite payload. Ogni chiave in questo oggetto rappresenta un tipo di relazione specifico. Nell’esempio precedente, sono stabilite le relazioni `extension` e `rules`, che sono specifiche per `rule_components`. Per ulteriori informazioni sui tipi di relazione compatibili per risorse diverse, consulta la sezione sui [requisiti delle relazioni per risorsa](#relationship-requirements-by-resource). |
| `data` | Ogni tipo di relazione fornito sotto l’oggetto `relationship` deve contenere una proprietà `data` che fa riferimento all’`id` e al `type` della risorsa con cui viene stabilita una relazione. Per creare una relazione con più risorse dello stesso tipo, puoi formattare la proprietà `data` come array di oggetti, con ogni oggetto contenente l’`id` e il `type` di una risorsa applicabile. |
| `id` | ID univoco di una risorsa. A ogni `id` deve essere associata una proprietà `type` di pari livello che indica il tipo di risorsa in questione. |
| `type` | Tipo di risorsa a cui fa riferimento un campo `id` di pari livello. I valori accettati sono `data_elements`, `rules`, `extensions` e `environments`. |

{style="table-layout:auto"}

## Creare una relazione tramite URL {#url}

A differenza di altre risorse, le librerie stabiliscono relazioni attraverso i propri endpoint `/relationship` dedicati. Gli esempi includono:

* [Aggiunta di estensioni, elementi dati e regole a una libreria](../endpoints/libraries.md#add-resources)
* [Assegnazione di una libreria a un ambiente](../endpoints/libraries.md#environment)

**Formato API**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{PROPERTY_ID}` | ID della proprietà a cui appartiene la libreria. |
| `{LIBRARY_ID}` | ID della libreria per cui desideri creare una relazione. |
| `{RESOURCE_TYPE}` | Tipo di risorsa di destinazione della relazione. I valori possibili includono `environment`, `data_elements`, `extensions` e `rules`. |

**Richiesta**

La seguente richiesta utilizza l’endpoint `/relationships/environment` di una libreria per creare una relazione con un ambiente.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `data` | Oggetto che fa riferimento all’`id` e al `type` della risorsa di destinazione della relazione. Se vuoi creare una relazione con più risorse dello stesso tipo (ad esempio `extensions` e `rules`), la proprietà `data` deve essere formattata come un array di oggetti, ognuno dei quali deve contenere i valori `id` e `type` della risorsa applicabile. |
| `id` | ID univoco di una risorsa. A ogni `id` deve essere associata una proprietà `type` di pari livello che indica il tipo di risorsa in questione. |
| `type` | Tipo di risorsa a cui fa riferimento un campo `id` di pari livello. I valori accettati sono `data_elements`, `rules`, `extensions` e `environments`. |

{style="table-layout:auto"}

## Requisiti delle relazioni per risorsa {#requirements}

Le tabelle seguenti descrivono le relazioni disponibili per ogni tipo di risorsa, obbligatorie o meno, e il metodo accettato per creare manualmente la relazione applicabile.

>[!NOTE]
>
>Se una relazione non è elencata tra quelle create tramite payload o URL, viene assegnata automaticamente dal sistema.

### Eventi di audit

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### Build

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Callback

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Aziende

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### Elementi dati

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Ambienti

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Estensioni

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Host

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Librerie

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style="table-layout:auto"}

### Note

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### Proprietà

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### Componenti della regola

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### Regole

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### Segreti

| Relazione | Obbligatorio | Creare tramite payload | Creare tramite URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

