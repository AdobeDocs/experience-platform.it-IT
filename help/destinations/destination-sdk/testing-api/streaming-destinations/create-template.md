---
description: Scopri come utilizzare l’API di test di destinazione per testare il modello di trasformazione dei messaggi di destinazione in streaming prima di pubblicare la destinazione.
title: Creare e testare un modello di trasformazione dei messaggi
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Creare e testare un modello di trasformazione dei messaggi {#create-template}

## Panoramica {#overview}

Come parte di Destination SDK, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come creare e testare un modello di trasformazione dei messaggi. Per informazioni su come verificare la destinazione, leggere [Verifica la configurazione di destinazione](streaming-destination-testing-overview.md).

Per **creare e testare un modello di trasformazione dei messaggi** tra lo schema di destinazione in Adobe Experience Platform e il formato di messaggio supportato dalla destinazione, utilizzare lo *strumento di creazione dei modelli* descritto di seguito.  Ulteriori informazioni sulla trasformazione dei dati tra lo schema di origine e di destinazione nel documento [formato messaggio](../../functionality/destination-server/message-format.md#using-templating).

Di seguito è illustrato il modo in cui la creazione e il test di un modello di trasformazione dei messaggi si adattano al [flusso di lavoro di configurazione di destinazione](../../guides/configure-destination-instructions.md) in Destination SDK:

![Immagine di dove il passaggio di creazione del modello si inserisce nel flusso di lavoro di configurazione di destinazione](../../assets/testing-api/create-template-step.png)

## Perché è necessario creare e testare un modello di trasformazione dei messaggi {#why-create-message-transformation-template}

Uno dei primi passaggi nella creazione della destinazione in Destination SDK consiste nel pensare a come il formato dei dati per l’iscrizione al pubblico, le identità e gli attributi di profilo viene trasformato quando si esporta da Adobe Experience Platform alla destinazione. Trova informazioni sulla trasformazione tra lo schema XDM Adobe e lo schema di destinazione nel [documento in formato messaggio](../../functionality/destination-server/message-format.md#using-templating).

Affinché la trasformazione venga eseguita correttamente, è necessario fornire un modello di trasformazione simile a questo esempio: [Creare un modello che invia segmenti, identità e attributi di profilo](../../functionality/destination-server/message-format.md#segments-identities-attributes).

Adobe fornisce uno strumento per modelli che consente di creare e testare il modello di messaggio che trasforma i dati dal formato XDM di Adobe nel formato supportato dalla destinazione. Lo strumento dispone di due endpoint API che puoi utilizzare:

* Utilizza *API modello di esempio* per ottenere un modello di esempio.
* Utilizza l&#39;*API modello di rendering* per eseguire il rendering del modello di esempio in modo da confrontare il risultato con il formato di dati previsto della tua destinazione. Dopo aver confrontato i dati esportati con il formato dati previsto dalla destinazione, puoi modificare il modello. In questo modo, i dati esportati generati corrisponderanno al formato dati previsto dalla destinazione.

## Passaggi da completare prima di creare il modello {#prerequisites}

Prima di creare il modello, assicurati di completare i passaggi seguenti:

1. [Crea una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Il modello che verrà generato è diverso in base al valore fornito per il parametro `maxUsersPerRequest`.
   * Utilizza `maxUsersPerRequest=1` se vuoi che una chiamata API alla tua destinazione includa un singolo profilo, insieme alle sue qualifiche di pubblico, identità e attributi di profilo.
   * Utilizza `maxUsersPerRequest` con un valore maggiore di uno se desideri che una chiamata API alla tua destinazione includa più profili, insieme alle loro qualifiche di pubblico, identità e attributi di profilo.
2. [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) e aggiungere l&#39;ID della configurazione del server di destinazione in `destinationDelivery.destinationServerId`.
3. [Ottieni l&#39;ID della configurazione di destinazione](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) appena creata, in modo da poterlo utilizzare nello strumento di creazione del modello.
4. Comprendere [quali funzioni e filtri è possibile utilizzare](../../functionality/destination-server/supported-functions.md) nel modello di trasformazione dei messaggi.

## Utilizzare l’API modello di esempio e l’API modello di rendering per creare un modello per la destinazione {#iterative-process}

>[!TIP]
>
>Prima di creare e modificare il modello di trasformazione dei messaggi, è possibile iniziare chiamando l&#39;[endpoint API del modello di rendering](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) con un semplice modello che esporta i profili non elaborati senza applicare alcuna trasformazione. Sintassi del modello semplice: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Il processo per ottenere e testare il modello è iterativo. Ripeti i passaggi seguenti fino a quando i profili esportati non corrispondono al formato di dati previsto della destinazione.

1. [ottenere un modello di esempio](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. Utilizza il modello di esempio come punto di partenza per creare una bozza personalizzata.
3. Chiama l&#39;endpoint API del modello di rendering [&#128279;](../../testing-api/streaming-destinations/create-template.md#render-template-api) con il tuo modello. Adobe genera profili di esempio in base allo schema e restituisce il risultato o eventuali errori riscontrati.
4. Confronta i dati esportati con il formato dati previsto dalla destinazione. Se necessario, modifica il modello.
5. Ripeti questo processo fino a quando i profili esportati non corrispondono al formato di dati previsto della destinazione.

## Ottenere un modello di esempio utilizzando l’API del modello di esempio {#sample-template-api}

>[!NOTE]
>
>Per la documentazione completa di riferimento sulle API, leggere [Operazioni per ottenere un modello di esempio per le API](../../testing-api/streaming-destinations/sample-template-api.md).

Aggiungi un ID di destinazione alla chiamata, come mostrato di seguito, e la risposta restituirà un esempio di modello corrispondente all’ID di destinazione.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Se l&#39;ID di destinazione fornito corrisponde a una configurazione di destinazione con [aggregazione della migliore risorsa](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) e `maxUsersPerRequest=1` nel criterio di aggregazione, la richiesta restituisce un modello di esempio simile al seguente:

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

## Carattere-escape per il modello {#character-escape-template}

Prima di utilizzare il modello per eseguire il rendering di profili che corrispondono al formato previsto della destinazione, è necessario eseguire l’escape carattere del modello, come illustrato nella registrazione schermata seguente.

![Video che mostra come eseguire l&#39;escape dei caratteri in un modello utilizzando uno strumento di escape dei caratteri in linea](../../assets/testing-api/escape-characters.gif)

È possibile utilizzare uno strumento di escape di caratteri online. La demo precedente utilizza il formattatore di escape [JSON](https://jsonformatter.org/json-escape).

## Rendering dell’API modello {#render-template-api}

Dopo aver creato un modello di trasformazione dei messaggi utilizzando l&#39;[API modello di esempio](create-template.md#sample-template-api), puoi [eseguire il rendering del modello](render-template-api.md) per generare i dati esportati in base a esso. Questo ti consente di verificare se i profili che Adobe Experience Platform esporterebbe nella destinazione corrispondono al formato previsto della destinazione.

Per esempi di chiamate che puoi effettuare, consulta il riferimento API:

* [Rendering di un modello senza profili inviati nel corpo](render-template-api.md#multiple-profiles-no-body)
* [Eseguire il rendering di un modello con i profili inviati nel corpo](render-template-api.md#multiple-profiles-with-body)

Modifica il modello ed effettua chiamate all’endpoint API del modello di rendering fino a quando i profili esportati non corrispondono al formato di dati previsto della destinazione.

## Aggiungere il modello con escape di caratteri alla configurazione del server di destinazione

Una volta ottenuto il modello di trasformazione del messaggio, aggiungerlo alla [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md), in `httpTemplate.requestBody.value`.
