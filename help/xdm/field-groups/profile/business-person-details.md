---
title: Gruppo di campi dello schema dei dettagli della persona aziendale XDM
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli persona aziendale XDM.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL Dettagli persona aziendale XDM] gruppo di campi schema

[!UICONTROL Dettagli persona aziendale XDM] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) che acquisisce informazioni su una singola persona nel contesto di un’azienda business-to-business (B2B).

![](../../images/field-groups/business-person-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `b2b` | Oggetto | Oggetto che acquisisce i dettagli specifici di B2B sulla persona. |
| `b2b.accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Un identificatore composito per l’account aziendale relativo alla persona. |
| `b2b.convertedContactKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito del contatto associato se il lead è stato convertito. |
| `b2b.personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona o il frammento di profilo. |
| `b2b.accountID` | Stringa | Un ID univoco per l’account aziendale a cui è associata questa persona. |
| `b2b.blockedCause` | Stringa | Se la persona è bloccata, questa proprietà fornisce il motivo. |
| `b2b.convertedContactID` | Stringa | ID del contatto se il lead è stato convertito correttamente. |
| `b2b.convertedDate` | DateTime | Data di conversione se il lead è stato convertito correttamente. |
| `b2b.isBlocked` | Booleano | Indica se la persona è bloccata. |
| `b2b.isConverted` | Booleano | Indica se il lead viene convertito. |
| `b2b.isMarketingSuspended` | Booleano | Indica se il marketing è sospeso per la persona. |
| `b2b.marketingSuspendedCause` | Stringa | Se il marketing viene sospeso per la persona, questa proprietà fornisce il motivo. |
| `b2b.personGroupID` | Stringa | Un identificatore di gruppo della persona. |
| `b2b.personScore` | Doppio | Un punteggio generato per la persona da un sistema di gestione delle relazioni con i clienti. |
| `b2b.personSource` | Stringa | Origine da cui sono state ricevute le informazioni della persona. |
| `b2b.personStatus` | Stringa | Lo stato attuale di marketing o di vendita della persona. |
| `b2b.personType` | Stringa | Il tipo di persona B2B. |
| `extSourceSystemAudit` | [Attributi di controllo del sistema di sorgente esterna](../../data-types/external-source-system-audit-attributes.md) | Se la relazione della persona aziendale proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `extendedWorkDetails` | Oggetto | Acquisisce ulteriori dettagli relativi al lavoro sulla persona. |
| `extendedWorkDetails.assistantDetails` | Oggetto | Acquisisce i seguenti attributi relativi all’assistente della persona: <ul><li>`name`: ([Nome della persona](../../data-types/person-name.md)) Nome e cognome dell&#39;assistente.</li><li>`phone`: ([Numero di telefono](../../data-types/phone-number.md)) Il numero di telefono dell&#39;assistente.</li></ul> |
| `extendedWorkDetails.departments` | Array di stringhe | Un elenco dei nomi dei reparti in cui lavora la persona. |
| `extendedWorkDetails.jobTitle` | Stringa | Qualifica della persona. |
| `extendedWorkDetails.photoUrl` | Stringa | URL di una foto della persona. |
| `extendedWorkDetails.reportsToID` | Stringa | Identificatore per il manager della persona responsabile della generazione rapporti. |
| `faxPhone` | [Numero di telefono](../../data-types/phone-number.md) | Numero di fax della persona. |
| `homeAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Indirizzo dell&#39;abitazione della persona. |
| `homePhone` | [Numero di telefono](../../data-types/phone-number.md) | Numero di telefono dell&#39;abitazione della persona. |
| `mobilePhone` | [Numero di telefono](../../data-types/phone-number.md) | Numero di telefono cellulare della persona. |
| `otherAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Indirizzo alternativo della persona. |
| `otherPhone` | [Numero di telefono](../../data-types/phone-number.md) | Numero di telefono alternativo della persona. |
| `person` | [Persona](../../data-types/person.md) | Un singolo attore, contatto o proprietario. |
| `personalEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Indirizzo e-mail personale della persona. |
| `workAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Indirizzo aziendale della persona. |
| `workEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Indirizzo e-mail aziendale della persona. |
| `workPhone` | [Numero di telefono](../../data-types/phone-number.md) | Numero di telefono aziendale della persona. |
| `identityMap` | Mappa | Campo mappa che contiene un set di identità con spazio dei nomi per la persona. Questo campo viene aggiornato automaticamente dal sistema durante l’acquisizione dei dati di identità. Per utilizzare correttamente questo campo per [Profilo cliente in tempo reale](../../../profile/home.md), non tentare di aggiornare manualmente il contenuto del campo nelle operazioni sui dati.<br /><br />Consulta la sezione sulle mappe di identità in [nozioni di base sulla composizione dello schema](../../schema/composition.md#identityMap) per ulteriori informazioni sul caso d’uso. |
| `isDeleted` | Booleano | Indica se questa persona è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati in Real-Time Customer Profile. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `organizations` | Array di stringhe | Elenco di nomi di organizzazioni in cui lavora la persona. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
