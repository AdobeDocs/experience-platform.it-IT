---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;iab;tcf;consent;
solution: Experience Platform
title: Gruppo di campi per il consenso IAB TCF 2.0 per gli schemi evento
description: Questo documento fornisce una panoramica del gruppo di campi Schema di consenso IAB TCF 2.0 per la classe XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# [!UICONTROL Consenso IAB TCF 2.0] gruppo di campi per gli schemi evento

>[!IMPORTANT]
>
>Questo documento descrive [!UICONTROL Consenso IAB TCF 2.0] gruppo di campi dello schema per la classe ExperienceEvent XDM. Questo gruppo di campi deve essere utilizzato solo se desideri tenere traccia degli eventi di modifica del consenso nel tempo.
>
>Tieni presente che i valori del consenso registrati nei dati dell’evento non vengono rispettati nei flussi di lavoro di applicazione automatica. Affinché l’applicazione automatica possa avvenire, i valori del consenso devono essere acquisiti nella classe Profilo individuale XDM e abilitati per Profilo cliente in tempo reale.
>
>Per il gruppo di campi previsto per la classe Profilo individuale XDM, fai riferimento a quanto segue [documento](../profile/iab.md) invece.

[!UICONTROL Consenso IAB TCF 2.0] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzato per acquisire una serie con marca temporale di stringhe di consenso IAB, al fine di monitorare i modelli di modifica del consenso nel tempo.

![](../../images/field-groups/iab-event.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `consentStrings` | Array di [Stringhe di consenso](../../data-types/consent-string.md) | Array di valori stringa di consenso associati all’evento. |

{style="table-layout:auto"}

Consulta la guida su [Supporto IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) per ulteriori informazioni sul caso d’uso di questo gruppo di campi. Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
