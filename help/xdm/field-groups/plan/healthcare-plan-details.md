---
title: Gruppo di campi schema Dettagli piano sanitario
description: Scopri il gruppo di campi schema Dettagli piano sanitario.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL Dettagli piano sanitario] gruppo di campi schema

[!UICONTROL Dettagli piano sanitario] è un gruppo di campi di schema standard per la classe [[!UICONTROL Piano]](../../classes/plan.md). Fornisce un singolo campo di tipo oggetto `healthcarePlanDetails` che acquisisce le proprietà relative a un piano medico.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `networkDetails` | Array di oggetti | Elenca i dettagli della rete o delle reti di fornitori definite dall&#39;assicuratore a cui il beneficiario può chiedere il trattamento e saranno coperte al tasso &quot;in rete&quot;. Ogni oggetto include le seguenti proprietà: <ul><li>`networkID`: (stringa) ID specifico dell&#39;assicuratore per la rete.</li><li>`networkName`: (stringa) il nome specifico dell&#39;assicuratore per la rete.</li></ul> |
| `affiliations` | Array di stringhe | Elenco di entità aziendali affiliate al piano. |
| `coverageType` | Stringa | Tipo di copertura del piano. I valori accettati sono:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booleano | Indica se il piano è attivo. |
| `lastVerificationDate` | Data e ora | Data dell’ultima verifica del piano. |
| `payerID` | Stringa | L’identificativo unico dell’ordinante (in altre parole, il fornitore di assicurazione del piano). |
| `planLevel` | Stringa | Indica il livello del piano. I valori accettati sono:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Stringa | Indica il tipo di piano. I valori accettati sono:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Stringa | Il tipo di proprietario per il quale è stato creato un piano. Alcuni esempi includono singoli utenti, gruppi, organizzazioni e così via. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
