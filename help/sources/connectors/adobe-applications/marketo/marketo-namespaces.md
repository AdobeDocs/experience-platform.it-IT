---
keywords: Experience Platform;home;argomenti comuni;connettore sorgente Marketo;spazi dei nomi;schemi
solution: Experience Platform
title: namespace Marketo
topic-legacy: overview
description: Questo documento fornisce una panoramica dei namespace personalizzati necessari per la creazione di un connettore di origine del Marketo Engage.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: af728fb508c514db3d5871114f9a406c1ed428f2
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 3%

---

# (Beta) [!DNL Marketo Engage] spazi dei nomi e schemi

>[!IMPORTANT]
>
>La sorgente [!DNL Marketo Engage] è attualmente in versione beta. La funzione e la documentazione sono soggette a modifica.

Il presente documento fornisce informazioni sulla configurazione sottostante per i namespace e gli schemi B2B utilizzati con [!DNL Marketo Engage] (in seguito denominati &quot;[!DNL Marketo]&quot;). Questo documento fornisce anche dettagli sulla configurazione dell&#39;utility di automazione Postman necessaria per generare [!DNL Marketo] spazi dei nomi e schemi B2B.

## Imposta l&#39;utilità di generazione automatica dello spazio dei nomi [!DNL Marketo] e dello schema

Il primo passaggio nell’utilizzo dell’utility di generazione automatica dello spazio dei nomi e dello schema [!DNL Marketo] è quello di configurare la console per sviluppatori di Platform e l’ambiente [!DNL Postman] .

- Puoi scaricare lo spazio dei nomi e lo schema per la raccolta e l&#39;ambiente di utilità di generazione automatica da questo [archivio GitHub](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility).
- Per informazioni sull’utilizzo delle API di Platform, compresi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API di Platform, consulta l’esercitazione sull’ [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md).
- Per informazioni su come impostare [!DNL Postman] per le API di Platform, consulta l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../../landing/postman.md).

Con una console per sviluppatori Platform e [!DNL Postman] configurata, ora puoi iniziare ad applicare i valori di ambiente appropriati all’ambiente [!DNL Postman].

La tabella seguente contiene valori di esempio e informazioni aggiuntive sulla compilazione dell&#39;ambiente [!DNL Postman] :

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificatore univoco utilizzato per generare il `{ACCESS_TOKEN}`. Per informazioni su come recuperare le `{CLIENT_SECRET}`, consulta l’esercitazione sull’ [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md) . | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare il tuo {ACCESS_TOKEN}. Per informazioni su come generare le `{JWT_TOKEN}`, consulta l’esercitazione sull’ [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md) . | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API di Experience Platform. Per informazioni su come recuperare le `{API_KEY}`, consulta l’esercitazione sull’ [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md) . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Token di autorizzazione necessario per completare le chiamate alle API di Experience Platform. Per informazioni su come recuperare le `{ACCESS_TOKEN}`, consulta l’esercitazione sull’ [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md) . | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso e sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il contenitore `global` contiene tutte le classi, i gruppi di campi di schema, i tipi di dati e gli schemi standard forniti dal partner di Adobe e Experience Platform. Per quanto riguarda [!DNL Marketo], questo valore è fisso e viene sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Credenziale utilizzata per autenticare l’istanza [!DNL Postman] alle API di Experience Platform. Per istruzioni su come recuperare {PRIVATE_KEY}, consulta l’esercitazione sulla configurazione della console per sviluppatori e [configurazione della console per sviluppatori e  [!DNL Postman]](../../../../landing/postman.md) . | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziale utilizzata per l’integrazione con Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Il sistema Identity Management (IMS) fornisce il framework per l’autenticazione ai servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Un&#39;entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni su `{IMS_ORG}`, consulta l’esercitazione su [configurazione della console per sviluppatori e [!DNL Postman]](../../../../landing/postman.md) . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | Un ID utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L&#39;endpoint URL a cui si effettua la chiamata API. Questo valore è fisso e viene sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | L&#39;ID univoco del tuo account [!DNL Marketo]. Per informazioni su come recuperare il `munchkinId`, consulta l’esercitazione sull’ [autenticazione dell’ [!DNL Marketo] istanza](./marketo-auth.md) . | `123-ABC-456` |
| `sfdc_org_id` | L&#39;ID organizzazione del tuo account [!DNL Salesforce]. Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione [!DNL Salesforce], consulta la seguente [[!DNL Salesforce] guida](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) . | `00D4W000000FgYJUA0` |
| `msd_org_id` | L&#39;ID organizzazione del tuo account [!DNL Dynamics]. Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione [!DNL Dynamics], consulta la seguente [[!DNL Microsoft Dynamics] guida](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) . | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Un valore booleano che indica se sei abbonato a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Un valore booleano che indica se sei iscritto a [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Esecuzione degli script

