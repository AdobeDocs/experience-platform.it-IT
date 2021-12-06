---
description: Come parte di Destination SDK, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come creare e testare un modello di trasformazione dei messaggi.
title: Creare e testare un modello di trasformazione dei messaggi
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: aa5898369d41ba48a1416a0b4ea82f6345333d18
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Creare e testare un modello di trasformazione dei messaggi {#create-template}

## Panoramica {#overview}

Come parte di Destination SDK, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come creare e testare un modello di trasformazione dei messaggi. Per informazioni su come verificare la destinazione, consulta [Verifica la configurazione di destinazione](./test-destination.md).

A **creare e testare un modello di trasformazione dei messaggi** tra lo schema di destinazione in Adobe Experience Platform e il formato del messaggio supportato dalla destinazione, utilizza *Strumento per la creazione di modelli* descritto più avanti.  Ulteriori informazioni sulla trasformazione dei dati tra lo schema di origine e di destinazione nel [documento con formato messaggio](./message-format.md#using-templating).

Di seguito è illustrato come creare e testare un modello di trasformazione dei messaggi si adatta all’interno di [flusso di lavoro di configurazione della destinazione](./configure-destination-instructions.md) in Destination SDK:

![Grafico in cui il passaggio crea modello si inserisce nel flusso di lavoro di configurazione della destinazione](./assets/create-template-step.png)

## Perché è necessario creare e testare un modello di trasformazione dei messaggi {#why-create-message-transformation-template}

Uno dei primi passi nella creazione della destinazione in Destination SDK è pensare a come il formato dei dati per l’appartenenza al segmento, le identità e gli attributi di profilo viene trasformato quando si esporta da Adobe Experience Platform alla destinazione. Trova informazioni sulla trasformazione tra lo schema XDM di Adobe e lo schema di destinazione nel [documento con formato messaggio](./message-format.md#using-templating).

Affinché la trasformazione abbia successo, è necessario fornire un modello di trasformazione, simile a questo esempio: [Creare un modello che invia segmenti, identità e attributi di profilo](./message-format.md#segments-identities-attributes).

Adobe fornisce uno strumento modello che ti consente di creare e testare il modello di messaggio che trasforma i dati dal formato Adobe XDM nel formato supportato dalla tua destinazione. Lo strumento dispone di due endpoint API che puoi utilizzare:
* Utilizza la *API modello di esempio* per ottenere un modello di esempio.
* Utilizza la *API del modello di rendering* per eseguire il rendering del modello di esempio in modo da poter confrontare il risultato rispetto al formato dati previsto per la destinazione. Dopo aver confrontato i dati esportati con il formato di dati previsto dalla destinazione, puoi modificare il modello. In questo modo, i dati esportati generati corrispondono al formato di dati previsto dalla destinazione.

## Passaggi da completare prima di creare il modello {#prerequisites}

Prima di essere pronti per creare il modello, assicurati di completare i passaggi seguenti:

1. [Creare una configurazione del server di destinazione](./destination-server-api.md). Il modello che verrà generato differisce, in base al valore fornito per il `maxUsersPerRequest` parametro .
   * Utilizzo `maxUsersPerRequest=1` se desideri che una chiamata API alla destinazione includa un singolo profilo, insieme alle relative qualifiche del segmento, identità e attributi di profilo.
   * Utilizzo `maxUsersPerRequest` con un valore maggiore di uno se desideri che una chiamata API alla destinazione includa più profili, insieme alle relative qualifiche dei segmenti, identità e attributi di profilo.
2. [Creare una configurazione di destinazione](./destination-configuration-api.md#create) e aggiungi l&#39;ID della configurazione del server di destinazione in `destinationDelivery.destinationServerId`.
3. [Ottieni l&#39;ID della configurazione di destinazione](./destination-configuration-api.md#retrieve-list) che hai appena creato, in modo da poterlo utilizzare nello strumento di creazione del modello.

## Come utilizzare l’API del modello di esempio e l’API del modello di rendering per creare un modello per la destinazione {#iterative-process}

>[!TIP]
>
>Prima di creare e modificare il modello di trasformazione del messaggio, puoi iniziare chiamando il [endpoint API del modello di rendering](./render-template-api.md#render-exported-data) con un modello semplice che esporta i profili non elaborati senza applicare alcuna trasformazione. La sintassi per il modello semplice è la seguente: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Il processo per ottenere e testare il modello è iterativo. Ripeti i passaggi seguenti fino a quando i profili esportati non corrispondono al formato dati previsto per la tua destinazione.

1. Primo, [ottenere un modello di esempio](./create-template.md#sample-template-api).
2. Utilizza il modello di esempio come punto di partenza per creare una bozza personalizzata.
3. Chiama il [endpoint API del modello di rendering](./create-template.md#render-template-api) con il proprio modello. Adobe genera profili di esempio in base allo schema e restituisce il risultato o eventuali errori rilevati.
4. Confrontare i dati esportati con il formato dati previsto dalla destinazione. Se necessario, modifica il modello.
5. Ripeti questo processo fino a quando i profili esportati non corrispondono al formato dati previsto dalla tua destinazione.

## Ottieni un modello di esempio utilizzando l’API del modello di esempio {#sample-template-api}

>[!NOTE]
>
>Per consultare la documentazione completa di riferimento API, leggi [Ottieni operazioni API con modelli di esempio](./sample-template-api.md).

Aggiungi un ID di destinazione alla chiamata , come mostrato di seguito, e la risposta restituisce un esempio di modello corrispondente all’ID di destinazione.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

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

## Esc i caratteri del modello {#character-escape-template}

Prima di utilizzare il modello per eseguire il rendering dei profili che corrispondono al formato previsto della destinazione, è necessario applicare l’escape dei caratteri al modello, come mostrato nella registrazione dello schermo riportata di seguito.

![Video che mostra come applicare l’escape ai caratteri di un modello utilizzando uno strumento online di escape dei caratteri](./assets/escape-characters.gif)

È possibile utilizzare uno strumento di escape online dei caratteri. La demo di cui sopra utilizza il [Formattatore JSON Escape](https://jsonformatter.org/json-escape).

## API modello di rendering {#render-template-api}

Dopo aver creato un modello di trasformazione del messaggio utilizzando [API modello di esempio](./create-template.md#sample-template-api), puoi [eseguire il rendering del modello](./render-template-api.md) per generare dati esportati in base ad essi. Questo ti consente di verificare se i profili che Adobe Experience Platform esporta nella destinazione corrispondono al formato previsto della tua destinazione.

Fai riferimento alle API per esempi di chiamate che puoi effettuare:

* [Eseguire il rendering di un modello senza profili inviati nel corpo](./render-template-api.md#multiple-profiles-no-body)
* [Eseguire il rendering di un modello con profili inviati nel corpo](./render-template-api.md#multiple-profiles-with-body)

Modifica il modello e effettua chiamate all’endpoint API del modello di rendering fino a quando i profili esportati non corrispondono al formato di dati previsto dalla tua destinazione.

## Aggiungi il modello con sequenza di caratteri alla configurazione del server di destinazione

Una volta che sei soddisfatto del modello di trasformazione del messaggio, aggiungilo al tuo [configurazione del server di destinazione](./server-and-template-configuration.md), in `httpTemplate.requestBody.value`.
