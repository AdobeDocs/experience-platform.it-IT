---
description: Scopri come formattare le richieste HTTP inviate all’endpoint. Utilizza l’endpoint /authoring/destination-servers per configurare le specifiche del modello del server di destinazione in Adobe Experience Platform Destination SDK.
title: Specifiche dei modelli per le destinazioni create con Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---


# Specifiche dei modelli per le destinazioni create con Destination SDK

Utilizza la specifica del modello nella configurazione del server di destinazione per configurare il formato delle richieste HTTP inviate alla destinazione.

In una specifica del modello è possibile definire come trasformare i campi dell’attributo del profilo tra lo schema XDM e il formato supportato dalla piattaforma.

Le specifiche dei modelli fanno parte della configurazione del server di destinazione per le destinazioni in tempo reale (streaming).

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta la guida su come [utilizza Destination SDK per configurare una destinazione streaming](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Puoi configurare le specifiche del modello per la destinazione tramite `/authoring/destination-servers` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | No |

## Configurare una specifica di modello {#configure-template-spec}

Adobe utilizza un linguaggio modello simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla destinazione.

![Configurazione del modello evidenziata](../../assets/functionality/destination-server/template-configuration.png)

Per ulteriori informazioni sulla trasformazione, visita i collegamenti seguenti:

* [Formato del messaggio](message-format.md)
* [Utilizzo di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza ai segmenti ](message-format.md#using-templating)

>[!TIP]
>
>L’Adobe offre un [strumento per sviluppatori](../../testing-api/streaming-destinations/create-template.md) che consente di creare e testare un modello di trasformazione del messaggio.

Di seguito è riportato un esempio di modello di richiesta HTTP, con le descrizioni di ogni singolo parametro.

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
| `templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `value` | Stringa | *Obbligatorio.* Questa stringa è la versione con sequenza di caratteri del modello che formatta le richieste HTTP inviate da Platform nel formato previsto dalla tua destinazione. <br> Per informazioni su come scrivere il modello, consulta la sezione su [utilizzo di modelli](message-format.md#using-templating). <br> Per ulteriori informazioni sull&#39;escape dei caratteri, consulta la [RFC JSON standard, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). <br> Per un esempio di trasformazione semplice, consulta la sezione [attributi del profilo](message-format.md#attributes) trasformazione. |
| `contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. A seconda del tipo di output prodotto dal modello di trasformazione, questo può essere uno dei [Tipi di contenuto dell’applicazione HTTP](https://www.iana.org/assignments/media-types/media-types.xhtml#application). Nella maggior parte dei casi, questo valore deve essere impostato su `application/json`. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di ciò che è una specifica del modello e di come puoi configurarlo.

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche server per le destinazioni create con Destination SDK](server-specs.md)
* [Formato del messaggio](message-format.md)
* [Configurazione della formattazione dei file](file-formatting.md)