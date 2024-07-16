---
title: Spazi dei nomi e schemi B2B
description: Questo documento fornisce una panoramica degli spazi dei nomi personalizzati necessari per la creazione di un connettore di origine B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5e8bb04ca18159eab98b2f7f0bba8cb1488a1f26
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 11%

---

# Spazi dei nomi e schemi B2B

>[!NOTE]
>
>Puoi utilizzare i modelli nell’interfaccia utente di Adobe Experience Platform per accelerare la creazione delle risorse per i dati B2B e B2C. Per ulteriori informazioni, leggere la guida su [utilizzo dei modelli nell&#39;interfaccia utente di Platform](../../../tutorials/ui/templates.md).

Questo documento fornisce informazioni sulla configurazione di base per gli spazi dei nomi e gli schemi da utilizzare con origini B2B. Questo documento fornisce anche dettagli sulla configurazione dell’utility di automazione Postman necessaria per generare spazi dei nomi e schemi B2B.

>[!IMPORTANT]
>
>Devi avere accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) per consentire agli schemi B2B di partecipare a [Real-Time Customer Profile](../../../../profile/home.md).

## Configurare gli spazi dei nomi B2B e l’utility di generazione automatica dello schema

Il primo passaggio nell’utilizzo dello spazio dei nomi B2B e dell’utility di generazione automatica dello schema consiste nell’impostare la console di sviluppo di Platform e l’ambiente [!DNL Postman].

- È possibile scaricare la raccolta di utilità di generazione automatica dello spazio dei nomi e dello schema e l&#39;ambiente da questo [archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull&#39;utilizzo delle API di Platform, inclusi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida introduttiva [alle API di Platform](../../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API di Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md).
- Per informazioni sulla configurazione di [!DNL Postman] per le API di Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../../landing/postman.md).

Con una console per sviluppatori Platform e [!DNL Postman] configurati, puoi iniziare ad applicare i valori di ambiente appropriati all&#39;ambiente [!DNL Postman].

La tabella seguente contiene valori di esempio e informazioni aggiuntive sul popolamento dell&#39;ambiente [!DNL Postman]:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificatore univoco utilizzato per generare `{ACCESS_TOKEN}`. Per informazioni su come recuperare `{CLIENT_SECRET}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md). | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare {ACCESS_TOKEN}. Per informazioni su come generare `{JWT_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md). | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API Experience Platform. Per informazioni su come recuperare `{API_KEY}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Il token di autorizzazione necessario per completare le chiamate alle API Experience Platform. Per informazioni su come recuperare `{ACCESS_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../../landing/api-authentication.md). | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il contenitore `global` contiene tutte le classi, i gruppi di campi dello schema, i tipi di dati e gli schemi standard forniti dal partner Adobe e Experience Platform. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Credenziali utilizzate per autenticare l&#39;istanza [!DNL Postman] in Experience Platform API. Per istruzioni su come recuperare {PRIVATE_KEY}, consulta il tutorial sulla configurazione di Developer Console e [configurazione di Developer Console e [!DNL Postman]](../../../../landing/postman.md). | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziali utilizzate per l&#39;integrazione in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) fornisce il framework per l’autenticazione nei servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni di `{ORG_ID}`, consulta il tutorial su [come configurare la console per sviluppatori e  [!DNL Postman]](../../../../landing/postman.md). | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | ID utilizzato per garantire che le risorse create abbiano lo spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L’endpoint URL a cui stai effettuando chiamate API. Questo valore è fisso ed è sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Esecuzione degli script

Dopo aver configurato la raccolta [!DNL Postman] e l&#39;ambiente, è ora possibile eseguire lo script tramite l&#39;interfaccia [!DNL Postman].

Nell&#39;interfaccia [!DNL Postman], selezionare la cartella principale dell&#39;utilità di generazione automatica, quindi selezionare **[!DNL Run]** dall&#39;intestazione superiore.

