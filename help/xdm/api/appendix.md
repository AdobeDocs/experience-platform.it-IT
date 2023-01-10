---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;compatibilità;modalità compatibilità;modalità compatibilità;tipo di campo;tipi di campo;
solution: Experience Platform
title: Appendice della guida API del registro dello schema
description: Questo documento fornisce informazioni supplementari relative all'utilizzo dell'API del Registro di sistema dello schema.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# Appendice della guida API del registro dello schema

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dei [!DNL Schema Registry] API.

## Utilizzo dei parametri di query {#query}

La [!DNL Schema Registry] supporta l’utilizzo di parametri di query per la pagina e filtrare i risultati quando vengono elencate le risorse.

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciale (`&`).

### Paging {#paging}

I parametri di query più comuni per il paging includono:

| Parametro | Descrizione |
| --- | --- |
| `orderby` | Ordinare i risultati per una proprietà specifica. Esempio: `orderby=title` ordinerà i risultati per titolo in ordine crescente (A-Z). Aggiunta di un `-` prima del valore del parametro (`orderby=-title`) ordina gli elementi in base al titolo in ordine decrescente (Z-A). |
| `limit` | Se utilizzato insieme a un `orderby` parametro `limit` limita il numero massimo di elementi che devono essere restituiti per una determinata richiesta. Questo parametro non può essere utilizzato senza un `orderby` parametro presente.<br><br>La `limit` specifica un numero intero positivo (tra `0` e `500`) come *suggerimento* il numero massimo di elementi da restituire. Ad esempio: `limit=5` restituisce solo cinque risorse nell’elenco. Tuttavia, questo valore non è strettamente rispettato. La dimensione effettiva della risposta può essere minore o maggiore a causa della necessità di fornire il funzionamento affidabile del `start` , se disponibile. |
| `start` | Se utilizzato insieme a un `orderby` parametro `start` specifica dove deve iniziare l&#39;elenco degli elementi impostato in modo secondario. Questo parametro non può essere utilizzato senza un `orderby` parametro presente. Questo valore può essere ottenuto dalla variabile `_page.next` attributo di una risposta a elenco e utilizzato per accedere alla pagina successiva di risultati. Se la `_page.next` è nullo, quindi non è disponibile alcuna pagina aggiuntiva.<br><br>In genere, questo parametro viene omesso per ottenere la prima pagina dei risultati. Dopo questo, `start` deve essere impostato sul valore massimo della proprietà di ordinamento principale del `orderby` campo ricevuto nella pagina precedente. La risposta API restituisce quindi le voci che iniziano con quelle che hanno una proprietà di ordinamento principale da `orderby` rigorosamente maggiore di (per ascendente) o rigorosamente inferiore (per decrescente) al valore specificato.<br><br>Ad esempio, se `orderby` è impostato su `orderby=name,firstname`, `start` contiene un valore per `name` proprietà. In questo caso, se desideri visualizzare le 20 voci successive di una risorsa immediatamente dopo il nome &quot;Miller&quot;, utilizza: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filtro {#filtering}

Puoi filtrare i risultati utilizzando la variabile `property` , che viene utilizzato per applicare un operatore specifico a una determinata proprietà JSON all’interno delle risorse recuperate. Gli operatori supportati includono:

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
>È possibile utilizzare `property` per filtrare i gruppi di campi dello schema in base alla relativa classe compatibile. Ad esempio: `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i gruppi di campi compatibili con [!DNL XDM Individual Profile] classe.

## Modalità di compatibilità {#compatibility}

[!DNL Experience Data Model] (XDM) è una specifica documentata pubblicamente, spinta dall&#39;Adobe per migliorare l&#39;interoperabilità, l&#39;espressività e il potere delle esperienze digitali. L&#39;Adobe mantiene il codice sorgente e le definizioni XDM formali in un [progetto open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM e utilizzano JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando osservi le definizioni XDM formali nell&#39;archivio pubblico, puoi notare che XDM standard è diverso da quello visualizzato in Adobe Experience Platform. Cosa vedi in [!DNL Experience Platform] è denominata Modalità compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato [!DNL Platform].

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
{ "xdm:nascitaDate": { "title": "Data di nascita", "tipo": "string", "format": "date" }, "xdm:nascitaDayAndMonth": { "title": "Data di nascita", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]" }, "xdm:nascitaYear": { "title": "Anno di nascita", "tipo": "integer", "minimum": 1, "massimo": 32767 } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "data di nascita": { "title": "Data di nascita", "tipo": "string", "format": "date", "meta:xdmField": "xdm:nascitaDate", "meta:xdmType": "date" }, "nascitaDayAndMonth": { "title": "Data di nascita", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:nascitaDayAndMonth", "meta:xdmType": "string" }, "nascitaYear": { "title": "Anno di nascita", "tipo": "integer", "minimum": 1, "massimo": 32767, "meta:xdmField": "xdm:nascitaYear", "meta:xdmType": "short" } }
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ognuno con le proprie sfide e limitazioni tecniche (ad esempio, come alcune tecnologie gestiscono caratteri speciali). Per superare queste limitazioni, è stata sviluppata la Modalità di compatibilità.

Più [!DNL Experience Platform] i servizi [!DNL Catalog], [!DNL Data Lake]e [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] in sostituzione del modello XDM standard. La [!DNL Schema Registry] L’API utilizza anche [!DNL Compatibility Mode]e gli esempi in questo documento vengono visualizzati utilizzando [!DNL Compatibility Mode].

Vale la pena sapere che una mappatura avviene tra XDM standard e il modo in cui viene operazionale in [!DNL Experience Platform], ma non dovrebbe influenzare l&#39;utilizzo di [!DNL Platform] servizi.

Il progetto open source è a tua disposizione, ma quando si tratta di interagire con le risorse tramite [!DNL Schema Registry], gli esempi di API in questo documento forniscono le best practice che dovresti conoscere e seguire.
