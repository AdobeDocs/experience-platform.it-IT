---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli fedeltà;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli fedeltà
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli fedeltà .
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---

# [!UICONTROL Dettagli fedeltà] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli fedeltà] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo di tipo oggetto, `loyalty`, che acquisisce informazioni relative all’appartenenza di una persona a un programma fedeltà clienti.

![](../../images/field-groups/loyalty-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `pointsExpiration` | Array di oggetti | Elenca tutti i punti fedeltà (o gruppi di punti fedeltà) che scadranno e le date in cui scadranno. Ogni elemento array deve essere un oggetto contenente le due proprietà seguenti: <ul><li>`pointsExpirationDate`: Un datetime ISO 8601 di quando i punti scadranno.</li><li>`pointsExpiring`: Il saldo a punti che scade alla data di scadenza associata.</li></ul> |
| `joinDate` | DateTime | Un datetime ISO 8601 di quando la persona è entrata nel programma fedeltà. |
| `loyaltyID` | Matrice di stringhe | Rappresenta gli ID del programma fedeltà associati al membro del programma fedeltà. |
| `points` | Doppio | Il saldo corrente dei punti fedeltà o dei premi per il membro fedeltà. |
| `pointsRedeemed` | Doppio | L&#39;ammontare dei punti che il membro fedeltà ha applicato a un acquisto o ha riscattato in altro modo. |
| `program` | Stringa | Nome del programma fedeltà in cui la persona è iscritta. |
| `status` | Stringa | Lo stato attuale dell&#39;iscrizione fedeltà della persona, ad esempio `active`, `disabled`oppure `suspended`. |
| `tier` | Stringa | Acquisisce il livello del programma fedeltà in cui la persona è iscritta. |
| `upgradeDate` | Stringa | Data in cui il membro fedeltà è stato aggiornato al livello di livello più recente. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