![cartella-radice](../images/marketo/root-folder.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner]. Da qui, assicurarsi che tutte le caselle di controllo siano selezionate, quindi selezionare **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

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

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedere le [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi B2B.

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Nome dello schema | Classe base | Gruppi di campi | [!DNL Profile] nello schema | Identità primaria | Spazio dei nomi dell’identità primaria | Identità secondaria | Spazio dei nomi dell’identità secondaria | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Account B2B | [Account aziendale XDM](../../../../xdm/classes/b2b/business-account.md) | Dettagli dell’account aziendale XDM | Abilitata | `accountKey.sourceKey` nella classe base | Account B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Account B2B | <ul><li>`accountParentKey.sourceKey` nel gruppo di campi Dettagli account aziendale XDM</li><li>Proprietà di destinazione: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li></ul> |
| Persona B2B | [Profilo individuale XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Dettagli persona aziendale XDM</li><li>Componenti della persona aziendale di XDM</li><li>IdentityMap</li><li>Dettagli di consenso e preferenze</li></ul> | Abilitata | `b2b.personKey.sourceKey` nel gruppo di campi Dettagli persona aziendale XDM | Persona B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` del gruppo di campi Dettagli persona aziendale XDM</li><li>`workEmail.address` del gruppo di campi Dettagli persona aziendale XDM</ol></li> | <ol><li>Persona B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` del gruppo di campi Componenti persona aziendale XDM</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: accountKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Opportunità B2B | [Opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Dettagli sull’opportunità di business XDM | Abilitata | `opportunityKey.sourceKey` nella classe base | Opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Opportunità B2B | <ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione da schema di riferimento: opportunità</li></ul> |
| Relazione persona opportunità B2B | [Relazione della persona dell&#39;opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Nessuna | Abilitata | `opportunityPersonKey.sourceKey` nella classe base | Relazione persona opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Relazione persona opportunità B2B | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: b2b.personKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione da schema di riferimento: opportunità</li></ul>**Seconda relazione**<ul><li>`opportunityKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: opportunità B2B </li><li>Namespace: Opportunità B2B </li><li>Proprietà di destinazione: `opportunityKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Campagna B2B | [Campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign.md) | Dettagli della campagna aziendale XDM | Abilitata | `campaignKey.sourceKey` nella classe base | Campagna B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Campagna B2B |
| Iscritto campagna B2B | [Membri della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Dettagli sui membri della campagna aziendale XDM | Abilitata | `ccampaignMemberKey.sourceKey` nella classe base | Iscritto campagna B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Iscritto campagna B2B | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Campagne</li></ul>**Seconda relazione**<ul><li>`campaignKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: campagna B2B</li><li>Spazio dei nomi: campagna B2B</li><li>Proprietà di destinazione: `campaignKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Campaign</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Elenco di marketing B2B | [Elenco marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Nessuna | Abilitata | `marketingListKey.sourceKey` nella classe base | Elenco di marketing B2B | Nessuna | Nessuna | Nessuna | L&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un&#39;identità secondaria. |
| Iscritto elenco di marketing B2B | [Membri dell&#39;elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Nessuna | Abilitata | `marketingListMemberKey.sourceKey` nella classe base | Iscritto elenco di marketing B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`PersonKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione da schema di riferimento: elenchi di marketing</li></ul>**Seconda relazione**<ul><li>`marketingListKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: elenco di marketing B2B</li><li>Spazio dei nomi: Elenco di marketing B2B</li><li>Proprietà di destinazione: `marketingListKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Elenco marketing</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> | Il membro dell&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un&#39;identità secondaria. |
| Attività B2B | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visita pagina Web</li><li>Nuovo lead</li><li>Conversione lead</li><li>Aggiunta all’elenco</li><li>Rimozione dall’elenco</li><li>Aggiunta all’opportunità</li><li>Rimozione dall’opportunità</li><li>Modulo compilato</li><li>Clic sui link</li><li>E-mail consegnata</li><li>E-mail aperta</li><li>Clic effettuato sull’e-mail</li><li>E-mail non recapitata</li><li>E-mail non recapitata temporaneamente</li><li>Iscrizione all’e-mail annullata</li><li>Punteggio modificato</li><li>Opportunità aggiornata</li><li>Stato nella progressione della campagna modificato</li><li>Identificatore della persona</li><li>URL web Marketo</li><li>Momento di interesse</li><li>Chiama webhook</li><li>Modifica cadenza campagna</li><li>Fase ricavi modificata</li><li>Unisci lead</li><li>E-mail inviata</li><li>Modifica flusso campagna</li><li>Aggiungi a campagna</li></ul> | Abilitata | `personKey.sourceKey` del gruppo di campi Identificatore persona | Persona B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>Campo `listOperations.listKey.sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: elenco di marketing B2B</li><li>Spazio dei nomi: Elenco di marketing B2B</li></ul>**Seconda relazione**<ul><li>Campo `opportunityEvent.opportunityKey.sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: opportunità B2B</li><li>Namespace: Opportunità B2B</li></ul>**Terza relazione**<ul><li>Campo `leadOperation.campaignProgression.campaignKey.sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: campagna B2B</li><li>Spazio dei nomi: campagna B2B</li></ul> | `ExperienceEvent` è diverso dalle entità. L’identità dell’evento esperienza è la persona che ha eseguito l’attività. |
| Relazione della persona dell’account B2B | [Relazione della persona dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mappa delle identità | Abilitata | `accountPersonKey.sourceKey` nella classe base | Relazione della persona dell’account B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.SourceKey`</li><li>Nome di relazione dallo schema corrente: Persone</li><li>Nome di relazione da schema di riferimento: Account</li></ul>**Seconda relazione**<ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi

Per informazioni su come collegare i dati di [!DNL Marketo] a Platform, consulta l&#39;esercitazione su [creazione di un connettore di origine Marketo nell&#39;interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
