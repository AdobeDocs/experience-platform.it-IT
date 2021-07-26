---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;dispositivo;commercio;commercio;commercio;
solution: Experience Platform
title: Gruppo di campi schema dettagli commercio dispositivo
topic-legacy: overview
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema Dettagli del commercio dispositivi.
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 4%

---

# [!UICONTROL Gruppo di campi ] Detailsschema di Device Trade-In

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Device Trade-In ] Consente di specificare un gruppo di campi schema standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Fornisce un singolo campo (`deviceTradeInDetails`) che descrive una transazione di trade-in per dispositivi, tra cui valore di trade-in, ID dispositivo originale e nuovo ID dispositivo.

![Struttura dei dettagli di Device Trade-In](../../images/field-groups/device-trade-in-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `tradeInValue` | [Valuta](../../data-types/currency.md) | Il valore del dispositivo oggetto della negoziazione. |
| `newDeviceID` | Stringa | L&#39;ID del nuovo dispositivo per il quale si sta eseguendo la negoziazione. |
| `originalDeviceID` | Stringa | ID del dispositivo oggetto della negoziazione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
