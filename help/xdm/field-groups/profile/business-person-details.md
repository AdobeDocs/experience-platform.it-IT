---
title: Gruppo di campi di schema Dettagli persona aziendale XDM
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli persona commerciale XDM.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 57370e4ed0807bcebf30c73af629671b5390d90d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 4%

---

# [!UICONTROL XDM Business Person ] Detailsschema field group (Beta)

>[!IMPORTANT]
>
>Questo gruppo di campi è disponibile come parte di Real-time Customer Data Platform B2B Edition, attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!UICONTROL Business Person XDM ] Consente di specificare un gruppo di campi di schema standard per la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe che acquisisce informazioni su una persona nel contesto di un&#39;azienda business-to-business (B2B).

![](../../images/field-groups/business-person-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `b2b` | Oggetto | Un oggetto che acquisisce i dettagli specifici di B2B sulla persona. |
| `b2b.accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per il conto commerciale relativo alla persona. |
| `b2b.convertedContactKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per il contatto associato se il lead è stato convertito. |
| `b2b.personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona o il frammento di profilo. |
| `b2b.accountID` | Stringa | Un ID univoco per l&#39;account aziendale a cui questa persona è associata. |
| `b2b.blockedCause` | Stringa | Se la persona è bloccata, questa proprietà ne fornisce il motivo. |
| `b2b.convertedContactID` | Stringa | ID contatto se il lead è stato convertito correttamente. |
| `b2b.convertedDate` | DateTime | La data di conversione se il lead è stato convertito correttamente. |
| `b2b.isBlocked` | Booleano | Indica se la persona è bloccata. |
| `b2b.isConverted` | Booleano | Indica se il lead viene convertito. |
| `b2b.isMarketingSuspended` | Booleano | Indica se il marketing è sospeso per la persona. |
| `b2b.marketingSuspendedCause` | Stringa | Se il marketing è sospeso per la persona, questa proprietà ne fornisce il motivo. |
| `b2b.personGroupID` | Stringa | Identificatore di gruppo per la persona. |
| `b2b.personScore` | Doppio | Punteggio generato per la persona da un sistema CRM. |
| `b2b.personSource` | Stringa | Origine da cui sono state ricevute le informazioni della persona. |
| `b2b.personStatus` | Stringa | Lo stato attuale di marketing o vendite della persona. |
| `b2b.personType` | Stringa | Tipo di persona B2B. |
| `extSourceSystemAudit` | [Attributi di controllo del sistema di origine esterna](../../data-types/external-source-system-audit-attributes.md) | Se la relazione uomo-lavoro proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `extendedWorkDetails` | Oggetto | Acquisisce ulteriori dettagli relativi al lavoro relativi alla persona. |
| `extendedWorkDetails.assistantDetails` | Oggetto | Acquisisce i seguenti attributi relativi all’assistente della persona: <ul><li>`name`: ([Nome persona](../../data-types/person-name.md)) Nome completo dell’assistente.</li><li>`phone`: ([Numero di telefono](../../data-types/phone-number.md)) Il numero di telefono dell&#39;assistente.</li></ul> |
| `extendedWorkDetails.departments` | Matrice di stringhe | Elenco dei nomi dei reparti in cui la persona lavora. |
| `extendedWorkDetails.jobTitle` | Stringa | Titolo del lavoro della persona. |
| `extendedWorkDetails.photoUrl` | Stringa | URL di una foto della persona. |
| `extendedWorkDetails.reportsToID` | Stringa | Identificatore per il responsabile rapporti della persona. |
| `faxPhone` | [Numero di telefono](../../data-types/phone-number.md) | Il numero di fax della persona. |
| `homeAddress` | [Indirizzo postale](../../data-types/postal-address.md) | L&#39;indirizzo di casa della persona. |
| `homePhone` | [Numero di telefono](../../data-types/phone-number.md) | Il numero di telefono di casa della persona. |
| `mobilePhone` | [Numero di telefono](../../data-types/phone-number.md) | Il numero di cellulare della persona. |
| `otherAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Indirizzo alternativo della persona. |
| `otherPhone` | [Numero di telefono](../../data-types/phone-number.md) | Un numero di telefono alternativo per la persona. |
| `person` | [Persona](../../data-types/person.md) | Un singolo attore, contatto o proprietario. |
| `personalEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Indirizzo e-mail personale della persona. |
| `workAddress` | [Indirizzo postale](../../data-types/postal-address.md) | L&#39;indirizzo di lavoro della persona. |
| `workEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Indirizzo e-mail aziendale della persona. |
| `workPhone` | [Numero di telefono](../../data-types/phone-number.md) | Il numero di telefono del lavoro della persona. |
| `identityMap` | Mappa | Campo mappa contenente un set di identità con spazi dei nomi per la persona. Questo campo viene aggiornato automaticamente dal sistema durante l’acquisizione dei dati di identità. Per utilizzare correttamente questo campo per [Profilo cliente in tempo reale](../../../profile/home.md), non tentare di aggiornare manualmente il contenuto del campo nelle operazioni sui dati.<br /><br />Per ulteriori informazioni sul relativo caso d’uso, consulta la sezione sulle mappe di identità nelle  [nozioni di base sulla ](../../schema/composition.md#identityMap) composizione degli schemi . |
| `organizations` | Matrice di stringhe | Un elenco di nomi di organizzazioni in cui la persona lavora. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
