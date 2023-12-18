---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;fullName;xdm:fullName;nome persona;nome;tipo dati;tipo dati;tipo dati;
solution: Experience Platform
title: Tipo di dati nome persona
description: Scopri il tipo di dati XDM Nome persona.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# [!UICONTROL Nome della persona] tipo di dati

[!UICONTROL Nome della persona] è un tipo di dati XDM standard che descrive il nome completo di una persona. Poiché le convenzioni per le strutture dei nomi differiscono ampiamente tra le lingue e le culture, i nomi devono sempre essere modellati utilizzando questo tipo di dati.

Inoltre, il tipo di dati fornisce una serie di proprietà facoltative che possono essere utilizzate in situazioni che richiedono l’utilizzo di un solo frammento del nome completo, ad esempio la creazione di un saluto formale o informale.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `courtesyTitle` | Un’abbreviazione del titolo, titolo onorifico o formula introduttiva di una persona (ad esempio `Mr.`, `Miss.`, o `Dr.`). |
| `firstName` | Il primo segmento del nome nell’ordine di scrittura più comunemente accettato nella lingua del nome. |
| `fullName` | Il nome completo della persona, nell’ordine di scrittura più comunemente accettato nella lingua del nome. |
| `lastName` | L’ultimo segmento del nome nell’ordine di scrittura più comunemente accettato nella lingua del nome. |
| `middleName` | Secondi nomi, nomi alternativi o aggiuntivi forniti tra nome e cognome. |
| `suffix` | Gruppo di lettere dopo il nome di una persona per fornire informazioni aggiuntive (ad esempio `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`e così via). |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati del nome della persona, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
