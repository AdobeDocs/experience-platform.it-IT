---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;dispositivo;commercio;commercio;commercio;
solution: Experience Platform
title: Gruppo di campi schema dettagli commercio dispositivo
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema Dettagli del commercio dispositivi.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 5%

---

# [!UICONTROL Dettagli sul trasferimento dei dispositivi] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli sul trasferimento dei dispositivi] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Fornisce un singolo campo (`deviceTradeInDetails`) che descrive una transazione di accesso ai dispositivi, tra cui valore di accesso, ID dispositivo originale e nuovo ID dispositivo.

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
