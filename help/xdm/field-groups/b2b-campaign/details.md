---
title: Gruppo campi schema dettagli campagna aziendale XDM
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli campagna aziendale XDM.
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 5%

---

# [!UICONTROL Dettagli della campagna aziendale XDM] gruppo di campi schema

[!UICONTROL Dettagli della campagna aziendale XDM] è un gruppo di campi di schema standard per [[!UICONTROL Campagna aziendale XDM] Classe](../../classes/b2b/business-campaign.md), che acquisisce informazioni dettagliate su una campagna aziendale.

![Struttura del gruppo di campi Dettagli campagna aziendale XDM visualizzato nell’interfaccia utente](../../images/field-groups/b2b/business-campaign-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Rappresenta il costo reale della campagna aziendale. |
| `budgetedCost` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Rappresenta il costo preventivato della campagna aziendale. |
| `expectedRevenue` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Rappresenta i ricavi che la campagna aziendale deve generare. |
| `parentCampaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | ID composito per una campagna principale, se applicabile. |
| `campaignEndDate` | [!UICONTROL DateTime] | La marca temporale ISO 8601 indica quando la campagna è terminata o terminerà. |
| `campaignProgressionName` | [!UICONTROL Stringa] | Nome della progressione della campagna. |
| `campaignStartDate` | [!UICONTROL DateTime] | La marca temporale ISO 8601 indica quando la campagna è iniziata o verrà avviata. |
| `campaignStatus` | [!UICONTROL Stringa] | Lo stato corrente della campagna. |
| `channelName` | [!UICONTROL Stringa] | Nome del canale associato alla campagna. |
| `expectedResponse` | [!UICONTROL Stringa] | Risposta prevista per la campagna. |
| `integrationPartnerName` | [!UICONTROL Stringa] | Nome del partner che si è integrato con questa campagna. |
| `isActive` | [!UICONTROL Booleano] | Indica se la campagna è attiva. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se la campagna è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi in Profilo cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |
| `lastActivityDate` | [!UICONTROL DateTime] | Timestamp ISO 8601 dell’ultima attività associata alla campagna. |
| `timeZone` | [!UICONTROL Stringa] | Il fuso orario in cui opera la campagna. |
| `timeZoneDelivery` | [!UICONTROL Stringa] | Il fuso orario di consegna in cui opera la campagna. |
| `timeZoneName` | [!UICONTROL Stringa] | Nome del fuso orario in cui opera la campagna. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Timestamp ISO 8601 dell&#39;ultima sincronizzazione della cronologia del webinar per questa campagna. |
| `webinarHistorySyncStatus` | [!UICONTROL Stringa] | Lo stato della sincronizzazione della cronologia del webinar per questa campagna. |
| `webinarSessionDescription` | [!UICONTROL Stringa] | Una descrizione della sessione del webinar associata a questa campagna. |
| `webinarSessionName` | [!UICONTROL Stringa] | Nome della sessione del webinar associata a questa campagna. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