Con la raccolta [!DNL Postman] e l&#39;ambiente impostati, ora puoi eseguire lo script tramite l&#39;interfaccia [!DNL Postman].

Nell&#39;interfaccia [!DNL Postman], seleziona la cartella principale dell&#39;utilità di generazione automatica e seleziona **[!DNL Run]** dall&#39;intestazione superiore.

![cartella principale](../images/marketo/root-folder.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner]. Da qui, accertati che tutte le caselle di controllo siano selezionate e quindi seleziona **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**.

![generatore di corrente](../images/marketo/run-generator.png)

Una richiesta corretta crea i namespace e gli schemi B2B in base alle specifiche beta.

## [!DNL Marketo] spazi dei nomi

Gli spazi dei nomi di identità sono un componente di [[!DNL Identity Service]](../../../../identity-service/home.md) che fungono da indicatori del contesto a cui si riferisce un’identità.

Un&#39;identità completa include un valore ID e uno spazio dei nomi. È necessario un nuovo namespace personalizzato per ogni nuova istanza [!DNL Marketo] e combinazione di set di dati. Ad esempio, un connettore di origine [!DNL Marketo] che acquisisce il set di dati `programs` richiede un proprio spazio dei nomi personalizzato, mentre un altro connettore di origine Marketo che acquisisce lo stesso set di dati richiede anche il proprio nuovo spazio dei nomi personalizzato. Per ulteriori informazioni, consulta la [panoramica dei namespace](../../../../identity-service/namespaces.md) .

Lo spazio dei nomi [!DNL Marketo] viene utilizzato nell’identità principale dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per i namespace [!DNL Marketo].

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

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

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome visualizzato | Simbolo di identità | Tipo di identità | Tipo di emittente | Tipo di entità emittente | [!DNL Salesforce] esempio di ID organizzazione sottoscrizione |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | generato automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] spazi dei nomi

