---
title: Gruppo di campi per l’arricchimento dei partner di profilo (esempio)
description: Scopri il gruppo di campi Schema per l’arricchimento dei partner di profilo (esempio).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 13%

---


# [!UICONTROL Arricchimento dei partner di profilo (esempio)] gruppo di campi schema

[!UICONTROL Arricchimento dei partner di profilo (esempio)] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Utilizza questo gruppo di campi per fornire dati aggiuntivi relativi ad arricchimenti basati sui partner per i profili cliente.

![Un diagramma del [!UICONTROL Arricchimento dei partner di profilo (esempio)] gruppo di campi.](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | La fascia di età all’interno della famiglia. |
| [!UICONTROL abbigliamentoAccessori] | `apparelAccessories` | string | Dati su abbigliamento e accessori. |
| [!UICONTROL ciclismo] | `bicycling` | string | Informazioni relative al ciclismo. |
| [!UICONTROL cableTv] | `cableTv` | string | Informazioni relative alla TV via cavo. |
| [!UICONTROL domestiche] | `domestics` | string | Dati relativi a residenti nazionali. |
| [!UICONTROL elettronica] | `electronics` | string | Informazioni relative all’elettronica. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Dati su cibi e bevande. |
| [!UICONTROL calzature] | `footwear` | string | Informazioni relative alle calzature. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Dati sugli alimenti sani. |
| [!UICONTROL trekking] | `hiking` | string | Informazioni relative al trekking. |
| [!UICONTROL familyId] | `householdId` | string | ID univoco di una famiglia. |
| [!UICONTROL individualId] | `individualId` | string | L’ID univoco di un individuo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | Informazioni dedotte sul titolare della carta. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | string | Dettagli del titolare della carta premio dedotti. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | Dati flag a livello di corrispondenza. |
| [!UICONTROL BuyerRating] | `buyerRating` | string | Informazioni sulla valutazione dell&#39;acquirente. |
| [!UICONTROL ValutazioneDonatore] | `donorRating` | string | Dettagli della valutazione del donatore. |
| [!UICONTROL InvestmentRating] | `investmentRating` | string | Dati di rating degli investimenti. |
| [!UICONTROL ResponderRating] | `responderRating` | string | Informazioni sulla valutazione del risponditore. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | string | Dettagli sulla velocità di spesa. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | string | Informazioni sul volume di spesa. |
| [!UICONTROL recordId] | `recordId` | string | Identificatore di record univoco. |
| [!UICONTROL residenceId] | `residenceId` | string | ID univoco della residenza. |
| [!UICONTROL vela] | `sailing` | string | Dati relativi alla navigazione. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | string | Informazioni sui prodotti per le vacanze stagionali. |
| [!UICONTROL sci] | `skiing` | string | Dati relativi allo sci. |
| [!UICONTROL tennis] | `tennis` | string | Informazioni relative al tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Informazioni per gli acquirenti di televisori. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) sull’archivio XDM pubblico.
