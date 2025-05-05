---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;identityMap;identity map;Identity map;schema;schema;schema;mapping;unione;;home;popular topic;schema;Schema;XDM;individual profile;fields;schemas;schemas;identityMap;identity map;Identity map;Schema design;schema;map;map;map;map;union
title: Gruppo di campi dello schema IdentityMap
description: Scopri la classe Profilo individuale XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# [!UICONTROL Gruppo di campi schema IdentityMap]

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [&#128279;](../name-updates.md).

[!UICONTROL IdentityMap] è un gruppo di campi dello schema standard per la classe [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) e un gruppo di campi compatibile per la classe [[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo mappa che contiene un set di identità utente basate sullo spazio dei nomi.

![Diagramma del gruppo di campi dello schema [!UICONTROL IdentityMap]](../../images/field-groups/identitymap.png)

Consulta la sezione sulle mappe di identità nelle [nozioni di base sulla composizione dello schema](../../schema/composition.md#identityMap) per ulteriori informazioni sul caso d&#39;uso, inclusi i vantaggi e gli svantaggi.

**esempio**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Per ulteriori dettagli sul gruppo di campi, consulta lo [schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) nell&#39;archivio XDM pubblico.
