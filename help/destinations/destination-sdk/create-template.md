---
description: Come parte di Destination SDK, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come creare e testare un modello di trasformazione dei messaggi.
title: Creare e testare un modello di trasformazione dei messaggi
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Creare e testare un modello di trasformazione dei messaggi {#create-template}

## Panoramica {#overview}

Come parte di Destination SDK, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come creare e testare un modello di trasformazione dei messaggi. Per informazioni su come verificare la destinazione, leggi [Verifica la configurazione di destinazione](./test-destination.md).

A **creare e testare un modello di trasformazione dei messaggi** tra lo schema di destinazione in Adobe Experience Platform e il formato di messaggio supportato dalla destinazione, utilizza *Strumento di authoring dei modelli* descritti più avanti.  Ulteriori informazioni sulla trasformazione dei dati tra lo schema di origine e di destinazione in [documento formato messaggio](./message-format.md#using-templating).

Di seguito è illustrato il modo in cui la creazione e il test di un modello di trasformazione dei messaggi si adattano al [flusso di lavoro di configurazione della destinazione](./configure-destination-instructions.md) nella Destination SDK:

![Immagine di dove il passaggio Crea modello si inserisce nel flusso di lavoro di configurazione di destinazione](./assets/create-template-step.png)

## Perché è necessario creare e testare un modello di trasformazione dei messaggi {#why-create-message-transformation-template}

Uno dei primi passaggi nella creazione della destinazione in Destination SDK consiste nel pensare a come il formato dati per l’iscrizione ai segmenti, le identità e gli attributi di profilo viene trasformato quando viene esportato da Adobe Experience Platform alla destinazione. Trova informazioni sulla trasformazione tra lo schema XDM di Adobe e lo schema di destinazione in [documento formato messaggio](./message-format.md#using-templating).

Affinché la trasformazione venga eseguita correttamente, è necessario fornire un modello di trasformazione simile al seguente esempio: [Creare un modello che invia segmenti, identità e attributi di profilo](./message-format.md#segments-identities-attributes).

Adobe fornisce uno strumento per modelli che consente di creare e testare il modello di messaggio che trasforma i dati dal formato XDM di Adobe nel formato supportato dalla destinazione. Lo strumento dispone di due endpoint API che puoi utilizzare:
* Utilizza il *API modello di esempio* per ottenere un modello di esempio.
* Utilizza il *API modello di rendering* per eseguire il rendering del modello di esempio in modo da poter confrontare il risultato con il formato di dati previsto della destinazione. Dopo aver confrontato i dati esportati con il formato dati previsto dalla destinazione, puoi modificare il modello. In questo modo, i dati esportati generati corrisponderanno al formato dati previsto dalla destinazione.

## Passaggi da completare prima di creare il modello {#prerequisites}

Prima di creare il modello, assicurati di completare i passaggi seguenti:

1. [Creare una configurazione del server di destinazione](./destination-server-api.md). Il modello che verrà generato è diverso in base al valore fornito per `maxUsersPerRequest` parametro.
   * Utilizzare `maxUsersPerRequest=1` se desideri che una chiamata API alla destinazione includa un singolo profilo, insieme alle relative qualifiche del segmento, identità e attributi di profilo.
   * Utilizzare `maxUsersPerRequest` con un valore maggiore di uno se desideri che una chiamata API alla destinazione includa più profili, insieme alle relative qualifiche dei segmenti, identità e attributi di profilo.
2. [Creare una configurazione di destinazione](./destination-configuration-api.md#create) e aggiungi l’ID della configurazione del server di destinazione in `destinationDelivery.destinationServerId`.
3. [Ottieni l’ID della configurazione di destinazione](./destination-configuration-api.md#retrieve-list) che hai appena creato, in modo da poterlo utilizzare nello strumento di creazione del modello.
4. Comprendere [quali funzioni e filtri è possibile utilizzare](./supported-functions.md) nel modello di trasformazione dei messaggi.

## Utilizzare l’API modello di esempio e l’API modello di rendering per creare un modello per la destinazione {#iterative-process}

>[!TIP]
>
>Prima di creare e modificare il modello di trasformazione del messaggio, puoi iniziare chiamando il [endpoint API del modello di rendering](./render-template-api.md#render-exported-data) con un semplice modello che esporta i profili non elaborati senza applicare alcuna trasformazione. La sintassi del modello semplice è la seguente: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Il processo per ottenere e testare il modello è iterativo. Ripeti i passaggi seguenti fino a quando i profili esportati non corrispondono al formato di dati previsto della destinazione.

1. In primo luogo, [ottenere un modello di esempio](./create-template.md#sample-template-api).
2. Utilizza il modello di esempio come punto di partenza per creare una bozza personalizzata.
3. Chiama il [endpoint API del modello di rendering](./create-template.md#render-template-api) con il tuo modello. Adobe genera profili di esempio in base allo schema e restituisce il risultato o eventuali errori riscontrati.
4. Confronta i dati esportati con il formato dati previsto dalla destinazione. Se necessario, modifica il modello.
5. Ripeti questo processo fino a quando i profili esportati non corrispondono al formato di dati previsto della destinazione.

## Ottenere un modello di esempio utilizzando l’API del modello di esempio {#sample-template-api}

>[!NOTE]
>
>Per la documentazione di riferimento completa sulle API, leggi [Ottieni operazioni API modello di esempio](./sample-template-api.md).

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

Se l’ID di destinazione fornito corrisponde a una configurazione di destinazione con [aggregazione della migliore fatica](./destination-configuration.md#best-effort-aggregation) e `maxUsersPerRequest=1` nel criterio di aggregazione, la richiesta restituisce un modello di esempio simile al seguente:

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

Se l’ID di destinazione fornito corrisponde a un modello di server di destinazione con [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) o [aggregazione della migliore fatica](./destination-configuration.md#best-effort-aggregation) con `maxUsersPerRequest` maggiore di uno, la richiesta restituisce un modello di esempio simile a questo:

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

## Carattere-escape per il modello {#character-escape-template}

Prima di utilizzare il modello per eseguire il rendering di profili che corrispondono al formato previsto della destinazione, è necessario eseguire l’escape carattere del modello, come illustrato nella registrazione schermata seguente.

![Video che mostra come applicare l’escape carattere a un modello utilizzando uno strumento online per l’escape carattere](./assets/escape-characters.gif)

È possibile utilizzare uno strumento di escape di caratteri online. La demo precedente utilizza [Formattatore di escape JSON](https://jsonformatter.org/json-escape).

## Rendering dell’API modello {#render-template-api}

Dopo aver creato un modello di trasformazione dei messaggi utilizzando [API modello di esempio](./create-template.md#sample-template-api), è possibile [eseguire il rendering del modello](./render-template-api.md) per generare i dati esportati in base ad essi. Questo ti consente di verificare se i profili che Adobe Experience Platform esporterebbe nella destinazione corrispondono al formato previsto della destinazione.

Per esempi di chiamate che puoi effettuare, consulta il riferimento API:

* [Rendering di un modello senza profili inviati nel corpo](./render-template-api.md#multiple-profiles-no-body)
* [Eseguire il rendering di un modello con i profili inviati nel corpo](./render-template-api.md#multiple-profiles-with-body)

Modifica il modello ed effettua chiamate all’endpoint API del modello di rendering fino a quando i profili esportati non corrispondono al formato di dati previsto della destinazione.

## Aggiungere il modello con escape di caratteri alla configurazione del server di destinazione

Una volta che sei soddisfatto del modello di trasformazione del messaggio, aggiungilo al [configurazione del server di destinazione](./server-and-template-configuration.md), in `httpTemplate.requestBody.value`.
