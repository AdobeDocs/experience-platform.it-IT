---
keywords: Experience Platform;home;argomenti comuni;connettore sorgente Marketo;spazi dei nomi;schemi
solution: Experience Platform
title: 'namespace Marketo '
topic-legacy: overview
description: Questo documento fornisce una panoramica dei namespace personalizzati necessari per la creazione di un connettore di origine del Marketo Engage.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 3%

---


# (Beta) [!DNL Marketo Engage] spazi dei nomi e schemi

>[!IMPORTANT]
>
>La sorgente [!DNL Marketo Engage] è attualmente in versione beta. La funzione e la documentazione sono soggette a modifica.

Il presente documento fornisce informazioni sulla configurazione sottostante per i namespace e gli schemi B2B utilizzati con [!DNL Marketo Engage] (in seguito denominati &quot;[!DNL Marketo]&quot;). Questo documento fornisce anche dettagli sulla configurazione dell&#39;utility di automazione Postman necessaria per generare [!DNL Marketo] spazi dei nomi e schemi B2B.

## Prerequisiti

Prima di poter generare i namespace e gli schemi B2B, è necessario impostare la console per sviluppatori di Platform e l’ambiente [!DNL Postman] . Per ulteriori informazioni, consulta l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../../landing/postman.md).

Con una console per sviluppatori Platform e una [!DNL Postman] configurazione, applica le seguenti variabili all’ambiente [!DNL Marketo] :

| Variabile di ambiente | Valore di esempio | Note |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Per ulteriori informazioni, consulta l’esercitazione sull’ [autenticazione di [!DNL Marketo] instance](./marketo-auth.md) . |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione, consulta la seguente [[!DNL Salesforce] guida](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) . |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione, consulta la seguente [[!DNL Microsoft Dynamics] guida](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) . |
| `has_abm` | `false` | Questo valore è impostato su `true` se sei iscritto a Marketing basato su account. |
| `has_msi` | `false` | Questo valore è impostato su `true` se sei iscritto a [!DNL Marketo Sales Insight]. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] spazi dei nomi

Gli spazi dei nomi di identità sono un componente di [[!DNL Identity Service]](../../../../identity-service/home.md) che fungono da indicatori del contesto a cui si riferisce un’identità.

Un&#39;identità completa include un valore ID e uno spazio dei nomi. È necessario un nuovo namespace personalizzato per ogni nuova istanza [!DNL Marketo] e combinazione di set di dati. Ad esempio, un connettore di origine [!DNL Marketo] che acquisisce il set di dati `programs` richiede un proprio spazio dei nomi personalizzato, mentre un altro connettore di origine Marketo che acquisisce lo stesso set di dati richiede anche il proprio nuovo spazio dei nomi personalizzato. Per ulteriori informazioni, consulta la [panoramica dei namespace](../../../../identity-service/namespaces.md) .

Lo spazio dei nomi [!DNL Marketo] viene utilizzato nell’identità principale dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per i namespace [!DNL Marketo].

| Nome visualizzato | Simbolo di identità | Tipo di identità | Tipo di emittente | Tipo di entità emittente | Esempio di ID Munchkin |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | generato automaticamente | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | generato automaticamente | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | generato automaticamente | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | generato automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | generato automaticamente | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | generato automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | generato automaticamente | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | generato automaticamente | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | generato automaticamente | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] spazi dei nomi

Se l’utente è iscritto all’integrazione [!DNL Salesforce], lo spazio dei nomi [!DNL Salesforce] viene utilizzato nell’identità secondaria dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per i namespace [!DNL Salesforce].

| Nome visualizzato | Simbolo di identità | Tipo di identità | Tipo di emittente | Tipo di entità emittente | [!DNL Salesforce] esempio di ID organizzazione sottoscrizione |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] spazi dei nomi

Se sei iscritto all’integrazione [!DNL Dynamics], lo spazio dei nomi [!DNL Dynamics] viene utilizzato come identità secondaria dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per i namespace [!DNL Dynamics].

