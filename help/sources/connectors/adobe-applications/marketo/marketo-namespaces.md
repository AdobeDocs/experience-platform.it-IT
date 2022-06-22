---
keywords: Experience Platform;home;argomenti popolari;connettore sorgente Marketo;spazi dei nomi;schemi;b2b;B2B
solution: Experience Platform
title: namespace e schemi B2B
topic-legacy: overview
description: Questo documento fornisce una panoramica dei namespace personalizzati necessari per la creazione di un connettore sorgente B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 9640124bd8fb8b7d069d433369468f8bdb57871b
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 2%

---

# namespace e schemi B2B

Questo documento fornisce informazioni sull&#39;impostazione sottostante per i namespace e gli schemi da utilizzare con le origini B2B. Questo documento fornisce inoltre dettagli sull&#39;impostazione dell&#39;utility di automazione Postman necessaria per la generazione di spazi dei nomi e schemi B2B.

>[!IMPORTANT]
>
>Devi avere accesso a [Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) affinché gli schemi B2B partecipino [Profilo cliente in tempo reale](../../../../profile/home.md).

## Imposta spazi dei nomi B2B e utilità di generazione automatica dello schema

Il primo passaggio nell’utilizzo dello spazio dei nomi B2B e dell’utility di generazione automatica dello schema è quello di configurare la console per sviluppatori di Platform e [!DNL Postman] ambiente.

- È possibile scaricare lo spazio dei nomi e lo schema di generazione automatica dell&#39;utilità raccolta e l&#39;ambiente da questo [Archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull’utilizzo delle API di Platform, compresi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida su [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API di Platform, consulta l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md).
- Per informazioni su come impostare [!DNL Postman] per le API di Platform, consulta l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../../landing/postman.md).

Con una console per sviluppatori Platform e [!DNL Postman] è ora possibile iniziare ad applicare i valori di ambiente appropriati al [!DNL Postman] ambiente.

La tabella seguente contiene valori di esempio e informazioni aggiuntive sulla compilazione [!DNL Postman] ambiente:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Un identificatore univoco utilizzato per generare il `{ACCESS_TOKEN}`. Guarda l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md) per informazioni su come recuperare `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare il tuo {ACCESS_TOKEN}. Guarda l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md) per informazioni su come generare il `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API di Experience Platform. Guarda l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md) per informazioni su come recuperare `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Token di autorizzazione necessario per completare le chiamate alle API di Experience Platform. Guarda l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../../landing/api-authentication.md) per informazioni su come recuperare `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso e viene sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | La `global` Il contenitore contiene tutte le classi standard fornite dal partner di Adobe e Experience Platform, i gruppi di campi di schema, i tipi di dati e gli schemi. Per quanto riguarda [!DNL Marketo], questo valore è fisso e viene sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Credenziale utilizzata per autenticare il [!DNL Postman] istanza alle API di Experience Platform. Consulta l’esercitazione sulla configurazione di Developer Console e [configurazione di Developer Console e [!DNL Postman]](../../../../landing/postman.md) per istruzioni su come recuperare il tuo {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziale utilizzata per l’integrazione con Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Il sistema Identity Management (IMS) fornisce il framework per l’autenticazione ai servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso e viene sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Un&#39;entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Guarda l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../../landing/postman.md) per istruzioni su come recuperare `{ORG_ID}` informazioni. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | Un ID utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L&#39;endpoint URL a cui si effettua la chiamata API. Questo valore è fisso e viene sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### Esecuzione degli script

Con il tuo [!DNL Postman] insieme e configurazione dell&#39;ambiente, ora puoi eseguire lo script tramite [!DNL Postman] interfaccia.

In [!DNL Postman] interfaccia, selezionare la cartella principale dell&#39;utilità di generazione automatica e quindi selezionare **[!DNL Run]** dall’intestazione superiore.

![cartella principale](../images/marketo/root-folder.png)

La [!DNL Runner] viene visualizzata l&#39;interfaccia. Da qui, accertati che tutte le caselle di controllo siano selezionate, quindi seleziona **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![generatore di corrente](../images/marketo/run-generator.png)

Una richiesta corretta crea i namespace e gli schemi richiesti per B2B.

## namespace B2B

Gli spazi dei nomi di identità sono un componente di [[!DNL Identity Service]](../../../../identity-service/home.md) che servono a distinguere il contesto o il tipo di identità. Un&#39;identità completa include un valore ID e uno spazio dei nomi. Consulta la sezione [panoramica dei namespace](../../../../identity-service/namespaces.md) per ulteriori informazioni.

I namespace B2B sono utilizzati nell’identità principale dell’entità.

La tabella seguente contiene informazioni sull’impostazione sottostante per i namespace B2B.

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome visualizzato | Simbolo di identità | Tipo di identità |
| --- | --- | --- |
| B2B Persona | `b2b_person` | `CROSS_DEVICE` |
| Conto B2B | `b2b_account` | `B2B_ACCOUNT` |
| Opportunità B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relazione personale opportunità B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campagna B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membro della campagna B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Elenco di marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membro della lista di marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relazione personale conto B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style=&quot;table-layout:auto&quot;}

