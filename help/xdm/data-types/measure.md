---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;misura;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Misura tipo di dati
description: Scopri il tipo di dati Misura Experience Data Model (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# Tipo di dati [!UICONTROL Measure]

[!UICONTROL Measure] è un tipo di dati XDM (Experience Data Model) standard che contiene un punto dati quantificabile concreto di una particolare metrica. Una misura è composta da un identificatore univoco e da un valore.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `id` | Stringa | L’identificatore univoco di questa misura. Nei casi in cui la raccolta dei dati utilizzi canali di comunicazione con perdita di dati, come app mobili o siti web con funzionalità offline in cui non è possibile garantire la trasmissione delle misure, questa proprietà contiene un ID univoco generato dal cliente della misura adottata. È buona prassi prolungare tale periodo in modo da garantire una sufficiente casualità. <br><br> Se informazioni quali timestamp, ID dispositivo, IP, indirizzo MAC o altri valori potenzialmente identificativi dell&#39;utente sono inclusi nella generazione di `id`, il risultato deve essere sottoposto a hashing. In questo modo, nel valore non viene codificata alcuna PII, in quanto l’obiettivo non è quello di identificare un utente o un dispositivo, ma la misura specifica nel tempo. |
| `value` | Doppio | Il valore quantificabile di questa misura. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
