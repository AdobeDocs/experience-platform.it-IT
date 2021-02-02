---
keywords: ' Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;schema di registro;schema di registro;compatibilità;compatibilità;modalità compatibilità;modalità compatibilità;tipo di campo;tipi di campo;'
solution: Experience Platform
title: Appendice sviluppatore del Registro di sistema dello schema
description: Questo documento fornisce informazioni supplementari relative all'utilizzo dell'API del Registro di sistema dello schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 1%

---


# Appendice

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dell&#39;API [!DNL Schema Registry].

## Utilizzo dei parametri di query {#query}

La [!DNL Schema Registry] supporta l&#39;utilizzo di parametri di query per visualizzare la pagina e filtrare i risultati durante l&#39;elencazione delle risorse.

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e-mail (`&`).

### Pagine {#paging}

I parametri di query più comuni per il paging includono:

| Parametro | Descrizione |
| --- | --- |
| `start` | Specificate dove devono iniziare i risultati elencati. Questo valore può essere ottenuto dall&#39;attributo `_page.next` di una risposta a un elenco e utilizzato per accedere alla pagina successiva dei risultati. Se il valore `_page.next` è null, non è disponibile alcuna pagina aggiuntiva. |
| `limit` | Limita il numero di risorse restituite. Esempio: `limit=5` restituirà un elenco di cinque risorse. |
| `orderby` | Ordinare i risultati in base a una proprietà specifica. Esempio: `orderby=title` ordinerà i risultati in ordine crescente (A-Z) in base al titolo. Se si aggiunge `-` prima del valore del parametro (`orderby=-title`), gli elementi vengono ordinati in base al titolo in ordine decrescente (Z-A). |

### Filtro {#filtering}

Potete filtrare i risultati utilizzando il parametro `property`, utilizzato per applicare un operatore specifico a una determinata proprietà JSON all&#39;interno delle risorse recuperate. Gli operatori supportati includono:

| Operatore | Descrizione | Esempio |
| --- | --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore fornito. | `property=title==test` |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore fornito. | `property=title!=test` |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore fornito. | `property=version<5` |
| `>` | Filtra in base al fatto che la proprietà sia maggiore del valore fornito. | `property=version>5` |
| `<=` | Filtra se la proprietà è minore o uguale al valore specificato. | `property=version<=5` |
| `>=` | Filtra in base al fatto che la proprietà sia maggiore o uguale al valore fornito. | `property=version>=5` |
| `~` | Filtra in base al fatto che la proprietà corrisponda o meno a un&#39;espressione regolare specificata. | `property=title~test$` |
| (Nessuna) | Se si specifica solo il nome della proprietà, vengono restituite solo le voci in cui esiste la proprietà. | `property=title` |

>[!TIP]
>
>Potete utilizzare il parametro `property` per filtrare i mixin in base alla classe compatibile. Ad esempio, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i mixin compatibili con la classe [!DNL XDM Individual Profile].

## Modalità compatibilità

[!DNL Experience Data Model] (XDM) è una specifica documentata pubblicamente, spinta da  Adobe per migliorare l&#39;interoperabilità, l&#39;espressività e il potere delle esperienze digitali.  Adobe mantiene il codice sorgente e le definizioni XDM formali in un progetto [open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM, utilizzando la Notazione oggetto JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando si esaminano le definizioni XDM formali nell&#39;archivio pubblico, è possibile notare che lo standard XDM è diverso da quello visualizzato in Adobe Experience Platform. Ciò che si vede in [!DNL Experience Platform] è denominata Modalità compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato all&#39;interno di [!DNL Platform].

### Funzionamento della modalità di compatibilità

La modalità di compatibilità consente al modello XDM JSON-LD di funzionare con l&#39;infrastruttura dati esistente modificando i valori all&#39;interno di XDM standard mantenendo la stessa semantica. Utilizza una struttura JSON nidificata, mostrando gli schemi in un formato simile a un albero.

La differenza principale che noterete tra XDM standard e Modalità compatibilità è la rimozione del prefisso &quot;xdm:&quot; per i nomi dei campi.

Di seguito è riportato un confronto affiancato che mostra i campi relativi al compleanno (con gli attributi &quot;description&quot; rimossi) sia in XDM standard che in Modalità compatibilità. I campi Modalità compatibilità includono un riferimento al campo XDM e al relativo tipo di dati negli attributi &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table>
  <th>XDM standard</th>
  <th>Modalità compatibilità</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:bornDate": {
              "title": "Data di nascita",
              "type": "string",
              "format": "date",
          },
          "xdm:bornDayAndMonth": {
              "title": "Data di nascita",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:bornYear": {
              "title": "Anno di nascita",
              "type": "integer",
              "minimo": 1,
              "massima": 32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
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
              "minimo": 1,
              "massima": 32767,
              "meta:xdmField": "xdm:bornYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ciascuno con le proprie problematiche e limitazioni tecniche (ad esempio, come alcune tecnologie gestiscono caratteri speciali). Per superare questi limiti, è stata sviluppata la Modalità di compatibilità.

La maggior parte dei servizi [!DNL Experience Platform], inclusi [!DNL Catalog], [!DNL Data Lake] e [!DNL Real-time Customer Profile] utilizzano [!DNL Compatibility Mode] al posto di XDM standard. Anche l&#39;API [!DNL Schema Registry] utilizza [!DNL Compatibility Mode], e gli esempi in questo documento vengono visualizzati utilizzando [!DNL Compatibility Mode].

Vale la pena sapere che una mappatura viene eseguita tra XDM standard e il modo in cui viene eseguita in [!DNL Experience Platform], ma non deve influenzare l&#39;utilizzo dei servizi [!DNL Platform].

Il progetto open source è disponibile, ma quando si tratta di interagire con le risorse tramite [!DNL Schema Registry], gli esempi di API in questo documento forniscono le best practice che dovreste conoscere e seguire.