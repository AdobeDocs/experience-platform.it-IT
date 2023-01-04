---
title: Dettagli dei membri della campagna aziendale XDM Dettagli gruppo di campi di schema
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli membri di Business Campaign XDM.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 5%

---

# [!UICONTROL Dettagli membri della campagna aziendale XDM] gruppo di campi schema

[!UICONTROL Dettagli membri della campagna aziendale XDM] è un gruppo di campi di schema standard per [[!UICONTROL Membri di una campagna aziendale XDM] Classe](../../classes/b2b/business-campaign-members.md), che acquisisce informazioni dettagliate su una campagna aziendale.

![Struttura del gruppo di campi Dettagli membri della campagna aziendale XDM visualizzato nell’interfaccia utente](../../images/field-groups/b2b/business-campaign-member-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | ID composito della campagna che ha acquisito il membro della campagna. |
| `acquiredByCampaignID` | [!UICONTROL Stringa] | Identificatore stringa per la campagna che ha acquisito il membro della campagna. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Una marca temporale ISO 8601 di quando la persona ha risposto per la prima volta alla campagna. |
| `hasReachedSuccess` | [!UICONTROL Booleano] | Indica se il membro della campagna ha dato esito positivo alla conversione. |
| `hasResponded` | [!UICONTROL Booleano] | Indica se il membro della campagna ha risposto alla campagna. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se il membro della campagna è stato eliminato nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi nel Profilo del cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |
| `isExhausted` | [!UICONTROL Booleano] | Indica se il membro della campagna ha esaurito tutte le interazioni della campagna. |
| `lastStatus` | [!UICONTROL Stringa] | Ultimo stato del membro della campagna. |
| `memberStatus` | [!UICONTROL Stringa] | Lo stato corrente del membro della campagna. |
| `memberStatusReason` | [!UICONTROL Stringa] | Motivo dello stato corrente per il membro della campagna. |
| `membershipDate` | [!UICONTROL DateTime] | Motivo dello stato corrente per il membro della campagna. |
| `nurtureCadence` | [!UICONTROL Stringa] | Frequenza temporale per le informazioni relative alla campagna da presentare al membro della campagna. |
| `nurtureTrackName` | [!UICONTROL Stringa] | Nome del programma di nutrizione a cui è soggetto questo membro della campagna. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Timestamp ISO 8601 per quando è stata effettuata una conversione corretta per il membro della campagna. |
| `webinarConfirmationUrl` | [!UICONTROL Stringa] | URL di conferma del webinar per il membro della campagna. |
| `webinarRegistrationID` | [!UICONTROL Stringa] | ID registrazione webinar per il membro della campagna. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
