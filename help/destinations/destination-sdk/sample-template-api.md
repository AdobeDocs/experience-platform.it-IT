---
description: Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando l'endpoint API `/authoring/testing/template/sample`, per ottenere un modello di trasformazione del messaggio di prova per la destinazione.
title: Ottieni operazioni API con modelli di esempio
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Ottieni operazioni API con modelli di esempio {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**Endpoint API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/testing/template/sample` endpoint API, per generare un [modello di trasformazione dei messaggi](./message-format.md#using-templating) per la tua destinazione. Per una descrizione delle funzionalità supportate da questo endpoint, leggere [crea modello](./create-template.md).

## Guida introduttiva alle operazioni API con modelli di esempio {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Ottieni modello di esempio {#generate-sample-template}

Puoi ottenere un modello di esempio effettuando una richiesta di GET al `authoring/testing/template/sample/` e fornisce l&#39;ID di destinazione della configurazione di destinazione in base a cui stai creando il modello.

>[!TIP]
>
>* L&#39;ID di destinazione da utilizzare qui è la variabile `instanceId` che corrisponde a una configurazione di destinazione, creata utilizzando `/destinations` punto finale. Fai riferimento a [riferimento API per la configurazione della destinazione](./destination-configuration-api.md#retrieve-list).


**Formato API**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID della configurazione di destinazione per la quale stai generando un modello di trasformazione del messaggio. |

**Richiesta**

La richiesta seguente genera un nuovo modello di esempio, configurato dai parametri forniti nel payload.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un modello di esempio che è possibile modificare per adattarlo al formato di dati previsto.

Se l&#39;ID di destinazione fornito corrisponde a una configurazione di destinazione con [aggregazione dello sforzo migliore](./destination-configuration.md#best-effort-aggregation) e `maxUsersPerRequest=1` nel criterio di aggregazione, la richiesta restituisce un modello di esempio simile a questo:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Se l&#39;ID di destinazione fornito corrisponde a un modello di server di destinazione con [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) o [aggregazione dello sforzo migliore](./destination-configuration.md#best-effort-aggregation) con `maxUsersPerRequest` maggiore di uno, la richiesta restituisce un modello di esempio simile a questo:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering segments by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come generare un modello di trasformazione del messaggio utilizzando `/authoring/testing/template/sample` Endpoint API. Successivamente, puoi utilizzare il [Endpoint API per modello di rendering](./render-template-api.md) per generare profili esportati in base al modello e confrontarli con il formato dati previsto della destinazione.
