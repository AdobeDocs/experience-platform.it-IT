---
title: Gruppo di campi per l’arricchimento dei partner di profilo (esempio)
description: Scopri il gruppo di campi Schema per l’arricchimento dei partner di profilo (esempio).
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---

# [!UICONTROL Arricchimento partner profilo (esempio)] gruppo di campi schema

[!UICONTROL Arricchimento partner profili (esempio)] è un gruppo di campi di schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Utilizza questo gruppo di campi per fornire dati aggiuntivi relativi ad arricchimenti basati sui partner per i profili cliente.

![Diagramma del gruppo di campi ] [!UICONTROL Arricchimento partner profilo (esempio).](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | stringa | La fascia di età all’interno della famiglia. |
| [!UICONTROL accessori di abbigliamento] | `apparelAccessories` | stringa | Dati su abbigliamento e accessori. |
| [!UICONTROL bicicletta] | `bicycling` | stringa | Informazioni relative al ciclismo. |
| [!UICONTROL cableTv] | `cableTv` | stringa | Informazioni relative alla TV via cavo. |
| [!UICONTROL unità domestiche] | `domestics` | stringa | Dati relativi a residenti nazionali. |
| [!UICONTROL elettronica] | `electronics` | stringa | Informazioni relative all’elettronica. |
| [!UICONTROL ciboEBevanda] | `foodAndBeverage` | stringa | Dati su cibi e bevande. |
| [!UICONTROL calzature] | `footwear` | stringa | Informazioni relative alle calzature. |
| [!UICONTROL healthFoods] | `healthFoods` | stringa | Dati sugli alimenti sani. |
| [!UICONTROL trekking] | `hiking` | stringa | Informazioni relative al trekking. |
| [!UICONTROL familyId] | `householdId` | stringa | ID univoco di una famiglia. |
| [!UICONTROL idIndividuale] | `individualId` | stringa | L’ID univoco di un individuo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | stringa | Informazioni dedotte sul titolare della carta. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | stringa | Dettagli del titolare della carta premio dedotti. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | stringa | Dati flag a livello di corrispondenza. |
| [!UICONTROL ValutazioneAcquirente] | `buyerRating` | stringa | Informazioni sulla valutazione dell&#39;acquirente. |
| [!UICONTROL ValutazioneDonatore] | `donorRating` | stringa | Dettagli della valutazione del donatore. |
| [!UICONTROL ValutazioneInvestimento] | `investmentRating` | stringa | Dati di rating degli investimenti. |
| [!UICONTROL ValutazioneRisponditore] | `responderRating` | stringa | Informazioni sulla valutazione del risponditore. |
| [!UICONTROL VelocitàSpesa] | `spendingVelocity` | stringa | Dettagli sulla velocità di spesa. |
| [!UICONTROL VolumeSpesa] | `spendingVolume` | stringa | Informazioni sul volume di spesa. |
| [!UICONTROL recordId] | `recordId` | stringa | Identificatore di record univoco. |
| [!UICONTROL residenceId] | `residenceId` | stringa | ID univoco della residenza. |
| [!UICONTROL navigazione] | `sailing` | stringa | Dati relativi alla navigazione. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | stringa | Informazioni sui prodotti per le vacanze stagionali. |
| [!UICONTROL sci] | `skiing` | stringa | Dati relativi allo sci. |
| [!UICONTROL tennis] | `tennis` | stringa | Informazioni relative al tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | stringa | Informazioni per gli acquirenti di televisori. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta lo [schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) nell&#39;archivio XDM pubblico.
