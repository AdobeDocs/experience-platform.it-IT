---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;compatibilità;modalità compatibilità;modalità compatibilità;tipo di campo;tipi di campo;
solution: Experience Platform
title: Appendice della guida API del registro dello schema
description: Questo documento fornisce informazioni supplementari relative all'utilizzo dell'API del Registro di sistema dello schema.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 2871108b67d3d84f1578e80e9c087444ff407820
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# Appendice della guida API del registro dello schema

Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API [!DNL Schema Registry].

## Utilizzo dei parametri di query {#query}

Il [!DNL Schema Registry] supporta l’utilizzo di parametri di query per la pagina e filtrare i risultati durante l’elenco delle risorse.

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciali (`&`).

### Paging {#paging}

I parametri di query più comuni per il paging includono:

| Parametro | Descrizione |
| --- | --- |
| `orderby` | Ordinare i risultati per una proprietà specifica. Esempio: `orderby=title` ordinerà i risultati per titolo in ordine crescente (A-Z). Se si aggiunge un `-` prima del valore del parametro (`orderby=-title`), gli elementi vengono ordinati per titolo in ordine decrescente (Z-A). |
| `limit` | Se utilizzato insieme a un parametro `orderby` , `limit` limita il numero massimo di elementi che devono essere restituiti per una determinata richiesta. Questo parametro non può essere utilizzato senza un parametro `orderby` presente.<br><br>Il  `limit` parametro specifica un numero intero positivo (tra  `0` e  `500`) come  ** hintas al numero massimo di elementi che devono essere restituiti. Ad esempio, `limit=5` restituisce solo cinque risorse nell’elenco. Tuttavia, questo valore non è strettamente rispettato. La dimensione effettiva della risposta può essere inferiore o maggiore in base alla necessità di fornire il funzionamento affidabile del parametro `start`, se fornito. |
| `start` | Se utilizzato insieme a un parametro `orderby`, `start` specifica la posizione di inizio dell’elenco degli elementi impostato come secondario. Questo parametro non può essere utilizzato senza un parametro `orderby` presente. Questo valore può essere ottenuto dall&#39;attributo `_page.next` di una risposta a elenco e utilizzato per accedere alla pagina successiva di risultati. Se il valore `_page.next` è null, non è disponibile alcuna pagina aggiuntiva.<br><br>In genere, questo parametro viene omesso per ottenere la prima pagina dei risultati. Successivamente, `start` deve essere impostato sul valore massimo della proprietà di ordinamento principale del campo `orderby` ricevuto nella pagina precedente. La risposta API restituisce quindi le voci che iniziano con quelle che hanno una proprietà di ordinamento principale da `orderby` rigorosamente maggiore di (per ascendente) o rigorosamente inferiore (per decrescente) al valore specificato.<br><br>Ad esempio, se il  `orderby` parametro è impostato su  `orderby=name,firstname`, il  `start` parametro conterrà un valore per la  `name` proprietà. In questo caso, se desideri visualizzare le 20 voci successive di una risorsa immediatamente dopo il nome &quot;Miller&quot;, utilizza: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filtro {#filtering}

Puoi filtrare i risultati utilizzando il parametro `property` , utilizzato per applicare un operatore specifico a una determinata proprietà JSON all’interno delle risorse recuperate. Gli operatori supportati includono:

| Operatore | Descrizione | Esempio |
| --- | --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore fornito. | `property=title==test` |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore fornito. | `property=title!=test` |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore specificato. | `property=version<5` |
| `>` | Filtra per determinare se la proprietà è maggiore del valore specificato. | `property=version>5` |
| `<=` | Filtra per specificare se la proprietà è minore o uguale al valore specificato. | `property=version<=5` |
| `>=` | Filtra per specificare se la proprietà è maggiore o uguale al valore specificato. | `property=version>=5` |
| `~` | Filtra per stabilire se la proprietà corrisponde a un&#39;espressione regolare specificata. | `property=title~test$` |
| (Nessuna) | Se si imposta solo il nome della proprietà, vengono restituite solo le voci in cui esiste la proprietà. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Puoi utilizzare il parametro `property` per filtrare i gruppi di campi dello schema in base alla relativa classe compatibile. Ad esempio, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i gruppi di campi compatibili con la classe [!DNL XDM Individual Profile] .