Se sei iscritto all’integrazione [!DNL Dynamics], lo spazio dei nomi [!DNL Dynamics] viene utilizzato come identità secondaria dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per i namespace [!DNL Dynamics].

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome visualizzato | Simbolo di identità | Tipo di identità | Tipo di emittente | Tipo di entità emittente | [!DNL Dynamics] esempio di ID organizzazione sottoscrizione |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | generato automaticamente | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | generato automaticamente | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | generato automaticamente | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | generato automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | generato automaticamente | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | generato automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] schemi

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che può essere contenuto all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi dello schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta le [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi [!DNL Marketo].

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome dello schema | Classe base | Gruppi di campi | [!DNL Profile] in Schema | Identità principale | Spazio dei nomi identità principale | Identità secondaria | Spazio dei nomi identità secondario | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | Account aziendale XDM | Dettagli account aziendale XDM | Abilitata | `accountID` nella classe base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` nel gruppo di campi Dettagli account business XDM</li><li>Tipo: uno a uno</li><li>Schema di riferimento: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | Profilo individuale XDM | <ul><li>Dettagli sulle persone aziendali XDM</li><li>Componenti per Business Person XDM</li><li>IdentityMap</li></ul> | Abilitata | `personID` nella classe base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` Gruppo di campi Dettagli persona commerciale XDM</li><li>`workEmail.address` Gruppo di campi Dettagli persona commerciale XDM</li><li>`identityMap` del gruppo di campi Identity Map</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-mail</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` Gruppo di campi Componenti Business Person XDM</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `accountID`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | Opportunità aziendali XDM | Dettagli opportunità di business XDM | Abilitata | `opportunityID` nella classe base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `accountID`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | Relazione personale opportunità di business XDM | Nessuna | Abilitata | `opportunityPersonID` nella classe base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Prima relazione<ul><li>`personID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `personID`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul>Seconda relazione<ul><li>`opportunityID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `opportunityID`</li><li>Nome di relazione dallo schema corrente: Opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | Campagna aziendale XDM | Dettagli della campagna aziendale XDM | Abilitata | `campaignID` nella classe base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | Membro della campagna aziendale XDM | Dettagli membri della campagna aziendale XDM | Abilitata | `campaignMemberID` nella classe base | `marketo_program_member_{MUNCHKIN_ID}` | Nessuna | Nessuna | Prima relazione<ul><li>`personID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Persona Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `personID`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Programmi</li></ul>Seconda relazione<ul><li>`campaignID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `campaignID`</li><li>Nome di relazione dallo schema corrente: Programma</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | Elenco di marketing aziendale XDM | Nessuna | Abilitata | `marketingListID` nella classe base | `marketo_static_list_{MUNCHKIN_ID}` | Nessuna | Nessuna | Nessuna | L’elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un’identità secondaria. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | Membri elenco marketing commerciale XDM | Nessuna | Abilitata | `marketingListMemberID` nella classe base | `marketo_static_list_member_{MUNCHKIN_ID}` | Nessuna | Nessuna | Prima relazione<ul><li>`personID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `personID`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Elenchi</li></ul>Seconda relazione<ul><li>`marketingListID` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Proprietà di destinazione: `marketingListID`</li><li>Nome di relazione dallo schema corrente: Elenco</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> | Il membro dell’elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un’identità secondaria. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | Account aziendale XDM | Dettagli account aziendale XDM | Abilitata | `accountID` nella classe base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` nella classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` nel gruppo di campi Dettagli account business XDM</li><li>Tipo: uno a uno</li><li>Schema di riferimento: `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Namespace: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Attività `{MUNCHKIN ID}` | ExperienceEvent XDM | <ul><li>Visita WebPage</li><li>Nuovo lead</li><li>Converti lead</li><li>Aggiungi all’elenco</li><li>Rimuovi da elenco</li><li>Aggiungi a opportunità</li><li>Rimuovi da opportunità</li><li>Modulo compilato</li><li>Clic sui collegamenti</li><li>E-mail consegnata</li><li>E-mail aperta</li><li>E-mail selezionata</li><li>E-mail rimbalzata</li><li>E-mail - Soft rimbalzato</li><li>E-mail annullata</li><li>Punteggio modificato</li><li>Opportunità aggiornata</li><li>Stato in progressione campagna modificato</li><li>Identificatore persona</li><li>URL web Marketo | Abilitata | `personID` del gruppo di campi ID persona | `marketo_person_{MUNCHKIN_ID}` | Nessuna | Nessuna | Prima relazione<ul><li>`listOperations.listID` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Seconda relazione<ul><li>`opportunityEvent.opportunityID` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Terza relazione<ul><li>`leadOperation.campaignProgression.campaignID` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li></ul> | L&#39;identità principale dello schema `[!DNL Marketo] Activity {MUNCHKIN_ID}` è `personID`, che è la stessa dell&#39;identità principale dello schema `[!DNL Marketo] Person {MUNCHKIN_ID}`. |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Per informazioni su come collegare i dati [!DNL Marketo] a Platform, consulta l’esercitazione su [creazione di un connettore sorgente Marketo nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
