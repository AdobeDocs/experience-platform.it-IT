---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;nome completo;xdm:fullName;nome persona;nome;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati Nome persona
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Nome persona.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# [!UICONTROL Tipo di dati ] con nome persona

[!UICONTROL Il ] nome della persona è un tipo di dati XDM standard che descrive il nome completo di una persona. Poiché le convenzioni per le strutture dei nomi differiscono notevolmente tra lingue e culture, i nomi devono sempre essere modellati utilizzando questo tipo di dati.

Inoltre, il tipo di dati fornisce una serie di proprietà facoltative che possono essere utilizzate in situazioni che richiedono l’utilizzo di un solo frammento del nome completo, ad esempio la creazione di un saluto formale o informale.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `courtesyTitle` | Abbreviazione del titolo, dell&#39;onorifico o del saluto di una persona (ad esempio `Mr.`, `Miss.` o `Dr.`). |
| `firstName` | Il primo segmento del nome nell’ordine di scrittura più comunemente accettato nella lingua del nome. |
| `fullName` | Nome completo della persona, nell&#39;ordine scritto più comunemente accettato nella lingua del nome. |
| `lastName` | Ultimo segmento del nome nell’ordine di scrittura più comunemente accettato nella lingua del nome. |
| `middleName` | Nomi intermedi, alternativi o aggiuntivi forniti tra il nome e il cognome. |
| `suffix` | Gruppo di lettere fornito dopo il nome di una persona per fornire informazioni aggiuntive (come `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III` e così via). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati del nome della persona, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
