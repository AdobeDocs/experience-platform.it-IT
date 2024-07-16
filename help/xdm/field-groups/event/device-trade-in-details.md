---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;schema design;gruppo di campi;gruppo di campi;dispositivo;permuta;trade-in;trade in;
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli di permuta del dispositivo
description: Scopri il gruppo di campi schema Dettagli permuta dispositivo.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# [!UICONTROL Dettagli permuta dispositivo] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Device Trade-In Details] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Fornisce un singolo campo (`deviceTradeInDetails`) che descrive una transazione di permuta del dispositivo, incluso il valore di permuta, l&#39;ID dispositivo originale e l&#39;ID nuovo dispositivo.

![Struttura dei dettagli sulla permuta dei dispositivi](../../images/field-groups/device-trade-in-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `tradeInValue` | [Valuta](../../data-types/currency.md) | Il valore del dispositivo di cui viene effettuata la permuta. |
| `newDeviceID` | Stringa | ID del nuovo dispositivo per cui viene effettuata la permuta. |
| `originalDeviceID` | Stringa | ID del dispositivo di cui viene effettuata la permuta. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