## Schemi B2B

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che può essere contenuto all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi dello schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta la sezione [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi B2B.

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome dello schema | Classe base | Gruppi di campi | [!DNL Profile] in Schema | Identità principale | Spazio dei nomi identità principale | Identità secondaria | Spazio dei nomi identità secondario | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Conto B2B | [Account aziendale XDM](../../../../xdm/classes/b2b/business-account.md) | Dettagli account aziendale XDM | Abilitata | `accountKey.sourceKey` nella classe base | Conto B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Conto B2B | <ul><li>`accountParentKey.sourceKey` nel gruppo di campi Dettagli account business XDM</li><li>Proprietà di destinazione: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li></ul> |
| B2B Persona | [Profilo individuale XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Dettagli sulle persone aziendali XDM</li><li>Componenti per Business Person XDM</li><li>IdentityMap</li><li>Dettagli su consenso e preferenza</li></ul> | Abilitata | `b2b.personKey.sourceKey` nel gruppo di campi Dettagli persona commerciale XDM | B2B Persona | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` Gruppo di campi Dettagli persona commerciale XDM</li><li>`workEmail.address` Gruppo di campi Dettagli persona commerciale XDM</ol></li> | <ol><li>B2B Persona</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` Gruppo di campi Componenti Business Person XDM</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li><li>Proprietà di destinazione: accountKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Opportunità B2B | [Opportunità aziendali XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Dettagli opportunità di business XDM | Abilitata | `opportunityKey.sourceKey` nella classe base | Opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Opportunità B2B | <ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul> |
| Relazione personale opportunità B2B | [Relazione personale opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Nessuna | Abilitata | `opportunityPersonKey.sourceKey` nella classe base | Relazione personale opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Relazione personale opportunità B2B | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: b2b.personKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul>**Seconda relazione**<ul><li>`opportunityKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Opportunità B2B </li><li>Namespace: Opportunità B2B </li><li>Proprietà di destinazione: `opportunityKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Campagna B2B | [Campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign.md) | Dettagli della campagna aziendale XDM | Abilitata | `campaignKey.sourceKey` nella classe base | Campagna B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Campagna B2B |
| Membro della campagna B2B | [Membri di una campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Dettagli membri della campagna aziendale XDM | Abilitata | `ccampaignMemberKey.sourceKey` nella classe base | Membro della campagna B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Membro della campagna B2B | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Campagne</li></ul>**Seconda relazione**<ul><li>`campaignKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Campagna B2B</li><li>Namespace: Campagna B2B</li><li>Proprietà di destinazione: `campaignKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Campaign</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Elenco di marketing B2B | [Elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Nessuna | Abilitata | `marketingListKey.sourceKey` nella classe base | Elenco di marketing B2B | Nessuna | Nessuna | Nessuna | Elenco statico non sincronizzato da [!DNL Salesforce] e quindi non ha un&#39;identità secondaria. |
| Membro della lista di marketing B2B | [Membri elenco marketing commerciale XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Nessuna | Abilitata | `marketingListMemberKey.sourceKey` nella classe base | Membro della lista di marketing B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`PersonKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Elenchi di marketing</li></ul>**Seconda relazione**<ul><li>`marketingListKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Elenco di marketing B2B</li><li>Namespace: Elenco di marketing B2B</li><li>Proprietà di destinazione: `marketingListKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Elenco marketing</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> | Il membro dell&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e quindi non ha un&#39;identità secondaria. |
| Attività B2B | [ExperienceEvent XDM](../../../../xdm/classes/experienceevent.md) | <ul><li>Visita WebPage</li><li>Nuovo lead</li><li>Converti lead</li><li>Aggiungi all’elenco</li><li>Rimuovi da elenco</li><li>Aggiungi a opportunità</li><li>Rimuovi da opportunità</li><li>Modulo compilato</li><li>Clic sui collegamenti</li><li>E-mail consegnata</li><li>E-mail aperta</li><li>E-mail selezionata</li><li>E-mail rimbalzata</li><li>E-mail - Soft rimbalzato</li><li>E-mail annullata</li><li>Punteggio modificato</li><li>Opportunità aggiornata</li><li>Stato in progressione campagna modificato</li><li>Identificatore persona</li><li>URL web Marketo</li><li>Momento interessante</li><li>Chiama Webhook</li><li>Cambia la cadenza della campagna</li><li>Fase dei ricavi modificata</li><li>Unisci lead</li><li>Invia e-mail</li></ul> | Abilitata | `personKey.sourceKey` del gruppo di campi ID persona | B2B Persona | Nessuna | Nessuna | **Prima relazione**<ul><li>`listOperations.listKey.sourceKey` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Elenco di marketing B2B</li><li>Namespace: Elenco di marketing B2B</li></ul>**Seconda relazione**<ul><li>`opportunityEvent.opportunityKey.sourceKey` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Opportunità B2B</li><li>Namespace: Opportunità B2B</li></ul>**Terza relazione**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Campagna B2B</li><li>Namespace: Campagna B2B</li></ul> | `ExperienceEvent` è diverso dalle entità. L’identità dell’evento di esperienza è la persona che ha eseguito l’attività. |
| Relazione personale conto B2B | [Relazione personale account aziendale XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mappa delle identità | Abilitata | `accountPersonKey.sourceKey` nella classe base | Relazione personale conto B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: `b2b.personKey.SourceKey`</li><li>Nome di relazione dallo schema corrente: Persone</li><li>Nome di relazione dallo schema di riferimento: Account</li></ul>**Seconda relazione**<ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Per scoprire come collegare le [!DNL Marketo] dati a Platform, consulta l’esercitazione su [creazione di un connettore sorgente Marketo nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
