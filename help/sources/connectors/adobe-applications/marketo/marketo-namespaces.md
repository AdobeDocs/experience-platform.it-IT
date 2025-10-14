---
title: Spazi dei nomi e schemi B2B
description: Questo documento fornisce una panoramica degli spazi dei nomi personalizzati necessari per la creazione di un connettore di origine B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 923e56098361b4ef42cbbc2395b748033c0e7b94
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 8%

---

# Spazi dei nomi e schemi B2B

>[!AVAILABILITY]
>
>Devi avere accesso a [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) per i tuoi schemi B2B per qualificarti in [Profilo cliente in tempo reale](../../../../profile/home.md).

>[!NOTE]
>
>Puoi utilizzare i modelli nell’interfaccia utente di Adobe Experience Platform per accelerare la creazione delle risorse per i dati B2B e B2C. Per ulteriori informazioni, consulta la guida su [utilizzo dei modelli nell&#39;interfaccia utente di Experience Platform](../../../tutorials/ui/templates.md).

Leggi questo documento per informazioni sulla configurazione di base per gli spazi dei nomi e gli schemi da utilizzare con origini B2B. Questo documento fornisce anche dettagli sulla configurazione dell’utility di automazione Postman necessaria per generare spazi dei nomi e schemi B2B.

## Configurare gli spazi dei nomi B2B e l’utility di generazione automatica dello schema

>[!IMPORTANT]
>
>Le credenziali dell’account di servizio (JWT) sono diventate obsolete. È necessario assicurarsi di migrare l’applicazione o l’integrazione alla nuova credenziale da server a server OAuth prima del 27 gennaio 2025. Per i passaggi dettagliati su [come eseguire la migrazione delle credenziali JWT alle credenziali da server a server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/), consulta la documentazione seguente.

Per informazioni sui prerequisiti per impostare l&#39;ambiente [!DNL Postman] per il supporto dello spazio dei nomi B2B e dell&#39;utilità di generazione automatica dello schema, fare riferimento alla seguente documentazione.

- È possibile scaricare la raccolta di utilità di generazione automatica dello spazio dei nomi e dello schema e l&#39;ambiente da questo [archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull&#39;utilizzo delle API di Experience Platform, inclusi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida introduttiva [alle API di Experience Platform](../../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API Experience Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md).
- Per informazioni sulla configurazione di [!DNL Postman] per le API di Experience Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../../landing/postman.md).

Con una console per sviluppatori Experience Platform e la configurazione di [!DNL Postman], puoi iniziare ad applicare i valori di ambiente appropriati all&#39;ambiente [!DNL Postman].