## Modalità di compatibilità {#compatibility}

[!DNL Experience Data Model] (XDM) è una specifica documentata pubblicamente, spinta dall&#39;Adobe per migliorare l&#39;interoperabilità, l&#39;espressività e il potere delle esperienze digitali. Adobe mantiene il codice sorgente e le definizioni XDM formali in un progetto [open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM e utilizzano JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando osservi le definizioni XDM formali nell&#39;archivio pubblico, puoi notare che XDM standard è diverso da quello visualizzato in Adobe Experience Platform. Ciò che visualizzi in [!DNL Experience Platform] si chiama Modalità di compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato in [!DNL Platform].

### Funzionamento della modalità di compatibilità

La modalità di compatibilità consente al modello XDM JSON-LD di funzionare con l’infrastruttura di dati esistente modificando i valori all’interno di XDM standard mantenendo la stessa semantica. Utilizza una struttura JSON nidificata, visualizzando gli schemi in un formato simile a una struttura.

La differenza principale che noterai tra XDM standard e Modalità di compatibilità è la rimozione del prefisso &quot;xdm:&quot; per i nomi di campo.

Di seguito è riportato un confronto affiancato che mostra i campi relativi al compleanno (con gli attributi &quot;description&quot; rimossi) sia in XDM standard che in Modalità compatibilità. I campi Modalità compatibilità includono un riferimento al campo XDM e al relativo tipo di dati negli attributi &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>XDM standard</th>
  <th>Modalità di compatibilità</th>
  <tr>
  <td>
  <pre class=" language-json">
{
  "xdm:nascitaDate": {
    "title": "Data di nascita",
    "type": "string",
    "format": "date"
  },
  "xdm:nascitaDayAndMonth": {
    "title": "Data di nascita",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]"
  },
  "xdm:nascitaYear": {
    "title": "Anno di nascita",
    "type": "integer",
    "minimo": 1
    "massimo": 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "data di nascita": {
    "title": "Data di nascita",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:nascitaDate",
    "meta:xdmType": "date"
  },
  "nascitaDayAndMonth": {
    "title": "Data di nascita",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:nascitaDayAndMonth",
    "meta:xdmType": "string"
  },
  "nataleYear": {
    "title": "Anno di nascita",
    "type": "integer",
    "minimo": 1
    "massimo": 32767,
    "meta:xdmField": "xdm:nascitaYear",
    "meta:xdmType": "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ognuno con le proprie sfide e limitazioni tecniche (ad esempio, come alcune tecnologie gestiscono caratteri speciali). Per superare queste limitazioni, è stata sviluppata la Modalità di compatibilità.

La maggior parte dei servizi [!DNL Experience Platform], inclusi [!DNL Catalog], [!DNL Data Lake] e [!DNL Real-time Customer Profile] utilizza [!DNL Compatibility Mode] al posto di XDM standard. L’ API [!DNL Schema Registry] utilizza anche [!DNL Compatibility Mode] e gli esempi contenuti in questo documento vengono visualizzati utilizzando [!DNL Compatibility Mode].

Vale la pena sapere che una mappatura avviene tra XDM standard e il modo in cui viene operazionale in [!DNL Experience Platform], ma non dovrebbe influenzare l&#39;utilizzo dei servizi [!DNL Platform].

Il progetto open source è a tua disposizione, ma quando si tratta di interagire con le risorse tramite [!DNL Schema Registry], gli esempi di API in questo documento forniscono le best practice da conoscere e seguire.
