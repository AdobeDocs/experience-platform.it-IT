---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;modello dati;registro schema;registro schema;compatibilità;compatibilità;modalità compatibilità;modalità compatibilità;modalità compatibilità;tipo di campo;tipi di campo;
solution: Experience Platform
title: Appendice alla guida API del registro dello schema
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Schema Registry.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# Appendice alla guida API del registro dello schema

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dell&#39;API [!DNL Schema Registry].

## Utilizzo dei parametri di query {#query}

[!DNL Schema Registry] supporta l&#39;utilizzo di parametri di query per la pagina e il filtro dei risultati quando si elencano le risorse.

>[!NOTE]
>
>Quando si combinano più parametri di query, è necessario separarli con il simbolo di E commerciale (`&`).

### Paging {#paging}

I parametri di query più comuni per il paging includono:

| Parametro | Descrizione |
| --- | --- |
| `orderby` | Ordinare i risultati per una proprietà specifica. Esempio: `orderby=title` ordinerà i risultati per titolo in ordine crescente (A-Z). L&#39;aggiunta di un `-` prima del valore del parametro (`orderby=-title`) ordinerà gli elementi in base al titolo in ordine decrescente (Z-A). |
| `limit` | Se utilizzato insieme a un parametro `orderby`, `limit` limita il numero massimo di elementi da restituire per una determinata richiesta. Impossibile utilizzare questo parametro senza un parametro `orderby`.<br><br>Il parametro `limit` specifica un numero intero positivo (tra `0` e `500`) come *suggerimento* per il numero massimo di elementi da restituire. Ad esempio, `limit=5` restituisce solo cinque risorse nell&#39;elenco. Tuttavia, questo valore non viene rispettato rigorosamente. La dimensione effettiva della risposta può essere minore o maggiore, in base alla necessità di fornire il funzionamento affidabile del parametro `start`, se fornito. |
| `start` | Se utilizzato insieme a un parametro `orderby`, `start` specifica da dove deve iniziare l&#39;elenco di elementi sottoimpostato. Impossibile utilizzare questo parametro senza un parametro `orderby`. Questo valore può essere ottenuto dall&#39;attributo `_page.next` di una risposta elenco e utilizzato per accedere alla pagina successiva dei risultati. Se il valore `_page.next` è null, non è disponibile alcuna pagina aggiuntiva.<br><br>Questo parametro viene in genere omesso per ottenere la prima pagina di risultati. Successivamente, `start` deve essere impostato sul valore massimo della proprietà di ordinamento primaria del campo `orderby` ricevuto nella pagina precedente. La risposta API restituisce quindi le voci che iniziano con quelle che hanno una proprietà di ordinamento primaria da `orderby` rigorosamente maggiore (per crescente) o minore (per decrescente) del valore specificato.<br><br>Ad esempio, se il parametro `orderby` è impostato su `orderby=name,firstname`, il parametro `start` conterrà un valore per la proprietà `name`. In questo caso, se desideri visualizzare le prossime 20 voci di una risorsa subito dopo il nome &quot;Miller&quot;, utilizza: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filtro {#filtering}

È possibile filtrare i risultati utilizzando il parametro `property`, utilizzato per applicare un operatore specifico a una determinata proprietà JSON nelle risorse recuperate. Gli operatori supportati includono:

| Operatore | Descrizione | Esempio |
| --- | --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore specificato. | `property=title==test` |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore specificato. | `property=title!=test` |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore specificato. | `property=version<5` |
| `>` | Filtra in base al fatto che la proprietà sia maggiore del valore specificato. | `property=version>5` |
| `<=` | Filtra in base al fatto che la proprietà sia minore o uguale al valore specificato. | `property=version<=5` |
| `>=` | Filtra in base al fatto che la proprietà sia maggiore o uguale al valore specificato. | `property=version>=5` |
| (Nessuno) | L&#39;indicazione solo del nome della proprietà restituisce solo le voci in cui la proprietà esiste. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>È possibile utilizzare il parametro `property` per filtrare i gruppi di campi dello schema in base alla classe compatibile. Ad esempio, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i gruppi di campi compatibili con la classe [!DNL XDM Individual Profile].

## Modalità di compatibilità {#compatibility}

[!DNL Experience Data Model] (XDM) è una specifica pubblicamente documentata, guidata da Adobe per migliorare l&#39;interoperabilità, l&#39;espressività e la potenza delle esperienze digitali. Adobe mantiene il codice sorgente e le definizioni XDM formali in un progetto [open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM, utilizzando JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando esamini le definizioni XDM formali nell’archivio pubblico, puoi notare che XDM standard è diverso da quello visualizzato in Adobe Experience Platform. Ciò che visualizzi in [!DNL Experience Platform] è chiamato Modalità di compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato in [!DNL Platform].

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
{
  "xdm:bornDate": {
    "title": "Data di nascita",
    "type": "string",
    "format": "date"
  },
  "xdm:bornDayAndMonth": {
    "title": "Data di nascita",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]"
  },
  "xdm:bornYear": {
    "title": "Anno di nascita",
    "type": "integer",
    "minimum": 1
    "maximum": 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "bornDate": {
    "title": "Data di nascita",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:bornDate",
    "meta:xdmType": "date"
  },
  "bornDayAndMonth": {
    "title": "Data di nascita",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:bornDayAndMonth",
    "meta:xdmType": "string"
  },
  "bornYear": {
    "title": "Anno di nascita",
    "type": "integer",
    "minimum": 1
    "maximum": 32767,
    "meta:xdmField": "xdm:bornYear",
    "meta:xdmType": "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ciascuno con le proprie sfide e limitazioni tecniche (ad esempio, il modo in cui alcune tecnologie gestiscono i caratteri speciali). Per superare queste limitazioni, è stata sviluppata la Modalità di compatibilità.

La maggior parte dei servizi [!DNL Experience Platform], tra cui [!DNL Catalog], [!DNL Data Lake] e [!DNL Real-Time Customer Profile], utilizza [!DNL Compatibility Mode] al posto di XDM standard. Anche l&#39;API [!DNL Schema Registry] utilizza [!DNL Compatibility Mode] e gli esempi in questo documento sono tutti visualizzati utilizzando [!DNL Compatibility Mode].

È utile sapere che viene eseguita una mappatura tra XDM standard e il modo in cui è operazionalizzato in [!DNL Experience Platform], ma non dovrebbe influire sull&#39;utilizzo dei servizi [!DNL Platform].

Il progetto open source è disponibile, ma quando si tratta di interagire con le risorse tramite [!DNL Schema Registry], gli esempi di API in questo documento forniscono le best practice da conoscere e seguire.
