---
title: Gruppo di campi Dettagli prospect partner (esempio)
description: Scopri il gruppo di campi per schema Gruppo di campi Dettagli prospect partner (esempio) (XDM).
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL Dettagli prospect partner (esempio)] gruppo di campi

[!UICONTROL Dettagli prospect partner (esempio)] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). [!UICONTROL Dettagli prospect partner (esempio)] fornisce un framework di esempio per vari dettagli relativi al profilo di un prospect. Questo framework semplifica il processo di organizzazione e gestione di diverse informazioni relative ai potenziali clienti.

Questo gruppo di campi estende la [classe Prospect individuale](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) nel contesto di un partner.

![Diagramma del [!UICONTROL gruppo di campi Dettagli prospect partner (esempio)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | stringa | Fascia di età all’interno della famiglia. |
| [!UICONTROL accessori di abbigliamento] | `apparelAccessories` | stringa | Preferenze o coinvolgimento in abbigliamento/accessori. |
| [!UICONTROL bicicletta] | `bicycling` | stringa | Interesse o partecipazione ad attività di bicicletta. |
| [!UICONTROL cableTv] | `cableTv` | stringa | Indica il coinvolgimento con la televisione via cavo. |
| [!UICONTROL unità domestiche] | `domestics` | stringa | Preferenze o impegno in attività nazionali. |
| [!UICONTROL elettronica] | `electronics` | stringa | Interesse o coinvolgimento in dispositivi elettronici. |
| [!UICONTROL ciboEBevanda] | `foodAndBeverage` | stringa | Preferenze o coinvolgimento in alimenti/bevande. |
| [!UICONTROL calzature] | `footwear` | stringa | Interesse o coinvolgimento in calzature. |
| [!UICONTROL healthFoods] | `healthFoods` | stringa | Preferenze o coinvolgimento negli alimenti per la salute. |
| [!UICONTROL trekking] | `hiking` | stringa | Interesse o partecipazione ad attività escursionistiche. |
| [!UICONTROL familyId] | `householdId` | stringa | Un identificatore univoco della famiglia. |
| [!UICONTROL idIndividuale] | `individualId` | stringa | Un identificatore univoco dell’individuo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | stringa | L’inferenza di essere un titolare della carta. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | stringa | L&#39;inferenza di essere un titolare di carta premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | stringa | Un indicatore del livello corrispondente. |
| [!UICONTROL ValutazioneAcquirente] | `buyerRating` | stringa | Una valutazione relativa al comportamento d’acquisto. |
| [!UICONTROL ValutazioneDonatore] | `donorRating` | stringa | Valutazione relativa al comportamento del donatore. |
| [!UICONTROL ValutazioneInvestimento] | `investmentRating` | stringa | Un rating relativo al comportamento di investimento. |
| [!UICONTROL ValutazioneRisponditore] | `responderRating` | stringa | Una valutazione relativa al comportamento del risponditore. |
| [!UICONTROL VelocitàSpesa] | `spendingVelocity` | stringa | Velocità o tasso di spesa. |
| [!UICONTROL VolumeSpesa] | `spendingVolume` | stringa | Quantità o volume di spesa. |
| [!UICONTROL recordId] | `recordId` | stringa | Un identificatore univoco del record. |
| [!UICONTROL residenceId] | `residenceId` | stringa | Un identificatore univoco della residenza. |
| [!UICONTROL navigazione] | `sailing` | stringa | Indica l’interesse o il coinvolgimento in attività di vela. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | stringa | Indica le preferenze o il coinvolgimento nei prodotti per le vacanze. |
| [!UICONTROL sci] | `skiing` | stringa | Indica l’interesse o il coinvolgimento in attività sciistiche. |
| [!UICONTROL tennis] | `tennis` | stringa | Indica l’interesse o il coinvolgimento in attività di tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | stringa | Indica il coinvolgimento con lo shopping televisivo. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta lo [schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) nell&#39;archivio XDM pubblico.
