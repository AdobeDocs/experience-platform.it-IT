---
description: Scopri come configurare le opzioni di formattazione dei file per le destinazioni basate su file create con Adobe Experience Platform Destination SDK tramite l’endpoint "/destination-servers".
title: Configurazione formattazione file
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# Configurazione formattazione file

Destination SDK supporta un set flessibile di funzioni che puoi configurare in base alle tue esigenze di integrazione. Tra queste funzioni è incluso il supporto per [!DNL CSV] formattazione del file.

Quando crei destinazioni basate su file tramite Destination SDK, puoi definire la formattazione dei file CSV esportati. Puoi personalizzare molte opzioni di formattazione, ad esempio, ma non solo:

* Se il file CSV deve includere un’intestazione;
* Quale carattere utilizzare per citare i valori;
* Come dovrebbero apparire i valori vuoti.

A seconda della configurazione di destinazione, gli utenti visualizzeranno determinate opzioni nell’interfaccia utente quando si connettono a una destinazione basata su file. Puoi vedere come si presentano queste opzioni in [opzioni di formattazione dei file per le destinazioni basate su file](../../../ui/batch-destinations-file-formatting-options.md) documentazione.


Le impostazioni di formattazione dei file fanno parte della configurazione del server di destinazione per le destinazioni basate su file.

Per capire dove questo componente si inserisce in un’integrazione creata con Destination SDK, consulta il diagramma riportato di seguito. [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

È possibile configurare le opzioni di formattazione del file tramite `/authoring/destination-servers` endpoint. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](../../authoring-api/destination-server/update-destination-server.md)

Questa pagina descrive tutte le impostazioni di formattazione dei file supportate per l&#39;esportazione `CSV` file.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | No |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

È possibile modificare diverse proprietà dei file esportati in modo che corrispondano ai requisiti del sistema di ricezione dei file della destinazione, al fine di leggere e interpretare in modo ottimale i file ricevuti da Experience Platform.

>[!NOTE]
>
>Le opzioni CSV sono supportate solo quando si esportano file CSV. Il `fileConfigurations` questa sezione non è obbligatoria durante la configurazione di un nuovo server di destinazione. Se nella chiamata API non trasmetti alcun valore per le opzioni CSV, i valori predefiniti verranno recuperati da [tabella di riferimento più avanti](#file-formatting-reference-and-example) verrà utilizzato.


## Opzioni CSV in cui gli utenti non possono selezionare le opzioni di configurazione {#file-configuration-templating-none}

Nell’esempio di configurazione seguente, tutte le opzioni CSV sono predefinite. Le impostazioni di esportazione definite in ciascuna `csvOptions` I parametri sono finali e gli utenti non possono modificarli.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## Opzioni CSV in cui gli utenti possono selezionare le opzioni di configurazione {#file-configuration-templating-pebble}

Nell’esempio di configurazione seguente, nessuna delle opzioni CSV è predefinita. Il `value` in ciascuno dei `csvOptions` parametri è configurato in un campo corrispondente dei dati del cliente tramite `/destinations` endpoint (ad esempio [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) per `quote` file (opzione di formattazione del file) e gli utenti possono utilizzare l’interfaccia utente di Experience Platform per selezionare tra le varie opzioni configurate nel campo dati cliente corrispondente. Puoi vedere come si presentano queste opzioni in [opzioni di formattazione dei file per le destinazioni basate su file](../../../ui/batch-destinations-file-formatting-options.md) documentazione.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      }
   }
}
```

## Riferimento completo ed esempi per le opzioni di formattazione dei file supportate {#file-formatting-reference-and-example}

>[!TIP]
>
>Le opzioni di formattazione del file CSV descritte di seguito sono documentate anche nel [Guida di Apache Spark per file CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Le descrizioni utilizzate di seguito sono tratte dalla guida di Apache Spark.

Di seguito è riportato un riferimento completo di tutte le opzioni di formattazione dei file disponibili in Destination SDK, insieme a esempi di output per ogni opzione.

| Campo | Obbligatorio/facoltativo | Descrizione | Valore predefinito | Esempio di output 1 | Esempio di output 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obbligatorio | Per ogni opzione di formattazione del file configurata, è necessario aggiungere il parametro `templatingStrategy`, che può avere due valori: <br><ul><li>`NONE`: utilizza questo valore se non intendi consentire agli utenti di selezionare tra valori diversi per una configurazione. Consulta [questa configurazione](#file-configuration-templating-none) ad esempio, in cui le opzioni di formattazione del file sono fisse.</li><li>`PEBBLE_V1`: utilizza questo valore se desideri consentire agli utenti di selezionare tra valori diversi per una configurazione. In questo caso, devi anche impostare un campo dati cliente corrispondente nel `/destination` configurazione dell’endpoint, per rendere note le varie opzioni agli utenti nell’interfaccia utente. Consulta [questa configurazione](#file-configuration-templating-pebble) ad esempio, in cui gli utenti possono selezionare tra diversi valori per le opzioni di formattazione del file.</li></ul> | - | - | - |
| `compression.value` | Facoltativo | Codec di compressione da utilizzare per il salvataggio dei dati nel file. Valori supportati: `none`, `bzip2`, `gzip`, `lz4`, e `snappy`. | `none` | - | - |
| `fileType.value` | Facoltativo | Specifica il formato del file di output. Valori supportati: `csv`, `parquet`, e `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape dei valori tra virgolette, in cui il separatore può far parte del valore. | `null` | - | - |
| `csvOptions.quoteAll.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tutti i valori devono essere sempre racchiusi tra virgolette. L&#39;impostazione predefinita prevede solo l&#39;escape di valori contenenti virgolette. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un separatore per ogni campo e valore. Il separatore può essere costituito da uno o più caratteri. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per eseguire l’escape delle virgolette all’interno di un valore già tra virgolette. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se i valori contenenti virgolette devono essere sempre racchiusi tra virgolette. L&#39;impostazione predefinita prevede l&#39;escape di tutti i valori contenenti una virgoletta. | `true` | - | - |
| `csvOptions.header.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se scrivere i nomi delle colonne come prima riga nel file esportato. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se eliminare gli spazi bianchi iniziali dai valori. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se rifilare gli spazi vuoti finali dai valori. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la rappresentazione di stringa di un valore null. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica il formato della data. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la stringa che indica un formato timestamp. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape del carattere virgolette. | `\` quando i caratteri escape e le virgolette sono diversi. `\0` quando il carattere di escape e le virgolette sono uguali. | - | - |
| `csvOptions.emptyValue.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la rappresentazione di stringa di un valore vuoto. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti conoscere meglio il funzionamento della formattazione dei file in una configurazione del server di destinazione e come configurarla.

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche del server per le destinazioni create con Destination SDK](server-specs.md)
* [Specifiche di modello](templating-specs.md)
* [Formato del messaggio](message-format.md)