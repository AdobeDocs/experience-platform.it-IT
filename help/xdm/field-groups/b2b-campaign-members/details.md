---
title: Gruppo di campi dello schema dei dettagli dei membri della campagna aziendale XDM
description: Scopri il gruppo di campi schema Dettagli membro della campagna aziendale XDM.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# [!UICONTROL Dettagli membri della campagna aziendale XDM] gruppo di campi dello schema

[!UICONTROL Dettagli membri della campagna aziendale XDM] è un gruppo di campi di schema standard per la [[!UICONTROL classe &#x200B;] membri della campagna aziendale XDM](../../classes/b2b/business-campaign-members.md), che acquisisce informazioni dettagliate su una campagna aziendale.

![Struttura del gruppo di campi Dettagli membri della campagna aziendale XDM come viene visualizzato nell&#39;interfaccia utente](../../images/field-groups/b2b/business-campaign-member-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | ID composito della campagna che ha acquisito questo membro della campagna. |
| `acquiredByCampaignID` | [!UICONTROL Stringa] | Un identificatore stringa per la campagna che ha acquisito questo membro della campagna. |
| `firstRespondedDate` | [!UICONTROL DataOra] | Una marca temporale ISO 8601 indicante quando la persona ha risposto per la prima volta alla campagna. |
| `hasReachedSuccess` | [!UICONTROL Booleano] | Indica se il membro della campagna ha generato una conversione riuscita. |
| `hasResponded` | [!UICONTROL Booleano] | Indica se il membro della campagna ha risposto alla campagna. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se il membro della campagna è stato eliminato nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `isExhausted` | [!UICONTROL Booleano] | Indica se il membro della campagna ha esaurito tutte le interazioni della campagna. |
| `lastStatus` | [!UICONTROL Stringa] | Ultimo stato del membro della campagna. |
| `memberStatus` | [!UICONTROL Stringa] | Lo stato corrente del membro della campagna. |
| `memberStatusReason` | [!UICONTROL Stringa] | Motivo dello stato corrente del membro della campagna. |
| `membershipDate` | [!UICONTROL DataOra] | Motivo dello stato corrente del membro della campagna. |
| `nurtureCadence` | [!UICONTROL Stringa] | La frequenza con cui le informazioni relative alla campagna devono essere presentate al membro della campagna. |
| `nurtureTrackName` | [!UICONTROL Stringa] | Il nome del programma di sviluppo a cui è soggetto il membro della campagna. |
| `reachedSuccessDate` | [!UICONTROL DataOra] | Una marca temporale ISO 8601 per indicare quando è stata effettuata una conversione corretta per il membro della campagna. |
| `webinarConfirmationUrl` | [!UICONTROL Stringa] | L’URL di conferma del webinar per il membro della campagna. |
| `webinarRegistrationID` | [!UICONTROL Stringa] | ID di registrazione del webinar per il membro della campagna. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
