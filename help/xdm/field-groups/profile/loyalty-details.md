---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli fedeltà;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli fedeltà
description: Scopri il gruppo di campi dello schema Dettagli fedeltà.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL Dettagli fedeltà] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Dettagli fedeltà] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo di tipo oggetto, `loyalty`, che acquisisce informazioni relative all&#39;appartenenza di una persona a un programma fedeltà clienti.

![](../../images/field-groups/loyalty-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `pointsExpiration` | Array di oggetti | Elenca eventuali punti fedeltà (o gruppi di punti fedeltà) che scadranno e le date in cui scadranno. Ogni elemento array deve essere un oggetto contenente le due proprietà seguenti: <ul><li>`pointsExpirationDate`: data/ora ISO 8601 di scadenza dei punti.</li><li>`pointsExpiring`: il saldo in punti che scade alla data di scadenza associata.</li></ul> |
| `joinDate` | Data e ora | Data e ora ISO 8601 del momento in cui la persona ha aderito al programma fedeltà. |
| `loyaltyID` | Array di stringhe | Rappresenta gli ID programma fedeltà associati al membro del programma fedeltà. |
| `points` | Doppio | Il saldo corrente di punti o premi fedeltà per il membro fedeltà. |
| `pointsRedeemed` | Doppio | L’importo dei punti che il membro fedeltà ha applicato a un acquisto o ha in altro modo rimborsato. |
| `program` | Stringa | Il nome del programma fedeltà a cui la persona è iscritta. |
| `status` | Stringa | Lo stato corrente dell&#39;iscrizione fedeltà della persona, ad esempio `active`, `disabled` o `suspended`. |
| `tier` | Stringa | Acquisisce il livello del programma fedeltà a cui la persona è iscritta. |
| `upgradeDate` | Stringa | La data in cui il membro fedeltà è stato aggiornato al livello più recente. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