La tabella seguente contiene valori di esempio e informazioni aggiuntive sul popolamento dell&#39;ambiente [!DNL Postman]:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificatore univoco utilizzato per generare `{ACCESS_TOKEN}`. Per informazioni su come recuperare [, consulta il tutorial su &#x200B;](../../../../landing/api-authentication.md)autenticazione e accesso alle API di Experience Platform`{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API di Experience Platform. Per informazioni su come recuperare [, consulta il tutorial su &#x200B;](../../../../landing/api-authentication.md)autenticazione e accesso alle API di Experience Platform`{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Il token di autorizzazione necessario per completare le chiamate alle API di Experience Platform. Per informazioni su come recuperare [, consulta il tutorial su &#x200B;](../../../../landing/api-authentication.md)autenticazione e accesso alle API di Experience Platform`{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il contenitore `global` contiene tutte le classi, i gruppi di campi di schema, i tipi di dati e gli schemi standard forniti dai partner Adobe e Experience Platform. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su `global`. | `global` |
| `TECHNICAL_ACCOUNT_ID` | Credenziali utilizzate per l’integrazione in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) fornisce il framework per l’autenticazione nei servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni di [, consulta il tutorial su  [!DNL Postman]](../../../../landing/postman.md)come configurare la console per sviluppatori e `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | ID utilizzato per garantire che le risorse create abbiano lo spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L’endpoint URL a cui stai effettuando chiamate API. Questo valore è fisso ed è sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Esecuzione degli script

Dopo aver configurato la raccolta [!DNL Postman] e l&#39;ambiente, è ora possibile eseguire lo script tramite l&#39;interfaccia [!DNL Postman].

Nell&#39;interfaccia [!DNL Postman], selezionare la cartella principale dell&#39;utilità di generazione automatica, quindi selezionare **[!DNL Run]** dall&#39;intestazione superiore.

![Cartella principale del generatore di spazi dei nomi e schemi nell&#39;interfaccia utente di Postman. &quot;Runs&quot; è evidenziato nella barra dei menu superiore.](../images/marketo/root_folder.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner]. Da qui, assicurarsi che tutte le caselle di controllo siano selezionate, quindi selezionare **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![L&#39;interfaccia Runner dell&#39;interfaccia utente di Postman con diverse richieste nella raccolta di spazi dei nomi e schemi selezionata e il pulsante &quot;Esegui spazi dei nomi e schemi&quot; evidenziato a destra.](../images/marketo/run_generator.png)

In caso di esito positivo, la richiesta crea gli spazi dei nomi e gli schemi necessari per B2B.

## Spazi dei nomi B2B

Gli spazi dei nomi di identità sono un componente di [[!DNL Identity Service]](../../../../identity-service/home.md) che servono a distinguere il contesto di un&#39;identità. Un’identità completa include un valore di identità e uno spazio dei nomi. Per ulteriori informazioni, leggere la [panoramica degli spazi dei nomi](../../../../identity-service/features/namespaces.md).

Gli spazi dei nomi B2B vengono utilizzati nell’identità primaria dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per gli spazi dei nomi B2B.

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Nome visualizzato | Simbolo identità | Tipo di identità |
| --- | --- | --- |
| Persona B2B | `b2b_person` | `CROSS_DEVICE` |
| Account B2B | `b2b_account` | `B2B_ACCOUNT` |
| Opportunità B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relazione persona opportunità B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campagna B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Iscritto campagna B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Elenco di marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Iscritto elenco di marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relazione della persona dell’account B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Schemi B2B

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati.

Prima che i dati possano essere acquisiti in Experience Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedere le [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi B2B.

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Nome dello schema | Classe base | Gruppi di campi | [!DNL Profile] nello schema | Identità primaria | Spazio dei nomi identità primaria | Identità secondaria | Spazio dei nomi dell’identità secondaria | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Account B2B | [Account aziendale XDM](../../../../xdm/classes/b2b/business-account.md) | Dettagli dell’account aziendale XDM | Abilitata | `accountKey.sourceKey` nella classe base | Account B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Account B2B | <ul><li>`accountParentKey.sourceKey` nel gruppo di campi Dettagli account aziendale XDM</li><li>Proprietà di destinazione: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li></ul> |
| Persona B2B | [Profilo individuale XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Dettagli persona aziendale XDM</li><li>Componenti della persona aziendale di XDM</li><li>IdentityMap</li><li>Dettagli di consenso e preferenze</li></ul> | Abilitata | `b2b.personKey.sourceKey` nel gruppo di campi Dettagli persona aziendale XDM | Persona B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` del gruppo di campi Dettagli persona aziendale XDM</li><li>`workEmail.address` del gruppo di campi Dettagli persona aziendale XDM</ol></li> | <ol><li>Persona B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` del gruppo di campi Componenti persona aziendale XDM</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: accountKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Opportunità B2B | [Opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Dettagli sull’opportunità di business XDM | Abilitata | `opportunityKey.sourceKey` nella classe base | Opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Opportunità B2B | <ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione da schema di riferimento: opportunità</li></ul> |
| Relazione persona opportunità B2B | [Relazione della persona dell&#39;opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Nessuna | Abilitata | `opportunityPersonKey.sourceKey` nella classe base | Relazione persona opportunità B2B | | | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: b2b.personKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione da schema di riferimento: opportunità</li></ul>**Seconda relazione**<ul><li>`opportunityKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: opportunità B2B </li><li>Namespace: Opportunità B2B </li><li>Proprietà di destinazione: `opportunityKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Campagna B2B | [Campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign.md) | Dettagli della campagna aziendale XDM | Abilitata | `campaignKey.sourceKey` nella classe base | Campagna B2B | | |
| Iscritto campagna B2B | [Membri della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Dettagli sui membri della campagna aziendale XDM | Abilitata | `ccampaignMemberKey.sourceKey` nella classe base | Iscritto campagna B2B | | | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Campagne</li></ul>**Seconda relazione**<ul><li>`campaignKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: campagna B2B</li><li>Spazio dei nomi: campagna B2B</li><li>Proprietà di destinazione: `campaignKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Campaign</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Elenco di marketing B2B | [Elenco marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Nessuna | Abilitata | `marketingListKey.sourceKey` nella classe base | Elenco di marketing B2B | Nessuna | Nessuna | Nessuna | L&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un&#39;identità secondaria. |
| Iscritto elenco di marketing B2B | [Membri dell&#39;elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Nessuna | Abilitata | `marketingListMemberKey.sourceKey` nella classe base | Iscritto elenco di marketing B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`PersonKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione da schema di riferimento: elenchi di marketing</li></ul>**Seconda relazione**<ul><li>`marketingListKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: elenco di marketing B2B</li><li>Spazio dei nomi: Elenco di marketing B2B</li><li>Proprietà di destinazione: `marketingListKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Elenco marketing</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> | Il membro dell&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un&#39;identità secondaria. |
| Relazione della persona dell’account B2B | [Relazione della persona dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mappa delle identità | Abilitata | `accountPersonKey.sourceKey` nella classe base | Relazione della persona dell’account B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.SourceKey`</li><li>Nome di relazione dallo schema corrente: Persone</li><li>Nome di relazione da schema di riferimento: Account</li></ul>**Seconda relazione**<ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi

Per informazioni su come collegare i dati di [!DNL Marketo] ad Experience Platform, consulta l&#39;esercitazione sulla [creazione di un connettore di origine Marketo nell&#39;interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).

<!--

| B2B Activity | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visit WebPage</li><li>New Lead</li><li>Convert Lead</li><li>Add To List</li><li>Remove From List</li><li>Add To Opportunity</li><li>Remove From Opportunity</li><li>Form Filled Out</li><li>Link Clicks</li><li>Email Delivered</li><li>Email Opened</li><li>Email Clicked</li><li>Email Bounced</li><li>Email Bounced Soft</li><li>Email Unsubscribed</li><li>Score Changed</li><li>Opportunity Updated</li><li>Status in Campaign Progression Changed</li><li>Person Identifier</li><li>Marketo Web URL</li><li>Interesting Moment</li><li>Call Webhook</li><li>Change Campaign Cadence</li><li>Revenue Stage Changed</li><li>Merge Leads</li><li>Email Sent</li><li>Change Campaign Stream</li><li>Add to Campaign</li></ul> | Enabled | `personKey.sourceKey` of Person Identifier field group | B2B Person | None | None | | `ExperienceEvent` is different from entities. The identity of experience event is the person who did the activity. |

-->