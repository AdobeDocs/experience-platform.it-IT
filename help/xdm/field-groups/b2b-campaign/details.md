---
title: Gruppo di campi dello schema dei dettagli della campagna aziendale XDM
description: Scopri il gruppo di campi dello schema Dettagli campagna aziendale XDM.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL Dettagli campagna aziendale XDM] gruppo di campi schema

[!UICONTROL Dettagli campagna aziendale XDM] è un gruppo di campi di schema standard per la [[!UICONTROL classe della campagna aziendale XDM]](../../classes/b2b/business-campaign.md), che acquisisce informazioni dettagliate su una campagna aziendale.

![Struttura del gruppo di campi Dettagli campagna aziendale XDM come viene visualizzato nell&#39;interfaccia utente](../../images/field-groups/b2b/business-campaign-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Rappresenta il costo reale della campagna aziendale. |
| `budgetedCost` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Rappresenta il costo preventivato della campagna aziendale. |
| `expectedRevenue` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Rappresenta i ricavi che la campagna aziendale deve generare. |
| `parentCampaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | ID composito di una campagna principale, se applicabile. |
| `campaignEndDate` | [!UICONTROL DataOra] | Una marca temporale ISO 8601 che indica quando la campagna è terminata o terminerà. |
| `campaignProgressionName` | [!UICONTROL Stringa] | Il nome della progressione della campagna. |
| `campaignStartDate` | [!UICONTROL DataOra] | Una marca temporale ISO 8601 che indica quando è iniziata o inizierà la campagna. |
| `campaignStatus` | [!UICONTROL Stringa] | Lo stato corrente della campagna. |
| `channelName` | [!UICONTROL Stringa] | Il nome del canale associato a questa campagna. |
| `expectedResponse` | [!UICONTROL Stringa] | Risposta prevista per la campagna. |
| `integrationPartnerName` | [!UICONTROL Stringa] | Il nome del partner che è stato integrato con questa campagna. |
| `isActive` | [!UICONTROL Booleano] | Indica se la campagna è attiva. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se la campagna è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `lastActivityDate` | [!UICONTROL DataOra] | Una marca temporale ISO 8601 dell’ultima attività associata alla campagna. |
| `timeZone` | [!UICONTROL Stringa] | Il fuso orario in cui opera la campagna. |
| `timeZoneDelivery` | [!UICONTROL Stringa] | Il fuso orario di consegna in cui opera la campagna. |
| `timeZoneName` | [!UICONTROL Stringa] | Nome del fuso orario in cui opera la campagna. |
| `webinarHistorySyncDate` | [!UICONTROL DataOra] | Una marca temporale ISO 8601 dell’ultima sincronizzazione della cronologia del webinar per questa campagna. |
| `webinarHistorySyncStatus` | [!UICONTROL Stringa] | Lo stato della sincronizzazione della cronologia del webinar per questa campagna. |
| `webinarSessionDescription` | [!UICONTROL Stringa] | Descrizione della sessione del webinar associata alla campagna. |
| `webinarSessionName` | [!UICONTROL Stringa] | Nome della sessione del webinar associata alla campagna. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
