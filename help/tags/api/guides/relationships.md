---
title: Relazioni nell'API di Reactor
description: Scopri in che modo le relazioni tra le risorse vengono stabilite nell’API di Reactor, compresi i requisiti di relazione per ogni risorsa.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 10%

---

# Relazioni nell&#39;API di Reactor

Le risorse nell’API di Reactor sono spesso correlate tra loro. Questo documento fornisce una panoramica dell’impostazione delle relazioni tra le risorse nell’API e dei requisiti di relazione di ciascun tipo di risorsa.

A seconda del tipo di risorsa in questione, sono necessarie alcune relazioni. Una relazione obbligatoria implica che la risorsa padre non può esistere senza la relazione. Tutte le altre relazioni sono facoltative.

Indipendentemente dal fatto che siano obbligatori o facoltativi, le relazioni vengono stabilite automaticamente dal sistema al momento della creazione delle relative risorse, oppure devono essere create manualmente. Nel caso di creazione manuale di relazioni, esistono due metodi possibili a seconda della risorsa in questione:

* [Crea per payload](#payload)
* [Crea per URL](#url)  (solo per le librerie)

Fai riferimento alla sezione sui [requisiti di relazione](#requirements) per un elenco delle relazioni compatibili per ciascun tipo di risorsa e ai metodi necessari per stabilire tali relazioni, se applicabile.

## Creare una relazione per payload {#payload}

Alcune relazioni devono essere stabilite manualmente al momento della creazione iniziale di una risorsa. A questo scopo, devi fornire un oggetto `relationship` nel payload della richiesta al momento della creazione della risorsa principale. Esempi di queste relazioni includono:

* [Creazione di un ](../endpoints/data-elements.md#create) elemento dati con le estensioni richieste
* [Creazione di un ](../endpoints/environments.md#create) ambiente con la relazione host richiesta

**Formato API**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{PROPERTY_ID}` | ID della proprietà a cui appartiene la risorsa. |
| `{RESOURCE_TYPE}` | Tipo di risorsa da creare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta crea un nuovo `rule_component`, stabilendo relazioni con `rules` e un `extension`.

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
| `relationships` | Un oggetto che deve essere fornito durante la creazione di relazioni per payload. Ogni chiave in questo oggetto rappresenta un tipo di relazione specifico. Nell&#39;esempio precedente, sono stabilite le relazioni `extension` e `rules`, che sono particolari per `rule_components`. Per ulteriori informazioni sui tipi di relazione compatibili per risorse diverse, consulta la sezione sui [requisiti di relazione per risorsa](#relationship-requirements-by-resource). |
| `data` | Ogni tipo di relazione fornito sotto l&#39;oggetto `relationship` deve contenere una proprietà `data` che fa riferimento a `id` e `type` della risorsa con cui viene stabilita una relazione. È possibile creare una relazione con più risorse dello stesso tipo formattando la proprietà `data` come array di oggetti, con ogni oggetto contenente le risorse `id` e `type` di una risorsa applicabile. |
| `id` | ID univoco di una risorsa. A ogni `id` deve essere associata una proprietà di pari livello `type` che indica il tipo di risorsa in questione. |
| `type` | Il tipo di risorsa a cui fa riferimento un campo di pari livello `id`. I valori accettati includono `data_elements`, `rules`, `extensions` e `environments`. |

{style=&quot;table-layout:auto&quot;}

## Creare una relazione per URL {#url}

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
| `{RESOURCE_TYPE}` | Il tipo di risorsa di destinazione della relazione. I valori disponibili sono `environment`, `data_elements`, `extensions` e `rules`. |

**Richiesta**

La richiesta seguente utilizza l&#39;endpoint `/relationships/environment` di una libreria per creare una relazione con un ambiente.

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
| `data` | Un oggetto che fa riferimento alle `id` e `type` della risorsa di destinazione per la relazione. Se si sta creando una relazione con più risorse dello stesso tipo (ad esempio `extensions` e `rules`), la proprietà `data` deve essere formattata come una matrice di oggetti, con ogni oggetto contenente i valori `id` e `type` di una risorsa applicabile. |
| `id` | ID univoco di una risorsa. A ogni `id` deve essere associata una proprietà di pari livello `type` che indica il tipo di risorsa in questione. |
| `type` | Il tipo di risorsa a cui fa riferimento un campo di pari livello `id`. I valori accettati includono `data_elements`, `rules`, `extensions` e `environments`. |

{style=&quot;table-layout:auto&quot;}

## Requisiti di relazione per risorsa {#requirements}

Le tabelle seguenti descrivono le relazioni disponibili per ogni tipo di risorsa, indipendentemente dal fatto che tali relazioni siano necessarie o meno, e il metodo accettato per creare manualmente la relazione, se applicabile.

>[!NOTE]
>
>Se una relazione non è elencata come creata dal payload o dall’URL, viene assegnata automaticamente dal sistema.

### Eventi di controllo

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `property` | . |  |  |
| `entity` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Build

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | . |  |  |
| `library` | . |  |  |
| `property` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Callback

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `property` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Aziende

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Elementi dati

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | . |  |  |
| `notes` |  |  |  |
| `property` | . |  |  |
| `origin` | . |  |  |
| `extension` | . | . |  |
| `updated_with_extension` | . |  |  |
| `updated_with_extension_package` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Ambienti

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | . | . |  |
| `property` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Estensioni

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | . |  |  |
| `notes` |  |  |  |
| `property` | . |  |  |
| `origin` | . |  |  |
| `extension_package` | . | . |  |
| `updated_with_extension_package` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Host

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `property` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Librerie

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | . |
| `data_elements` |  |  | . |
| `extensions` |  |  | . |
| `rules` |  |  | . |
| `notes` |  |  |  |
| `upstream_library` | . |  |  |
| `property` | . |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Note

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `resource` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Proprietà

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `company` | . |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Componenti della regola

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | . |  |  |
| `updated_with_extension` | . |  |  |
| `extension` | . | . |  |
| `notes` |  |  |  |
| `origin` | . |  |  |
| `property` | . |  |  |
| `rules` | . | . |  |
| `revisions` | . |  |  |

{style=&quot;table-layout:auto&quot;}

### Regole

| Relazione | Obbligatorio | Crea per payload | Crea per URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | . |  |  |
| `notes` |  |  |  |
| `property` | . |  |  |
| `origin` | . |  |  |
| `rule_components` |  |  |  |