| Nome visualizzato | Simbolo di identità | Tipo di identità | Tipo di emittente | Tipo di entità emittente | [!DNL Salesforce] esempio di ID organizzazione sottoscrizione |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | generato automaticamente | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | generato automaticamente | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | generato automaticamente | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | generato automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | generato automaticamente | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | generato automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] schemi

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che può essere contenuto all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più mixin.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta le [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi [!DNL Marketo].

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome dello schema | Classe base | Mixins | Identità principale | Spazio dei nomi identità principale | Identità secondaria | Spazio dei nomi identità secondario | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Società {MUNCHKIN_ID} | Account aziendale XDM | Dettagli account aziendale XDM | `accountID` nella classe base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` nel mixin Dettagli account aziendale XDM</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Società Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Persona {MUNCHKIN_ID} | Profilo individuale XDM | <ul><li>Dettagli sulle persone aziendali XDM</li><li>Componenti per Business Person XDM</li></ul> | `personID` nella classe base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` del mixaggio Dettagli persona commerciale XDM</li><li>`workEmail.address` del mixaggio Dettagli persona commerciale XDM</li><li>`identityMap` del mixin Identity Map</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-mail</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` del mixaggio dei componenti XDM Business Person</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Società Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `accountID`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| [!DNL Marketo] Opportunità {MUNCHKIN_ID} | Opportunità aziendali XDM | Dettagli opportunità di business XDM | `opportunityID` nella classe base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Società Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `accountID`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul> |
| [!DNL Marketo] Ruolo contatto opportunità {MUNCHKIN_ID} | Relazione personale opportunità di business XDM | Nessuna | `opportunityPersonID` nella classe base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Prima relazione<ul><li>`personID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Persona Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `personID`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul>Seconda relazione<ul><li>`opportunityID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Opportunità Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `opportunityID`</li><li>Nome di relazione dallo schema corrente: Opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| [!DNL Marketo] Programma {MUNCHKIN_ID} | Campagna aziendale XDM | Dettagli della campagna aziendale XDM | `campaignID` nella classe base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Membro del programma {MUNCHKIN_ID} | Membro della campagna aziendale XDM | Dettagli membri della campagna aziendale XDM | `campaignMemberID` nella classe base | `marketo_program_member_{MUNCHKIN_ID}` | Nessuna | Nessuna | Prima relazione<ul><li>`personID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Persona Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `personID`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Programmi</li></ul>Seconda relazione<ul><li>`campaignID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Programma Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: campaignID</li><li>Nome di relazione dallo schema corrente: Programma</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| [!DNL Marketo] Elenco statico {MUNCHKIN_ID} | Elenco di marketing aziendale XDM | Nessuna | `marketingListID` nella classe base | `marketo_static_list_{MUNCHKIN_ID}` | Nessuna | Nessuna | Nessuna | L’elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un’identità secondaria |
| [!DNL Marketo] Membro elenco statico {MUNCHKIN_ID} | Membri elenco marketing commerciale XDM | Nessuna | `marketingListMemberID` nella classe base | `marketo_static_list_member_{MUNCHKIN_ID}` | Nessuna | Nessuna | Prima relazione<ul><li>`personID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Persona Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `personID`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Elenchi</li></ul>Seconda relazione<ul><li>`marketingListID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Elenco statico Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `marketingListID`</li><li>Nome di relazione dallo schema corrente: Elenco</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| [!DNL Marketo] Account denominato {MUNCHKIN_ID} | Account aziendale XDM | Dettagli account aziendale XDM | `accountID` nella classe base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` nel mixin Dettagli account aziendale XDM</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Account Marketo denominato {MUNCHKIN_ID}</li><li>Namespace: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Attività {MUNCHKIN ID} | Evento esperienza XDM | <ul><li>Visita WebPage</li><li>Nuovo lead</li><li>Converti lead</li><li>Aggiungi all’elenco</li><li>Rimuovi da elenco</li><li>Aggiungi a opportunità</li><li>Rimuovi da opportunità</li><li>Modulo compilato</li><li>Clic sui collegamenti</li><li>E-mail consegnata</li><li>E-mail aperta</li><li>E-mail selezionata</li><li>E-mail rimbalzata</li><li>E-mail - Soft rimbalzato</li><li>E-mail annullata</li><li>Punteggio modificato</li><li>Opportunità aggiornata</li><li>Stato in progressione campagna modificato</li><li>Identificatore persona</li><li>URL web Marketo | `personID` del mixin dell’identificatore di persona | marketo_person_{MUNCHKIN_ID} | Nessuna | Nessuna | Prima relazione<ul><li>`listOperations.listID` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Elenco statico Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Seconda relazione<ul><li>`opportunityEvent.opportunityID` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Opportunità Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Terza relazione<ul><li>`leadOperation.campaignProgression.campaignID` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Programma Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Tutti gli schemi sono abilitati per [!DNL Real-time Customer Profile]

## Passaggi successivi

Per informazioni su come collegare i dati [!DNL Marketo] a Platform, consulta l’esercitazione su [creazione di un connettore sorgente Marketo nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).