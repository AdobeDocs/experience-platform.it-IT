---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;modello dati;registro schema;registro schema;compatibilità;compatibilità;modalità compatibilità;modalità compatibilità;modalità compatibilità;tipo di campo;tipi di campo;
solution: Experience Platform
title: Appendice alla guida API del registro dello schema
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Schema Registry.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Appendice alla guida API del registro dello schema

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo di [!DNL Schema Registry] API.

## Utilizzo dei parametri di query {#query}

Il [!DNL Schema Registry] supporta l’utilizzo di parametri di query per visualizzare e filtrare i risultati quando si elencano le risorse.

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciali (`&`).

### Paging {#paging}

I parametri di query più comuni per il paging includono:

| Parametro | Descrizione |
| --- | --- |
| `orderby` | Ordinare i risultati per una proprietà specifica. Esempio: `orderby=title` I risultati verranno ordinati in base al titolo in ordine crescente (A-Z). Aggiunta di un `-` prima del valore del parametro (`orderby=-title`) ordinerà gli elementi in base al titolo in ordine decrescente (Z-A). |
| `limit` | Se utilizzato in combinazione con un `orderby` parametro, `limit` limita il numero massimo di elementi da restituire per una determinata richiesta. Questo parametro non può essere utilizzato senza un `orderby` parametro presente.<br><br>Il `limit` Il parametro specifica un numero intero positivo (tra `0` e `500`) come *suggerimento* per quanto riguarda il numero massimo di elementi da restituire. Ad esempio: `limit=5` restituisce solo cinque risorse nell&#39;elenco. Tuttavia, questo valore non viene rispettato rigorosamente. La dimensione effettiva della risposta può essere minore o maggiore in funzione della necessità di garantire il funzionamento affidabile del `start` , se disponibile. |
| `start` | Se utilizzato in combinazione con un `orderby` parametro, `start` specifica da dove deve iniziare l&#39;elenco di elementi sottoimpostato. Questo parametro non può essere utilizzato senza un `orderby` parametro presente. Questo valore può essere ottenuto dalla proprietà `_page.next` attributo di una risposta elenco e utilizzato per accedere alla pagina successiva dei risultati. Se il `_page.next` il valore è nullo, quindi non sono disponibili pagine aggiuntive.<br><br>In genere, questo parametro viene omesso per ottenere la prima pagina di risultati. Dopo, `start` deve essere impostato sul valore massimo della proprietà di ordinamento primaria del `orderby` campo ricevuto nella pagina precedente. La risposta API restituisce quindi le voci che iniziano con quelle che hanno una proprietà di ordinamento primaria da `orderby` rigorosamente maggiore di (ascendente) o strettamente minore (discendente) del valore specificato.<br><br>Ad esempio, se `orderby` il parametro è impostato su `orderby=name,firstname`, il `start` il parametro conterrà un valore per `name` proprietà. In questo caso, se desideri visualizzare le prossime 20 voci di una risorsa subito dopo il nome &quot;Miller&quot;, utilizza: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filtro {#filtering}

Puoi filtrare i risultati utilizzando `property` , utilizzato per applicare un operatore specifico a una determinata proprietà JSON all’interno delle risorse recuperate. Gli operatori supportati includono:

| Operatore | Descrizione | Esempio |
| --- | --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore specificato. | `property=title==test` |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore specificato. | `property=title!=test` |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore specificato. | `property=version<5` |
| `>` | Filtra in base al fatto che la proprietà sia maggiore del valore specificato. | `property=version>5` |
| `<=` | Filtra in base al fatto che la proprietà sia minore o uguale al valore specificato. | `property=version<=5` |
| `>=` | Filtra in base al fatto che la proprietà sia maggiore o uguale al valore specificato. | `property=version>=5` |
| (Nessuna) | L&#39;indicazione solo del nome della proprietà restituisce solo le voci in cui la proprietà esiste. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>È possibile utilizzare `property` parametro per filtrare i gruppi di campi dello schema in base alla classe compatibile. Ad esempio: `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i gruppi di campi compatibili con [!DNL XDM Individual Profile] classe.

## Modalità di compatibilità {#compatibility}

[!DNL Experience Data Model] (XDM) è una specifica documentata pubblicamente, guidata da Adobe per migliorare l’interoperabilità, l’espressività e la potenza delle esperienze digitali. L’Adobe mantiene il codice sorgente e le definizioni XDM formali in un [progetto open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM, utilizzando JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando esamini le definizioni XDM formali nell’archivio pubblico, puoi notare che XDM standard è diverso da quello visualizzato in Adobe Experience Platform. Cosa vedi in [!DNL Experience Platform] si chiama Modalità di compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato in [!DNL Platform].

### Funzionamento della modalità di compatibilità

La modalità di compatibilità consente al modello XDM JSON-LD di funzionare con l’infrastruttura dati esistente alterando i valori all’interno di XDM standard mantenendo la stessa semantica. Utilizza una struttura JSON nidificata, che mostra gli schemi in un formato ad albero.

La differenza principale che noterai tra XDM standard e la modalità di compatibilità è la rimozione del prefisso &quot;xdm:&quot; per i nomi di campo.

Di seguito è riportato un confronto affiancato che mostra i campi relativi al compleanno (con gli attributi &quot;description&quot; rimossi) sia in XDM standard che in Modalità compatibilità. I campi Modalità di compatibilità includono un riferimento al campo XDM e al relativo tipo di dati negli attributi &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>XDM standard</th>
  <th>Modalità di compatibilità</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:bornDate": { "title": "Data di nascita", "type": "string", "format": "date" }, "xdm:bornDayAndMonth": { "title": "Data di nascita", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]" }, "xdm:bornYear": { "title": "Anno di nascita", "type": "integer", "minimum": 1, "maximum": 32767 }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "bornDate": { "title": "Birth Date", "type": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Birth Date", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth"", "meta:xdmType": "string" }, "bornYear": { "title": "Nascita anno", "type": "integer", "minimum": 1, "maximum": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ciascuno con le proprie sfide e limitazioni tecniche (ad esempio, il modo in cui alcune tecnologie gestiscono i caratteri speciali). Per superare queste limitazioni, è stata sviluppata la Modalità di compatibilità.

Più [!DNL Experience Platform] servizi, tra cui [!DNL Catalog], [!DNL Data Lake], e [!DNL Real-Time Customer Profile] utilizzare [!DNL Compatibility Mode] al posto dello standard XDM. Il [!DNL Schema Registry] L’API utilizza anche [!DNL Compatibility Mode], e gli esempi in questo documento sono tutti visualizzati utilizzando [!DNL Compatibility Mode].

Vale la pena sapere che viene eseguita una mappatura tra XDM standard e il modo in cui viene operata in [!DNL Experience Platform], ma non dovrebbe influire sull’uso di [!DNL Platform] servizi.

Il progetto open source è disponibile, ma quando si tratta di interagire con le risorse tramite [!DNL Schema Registry], gli esempi di API contenuti in questo documento forniscono le best practice da conoscere e seguire.
