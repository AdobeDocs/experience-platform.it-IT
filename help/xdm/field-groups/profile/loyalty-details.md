---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli fedeltà;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli fedeltà
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli fedeltà.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---

# [!UICONTROL Dettagli fedeltà] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli fedeltà] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo di tipo oggetto, `loyalty`, che acquisisce informazioni relative all’iscrizione di una persona a un programma di fidelizzazione dei clienti.

![](../../images/field-groups/loyalty-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `pointsExpiration` | Array di oggetti | Elenca eventuali punti fedeltà (o gruppi di punti fedeltà) che scadranno e le date in cui scadranno. Ogni elemento array deve essere un oggetto contenente le due proprietà seguenti: <ul><li>`pointsExpirationDate`: data/ora ISO 8601 della scadenza dei punti.</li><li>`pointsExpiring`: il saldo in punti in scadenza alla data di scadenza associata.</li></ul> |
| `joinDate` | DateTime | Data e ora ISO 8601 del momento in cui la persona ha aderito al programma fedeltà. |
| `loyaltyID` | Array di stringhe | Rappresenta gli ID programma fedeltà associati al membro del programma fedeltà. |
| `points` | Doppio | Il saldo corrente di punti o premi fedeltà per il membro fedeltà. |
| `pointsRedeemed` | Doppio | L’importo dei punti che il membro fedeltà ha applicato a un acquisto o ha in altro modo rimborsato. |
| `program` | Stringa | Il nome del programma fedeltà a cui la persona è iscritta. |
| `status` | Stringa | Lo stato corrente dell’iscrizione fedeltà della persona, ad esempio `active`, `disabled`, o `suspended`. |
| `tier` | Stringa | Acquisisce il livello del programma fedeltà a cui la persona è iscritta. |
| `upgradeDate` | Stringa | La data in cui il membro fedeltà è stato aggiornato al livello più recente. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
