---
title: Dettagli del piano sanitario Schema Field Group
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli piano sanitario.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---

# [!UICONTROL Dettagli sul piano sanitario] gruppo di campi schema

[!UICONTROL Dettagli sul piano sanitario] è un gruppo di campi di schema standard per [[!UICONTROL Pianificare] Classe](../../classes/plan.md). Fornisce un singolo campo di tipo oggetto `healthcarePlanDetails` che acquisisce proprietà correlate a un piano medico.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `networkDetails` | Array di oggetti | Elenca i dettagli della rete o delle reti definite dall&#39;assicuratore dei fornitori ai quali il beneficiario può chiedere un trattamento e sarà coperto al tasso &quot;in rete&quot;. Ogni oggetto include le seguenti proprietà: <ul><li>`networkID`: (Stringa) L&#39;ID specifico dell&#39;assicuratore per la rete.</li><li>`networkName`: (Stringa) Nome specifico dell&#39;assicuratore per la rete.</li></ul> |
| `affiliations` | Matrice di stringhe | Un elenco di entità aziendali collegate al piano. |
| `coverageType` | Stringa | Tipo di copertura del piano. I valori accettati sono:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booleano | Indica se il piano è attivo. |
| `lastVerificationDate` | DateTime | Data dell&#39;ultima verifica del piano. |
| `payerID` | Stringa | Identificatore univoco del pagatore (in altre parole, il fornitore di assicurazione del piano). |
| `planLevel` | Stringa | Indica il livello del piano. I valori accettati sono:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Stringa | Indica il tipo di piano. I valori accettati sono:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Stringa | Il tipo di proprietario per il quale è previsto un piano. Gli esempi includono singoli utenti, gruppi, organizzazioni e così via. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
