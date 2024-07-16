---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;iab;tcf;consent;
solution: Experience Platform
title: Gruppo di campi per il consenso IAB TCF 2.0 per gli schemi evento
description: Scopri il gruppo di campi Schema di consenso IAB TCF 2.0 per la classe XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0 Consenso] gruppo di campi per schemi evento

>[!IMPORTANT]
>
>Questo documento descrive il gruppo di campi dello schema [!UICONTROL Consenso IAB TCF 2.0] per la classe XDM ExperienceEvent. Questo gruppo di campi deve essere utilizzato solo se desideri tenere traccia degli eventi di modifica del consenso nel tempo.
>
>Tieni presente che i valori del consenso registrati nei dati dell’evento non vengono rispettati nei flussi di lavoro di applicazione automatica. Affinché l’applicazione automatica possa avvenire, i valori del consenso devono essere acquisiti nella classe Profilo individuale XDM e abilitati per Profilo cliente in tempo reale.
>
>Per il gruppo di campi previsto per la classe Profilo individuale XDM, fai riferimento al seguente [documento](../profile/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzata per acquisire una serie di stringhe di consenso IAB con marca temporale, al fine di monitorare i modelli di modifica del consenso nel tempo.

![](../../images/field-groups/iab-event.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `consentStrings` | Array di [stringhe di consenso](../../data-types/consent-string.md) | Array di valori stringa di consenso associati all’evento. |

{style="table-layout:auto"}

Per ulteriori informazioni sul caso d&#39;uso di questo gruppo di campi, consulta la guida sul supporto di [IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md). Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
