---
title: Gruppo di campi Dettagli prospect partner (esempio)
description: Scopri il gruppo di campi per schema Gruppo di campi Dettagli prospect partner (esempio) (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL Dettagli prospect partner (esempio)] gruppo di campi

[!UICONTROL Dettagli prospect partner (esempio)] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il [!UICONTROL Dettagli prospect partner (esempio)] fornisce un framework di esempio per vari dettagli relativi al profilo di un potenziale cliente. Questo framework semplifica il processo di organizzazione e gestione di diverse informazioni relative ai potenziali clienti.

Questo gruppo di campi estende [Classe Prospect Profile individuale](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) nel contesto di un partner.

![Un diagramma del [!UICONTROL Dettagli prospect partner (esempio)] gruppo di campi.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | Fascia di età all’interno della famiglia. |
| [!UICONTROL abbigliamentoAccessori] | `apparelAccessories` | string | Preferenze o coinvolgimento in abbigliamento/accessori. |
| [!UICONTROL ciclismo] | `bicycling` | string | Interesse o partecipazione ad attività di bicicletta. |
| [!UICONTROL cableTv] | `cableTv` | string | Indica il coinvolgimento con la televisione via cavo. |
| [!UICONTROL domestiche] | `domestics` | string | Preferenze o impegno in attività nazionali. |
| [!UICONTROL elettronica] | `electronics` | string | Interesse o coinvolgimento in dispositivi elettronici. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Preferenze o coinvolgimento in alimenti/bevande. |
| [!UICONTROL calzature] | `footwear` | string | Interesse o coinvolgimento in calzature. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Preferenze o coinvolgimento negli alimenti per la salute. |
| [!UICONTROL trekking] | `hiking` | string | Interesse o partecipazione ad attività escursionistiche. |
| [!UICONTROL familyId] | `householdId` | string | Un identificatore univoco della famiglia. |
| [!UICONTROL individualId] | `individualId` | string | Un identificatore univoco dell’individuo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | L’inferenza di essere un titolare della carta. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | string | L&#39;inferenza di essere un titolare di carta premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | Un indicatore del livello corrispondente. |
| [!UICONTROL BuyerRating] | `buyerRating` | string | Una valutazione relativa al comportamento d’acquisto. |
| [!UICONTROL ValutazioneDonatore] | `donorRating` | string | Valutazione relativa al comportamento del donatore. |
| [!UICONTROL InvestmentRating] | `investmentRating` | string | Un rating relativo al comportamento di investimento. |
| [!UICONTROL ResponderRating] | `responderRating` | string | Una valutazione relativa al comportamento del risponditore. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | string | Velocità o tasso di spesa. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | string | Quantità o volume di spesa. |
| [!UICONTROL recordId] | `recordId` | string | Identificatore univoco del record. |
| [!UICONTROL residenceId] | `residenceId` | string | Un identificatore univoco della residenza. |
| [!UICONTROL vela] | `sailing` | string | Indica l’interesse o il coinvolgimento in attività di vela. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | string | Indica le preferenze o il coinvolgimento nei prodotti per le vacanze. |
| [!UICONTROL sci] | `skiing` | string | Indica l’interesse o il coinvolgimento in attività sciistiche. |
| [!UICONTROL tennis] | `tennis` | string | Indica l’interesse o il coinvolgimento in attività di tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Indica il coinvolgimento con lo shopping televisivo. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) sull’archivio XDM pubblico.
