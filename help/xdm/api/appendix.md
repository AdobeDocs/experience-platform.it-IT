---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Appendice sviluppatore del Registro di sistema dello schema
description: Questo documento fornisce informazioni supplementari relative all'utilizzo dell'API del Registro di sistema dello schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Appendice

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dell&#39; [!DNL Schema Registry] API.

## Modalità compatibilità

[!DNL Experience Data Model] (XDM) è una specifica documentata pubblicamente, spinta da  Adobe per migliorare l&#39;interoperabilità, l&#39;espressività e il potere delle esperienze digitali.  Adobe mantiene il codice sorgente e le definizioni XDM formali in un progetto [open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM, utilizzando la Notazione oggetto JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando si esaminano le definizioni XDM formali nell&#39;archivio pubblico, è possibile notare che lo standard XDM è diverso da quello visualizzato in Adobe Experience Platform. Ciò che vedete in [!DNL Experience Platform] è chiamato Modalità compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato all&#39;interno [!DNL Platform].

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
        { "xdm:bornDate": { "title": "Data di nascita", "tipo": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Data di nascita", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Anno di nascita", "tipo": "integer", "Minimum": 1, "massimo": 32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Data di nascita", "tipo": "string", "format": "date", "meta:xdmField": "xdm:BirDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Data di nascita", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Anno di nascita", "tipo": "integer", "Minimum": 1, "massimo": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ciascuno con le proprie problematiche e limitazioni tecniche (ad esempio, come alcune tecnologie gestiscono caratteri speciali). Per superare questi limiti, è stata sviluppata la Modalità di compatibilità.

La maggior parte [!DNL Experience Platform] dei servizi, inclusi [!DNL Catalog], [!DNL Data Lake]e [!DNL Real-time Customer Profile] utilizzati [!DNL Compatibility Mode] al posto di XDM standard. L&#39; [!DNL Schema Registry] API utilizza anche [!DNL Compatibility Mode]e gli esempi in questo documento vengono visualizzati utilizzando [!DNL Compatibility Mode].

Vale la pena sapere che una mappatura avviene tra XDM standard e il modo in cui viene operata, [!DNL Experience Platform]ma non dovrebbe influenzare l&#39;utilizzo dei [!DNL Platform] servizi.

Il progetto open source è a vostra disposizione, ma quando si tratta di interagire con le risorse tramite [!DNL Schema Registry], gli esempi API di questo documento forniscono le best practice che dovreste conoscere e seguire.