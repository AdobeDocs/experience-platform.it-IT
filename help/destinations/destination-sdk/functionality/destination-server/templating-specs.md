---
description: Scopri come formattare le richieste HTTP inviate all’endpoint. Utilizza l’endpoint /authoring/destination-servers per configurare le specifiche di modello del server di destinazione in Adobe Experience Platform Destination SDK.
title: Specifiche di modello per le destinazioni create con Destination SDK
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# Specifiche del modello per le destinazioni create con Destination SDK

Utilizza la parte specifica del modello della configurazione del server di destinazione per configurare la modalità di formattazione delle richieste HTTP inviate alla destinazione.

In una specifica del modello è possibile definire come trasformare i campi degli attributi del profilo tra lo schema XDM e il formato supportato dalla piattaforma.

Le specifiche del modello fanno parte della configurazione del server di destinazione per le destinazioni in tempo reale (streaming).

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-server-template-configuration).

È possibile configurare le specifiche del modello per la destinazione tramite l&#39;endpoint `/authoring/destination-servers`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | No |

## Configurare una specifica di modello {#configure-template-spec}

Adobe utilizza un linguaggio per modelli simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla tua destinazione.

![Configurazione modello evidenziata](../../assets/functionality/destination-server/template-configuration.png)

Per ulteriori informazioni sulla trasformazione, consulta i collegamenti seguenti:

* [Formato del messaggio](message-format.md)
* [Utilizzo di un linguaggio per modelli per le trasformazioni di identità, attributi e appartenenza a un pubblico](message-format.md#using-templating)

>[!TIP]
>
>Adobe offre uno strumento per [sviluppatori](../../testing-api/streaming-destinations/create-template.md) che consente di creare e testare un modello di trasformazione dei messaggi.

Di seguito è riportato un esempio di modello di richiesta HTTP con la descrizione di ogni singolo parametro.

```json
{
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Metodi supportati: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `value` | Stringa | *Obbligatorio.* Questa stringa è la versione con escape carattere del modello che formatta le richieste HTTP inviate da Experience Platform nel formato previsto dalla destinazione. <br> Per informazioni su come scrivere il modello, leggere la sezione su [utilizzo del modello](message-format.md#using-templating). <br> Per ulteriori informazioni sull&#39;escape di caratteri, fare riferimento allo standard JSON [RFC, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). <br> Per un esempio di trasformazione semplice, fare riferimento alla trasformazione [attributi di profilo](message-format.md#attributes). |
| `contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. A seconda del tipo di output prodotto dal modello di trasformazione, può essere uno qualsiasi dei [tipi di contenuto dell&#39;applicazione HTTP supportati](https://www.iana.org/assignments/media-types/media-types.xhtml#application). Nella maggior parte dei casi, questo valore deve essere impostato su `application/json`. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti conoscere meglio cos’è una specifica di modello e come configurarla.

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche server per le destinazioni create con Destination SDK](server-specs.md)
* [Formato del messaggio](message-format.md)
* [Configurazione formattazione file](file-formatting.md)
