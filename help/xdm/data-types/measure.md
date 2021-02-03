---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;misure;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati misura
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Measure Experience Data Model).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---


# [!UICONTROL Measure] tipo di dati

[!UICONTROL Measure] è un tipo di dati XDM (Experience Data Model) standard che contiene un punto dati quantificabile concreto di una particolare metrica. Una misura è composta da un identificatore univoco e da un valore.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `id` | Stringa | Identificatore univoco della misura. In caso di raccolta di dati tramite canali di comunicazione con perdita di dati, come ad esempio app mobili o siti Web con funzionalità offline in cui non è possibile garantire la trasmissione delle misure, questa proprietà contiene un ID univoco della misura adottata generato dal client. È consigliabile prolungare tale periodo in modo da garantire una casualità sufficiente. <br><br> Se nella generazione del  `id`file vengono incorporate informazioni quali timestamp, ID dispositivo, IP, indirizzi MAC o altri valori potenzialmente identificativi dell&#39;utente, il risultato deve essere hashing. Questo assicura che nessun PII sia codificato nel valore, in quanto l&#39;obiettivo non è identificare un utente o un dispositivo, ma la misura specifica nel tempo. |
| `value` | Doppio | Valore quantificabile della misura. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)