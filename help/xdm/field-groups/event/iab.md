---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;progettazione schema;gruppo di campi;gruppo di campi;iab;tcf;consenso;
solution: Experience Platform
title: Gruppo di campi dello schema di consenso IAB TCF 2.0
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema di consenso IAB TCF 2.0 per la classe ExperienceEvent XDM.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# [!UICONTROL Gruppo di campi ] dello schema di consenso IAB TCF 2.0

>[!IMPORTANT]
>
>Questo documento copre il gruppo di campi dello schema [!UICONTROL IAB TCF 2.0 Consent] per la classe ExperienceEvent XDM. Utilizzare questo gruppo di campi solo se si intende tenere traccia degli eventi di modifica del consenso nel tempo.
>
>I valori di consenso registrati nei dati dell’evento non vengono rispettati nei flussi di lavoro di implementazione automatica. Affinché l’applicazione automatica avvenga, i valori di consenso devono essere acquisiti nella classe Profilo individuale XDM e attivati per il profilo cliente in tempo reale.
>
>Per il gruppo di campi destinato alla classe Profilo individuale XDM, fare riferimento al seguente [documento](../profile/iab.md).

[!UICONTROL Il ] consenso IAB TCF 2.0 è un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe utilizzata per acquisire le stringhe di consenso IAB di una serie con marca temporale, al fine di tenere traccia dei pattern di modifica del consenso nel tempo.

![](../../images/field-groups/iab-event.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `consentStrings` | Array di [stringhe di consenso](../../data-types/consent-string.md) | Matrice di valori stringa di consenso associati all&#39;evento. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sul caso d’uso di questo gruppo di campi, consulta la guida sul supporto di [IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) . Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
