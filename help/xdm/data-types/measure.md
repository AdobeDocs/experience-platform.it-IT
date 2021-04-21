---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;misure;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati misura
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Measure Experience Data Model).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---

# [!UICONTROL Measure] tipo di dati

[!UICONTROL Measure] è un tipo di dati XDM (Experience Data Model) standard che contiene un punto dati quantificabile concreto di una particolare metrica. Una misura è composta da un identificatore univoco e da un valore.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `id` | Stringa | Identificatore univoco della misura. Nei casi di raccolta di dati che utilizzano canali di comunicazione con perdita di dati, come applicazioni mobili o siti web con funzionalità offline in cui non è possibile garantire la trasmissione delle misure, questa proprietà contiene un ID univoco generato dal cliente della misura adottata. È buona prassi farlo abbastanza a lungo per garantire una casualità sufficiente. <br><br> Se nella generazione di  `id` sono incorporate informazioni quali timestamp, ID dispositivo, IP, indirizzo MAC o altri valori potenzialmente identificabili dall’utente, il risultato deve essere dotato di hash. Questo assicura che nessun PII sia codificato nel valore, in quanto l&#39;obiettivo non è quello di identificare un utente o un dispositivo, ma la misura specifica nel tempo. |
| `value` | Doppio | Valore quantificabile della misura. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
