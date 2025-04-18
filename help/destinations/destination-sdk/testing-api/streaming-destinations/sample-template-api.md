---
description: Scopri come utilizzare l’API di test di destinazione per generare un modello di trasformazione dei messaggi di test per la destinazione.
title: Genera un esempio di modello di trasformazione dei messaggi
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---


# Genera un esempio di modello di trasformazione dei messaggi {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**Endpoint API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

In questa pagina sono elencate e descritte tutte le operazioni API che è possibile eseguire utilizzando l&#39;endpoint API `/authoring/testing/template/sample` per generare un [modello di trasformazione dei messaggi](../../functionality/destination-server/message-format.md#using-templating) per la destinazione. Per una descrizione delle funzionalità supportate da questo endpoint, leggere [crea modello](create-template.md).

## Guida introduttiva alle operazioni API dei modelli di esempio {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Ottieni modello di esempio {#generate-sample-template}

Per ottenere un modello di esempio, devi eseguire una richiesta GET all&#39;endpoint `authoring/testing/template/sample/` e fornire l&#39;ID di destinazione della configurazione di destinazione in base alla quale stai creando il modello.

>[!TIP]
>
>* L&#39;ID di destinazione da utilizzare è `instanceId` che corrisponde a una configurazione di destinazione, creata utilizzando l&#39;endpoint `/destinations`. Per ulteriori dettagli, consultare [recuperare una configurazione di destinazione](../../authoring-api/destination-configuration/retrieve-destination-configuration.md).

**Formato API**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID della configurazione di destinazione per la quale stai generando un modello di trasformazione dei messaggi. |

**Richiesta**

La richiesta seguente genera un nuovo modello di esempio, configurato dai parametri forniti nel payload.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un modello di esempio modificabile in base al formato di dati previsto.

Se l&#39;ID di destinazione fornito corrisponde a una configurazione di destinazione con [aggregazione della migliore risorsa](../../functionality/destination-configuration/aggregation-policy.md) e `maxUsersPerRequest=1` nel criterio di aggregazione, la richiesta restituisce un modello di esempio simile al seguente:

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
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Se l&#39;ID di destinazione fornito corrisponde a un modello del server di destinazione con [aggregazione configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) o [aggregazione ottimale](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) con `maxUsersPerRequest` maggiore di uno, la richiesta restituisce un modello di esempio simile al seguente:

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
                {#- Alternative syntax for filtering audiences by status: -#}
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

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, sai come generare un modello di trasformazione dei messaggi utilizzando l&#39;endpoint API `/authoring/testing/template/sample`. Successivamente, puoi utilizzare l&#39;endpoint [API del modello di rendering](render-template-api.md) per generare profili esportati in base al modello e confrontarli con il formato di dati previsto della tua destinazione.
