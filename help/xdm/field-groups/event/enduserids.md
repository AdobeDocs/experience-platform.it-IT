---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;progettazione schema;gruppo di campi;gruppo di campi;enduserids;utente finale;utente finale;id;
solution: Experience Platform
title: Gruppo campi schema dettagli ID utente finale
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli ID utente finale.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---


# [!UICONTROL Gruppo di campi ] Dettagli ID utente finale

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL ID utente finale ] Consente di specificare un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni di identità di un individuo in diverse applicazioni di Adobe. Il gruppo di campi fornisce un oggetto a livello principale `endUserIDs`, che a sua volta contiene un campo di sola lettura `_experience` i cui valori vengono aggiornati automaticamente al momento dell’acquisizione dei dati.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `aacustomid` | [Identità](../../data-types/identity.md) | ID utente finale personalizzati per Adobe Analytics Cloud. |
| `aaid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Analytics Cloud. |
| `acid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Campaign. |
| `adcloud` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Advertising Cloud. |
| `emailid` | [Identità](../../data-types/identity.md) | ID degli indirizzi e-mail. |
| `mcid` | [Identità](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identità](../../data-types/identity.md) | ID dei numeri di telefono. |
| `tntid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Target. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
