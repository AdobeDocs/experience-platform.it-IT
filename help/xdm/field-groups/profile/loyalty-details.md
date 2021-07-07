---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli fedeltà;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli fedeltà
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli fedeltà .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---


# [!UICONTROL Gruppo di campi ] Detailsschema fedeltà

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Loyalty Details] is a standard schema field group for the [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo di tipo oggetto, `loyalty`, che acquisisce informazioni relative all&#39;appartenenza di una persona a un programma fedeltà clienti.

![](../../images/field-groups/loyalty-details.png)

| Proprietà | Data type | Descrizione |
| --- | --- | --- |
| `pointsExpiration` | Array di oggetti | Elenca tutti i punti fedeltà (o gruppi di punti fedeltà) che scadranno e le date in cui scadranno. Ogni elemento array deve essere un oggetto contenente le due proprietà seguenti: <ul><li>`pointsExpirationDate`: Un datetime ISO 8601 di quando i punti scadranno.</li><li>`pointsExpiring`: Il saldo a punti che scade alla data di scadenza associata.</li></ul> |
| `joinDate` | DateTime | Un datetime ISO 8601 di quando la persona è entrata nel programma fedeltà. |
| `loyaltyID` | Matrice di stringhe | Represents the loyalty program ID(s) associated with the loyalty program member. |
| `points` | Doppio | Il saldo corrente dei punti fedeltà o dei premi per il membro fedeltà. |
| `pointsRedeemed` | Doppio | L&#39;ammontare dei punti che il membro fedeltà ha applicato a un acquisto o ha riscattato in altro modo. |
| `program` | Stringa | Nome del programma fedeltà in cui la persona è iscritta. |
| `status` | Stringa | Lo stato corrente dell&#39;iscrizione fedeltà della persona, ad esempio `active`, `disabled` o `suspended`. |
| `tier` | Stringa | Captures the loyalty program tier in which the person is enrolled. |
| `upgradeDate` | Stringa | The date when the loyalty member was upgraded to their most recent tier level. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
