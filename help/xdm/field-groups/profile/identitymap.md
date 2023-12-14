---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;identityMap;mappa identità;mappa identità;mappa identità;progettazione schema;mappa;mappa;schema;unione;home;popular topic;schema;schema;XDM;individual profile;fields;schemas;schemas;identityMap;identity map;Identity map;schema map;schema;schema;map;map;map;map;union
title: Gruppo di campi dello schema IdentityMap
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: 43b3b79a4d24fd92c7afbf9ca9c83b0cbf80e2c2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL IdentityMap] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo mappa che contiene un set di identità utente basate sullo spazio dei nomi.

![Un diagramma del [!UICONTROL IdentityMap] gruppo di campi schema](../../images/field-groups/identitymap.png)

Consulta la sezione sulle mappe di identità in [nozioni di base sulla composizione dello schema](../../schema/composition.md#identityMap) per ulteriori informazioni sul loro caso d’uso, compresi i vantaggi e gli svantaggi.

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

Per ulteriori dettagli sul gruppo di campi, consulta [schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) nell’archivio XDM pubblico.
