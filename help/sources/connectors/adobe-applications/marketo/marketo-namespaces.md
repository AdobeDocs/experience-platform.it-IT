---
keywords: Experience Platform;home;argomenti popolari;connettore sorgente Marketo;spazi dei nomi;schemi;b2b;B2B
solution: Experience Platform
title: namespace e schemi B2B
topic-legacy: overview
description: Questo documento fornisce una panoramica dei namespace personalizzati necessari per la creazione di un connettore sorgente B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: a67e411c7d07bc5d94876b6bafbbea5056b7a9bc
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 2%

---

# namespace e schemi B2B

Questo documento fornisce informazioni sull&#39;impostazione sottostante per i namespace e gli schemi da utilizzare con le origini B2B. Questo documento fornisce anche dettagli sull&#39;impostazione dell&#39;utility di automazione Postman necessaria per generare spazi dei nomi e schemi B2B.

## Imposta spazi dei nomi B2B e utilità di generazione automatica dello schema

Il primo passaggio nell’utilizzo dell’utility di generazione automatica dello spazio dei nomi B2B e dello schema è quello di configurare la console per sviluppatori di Platform e l’ ambiente [!DNL Postman] .

- Puoi scaricare lo spazio dei nomi e lo schema per la raccolta e l&#39;ambiente di utilità di generazione automatica da questo [archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
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

{style=&quot;table-layout:auto&quot;}

### Esecuzione degli script

Con la raccolta [!DNL Postman] e l&#39;ambiente impostati, ora puoi eseguire lo script tramite l&#39;interfaccia [!DNL Postman].

Nell&#39;interfaccia [!DNL Postman], seleziona la cartella principale dell&#39;utilità di generazione automatica e seleziona **[!DNL Run]** dall&#39;intestazione superiore.

![cartella principale](../images/marketo/root-folder.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner]. Da qui, accertati che tutte le caselle di controllo siano selezionate e quindi seleziona **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![generatore di corrente](../images/marketo/run-generator.png)

Una richiesta corretta crea i namespace e gli schemi richiesti per B2B.

## namespace B2B

Gli spazi dei nomi di identità sono un componente di [[!DNL Identity Service]](../../../../identity-service/home.md) che serve a distinguere il contesto o il tipo di identità. Un&#39;identità completa include un valore ID e uno spazio dei nomi. Per ulteriori informazioni, consulta la [panoramica dei namespace](../../../../identity-service/namespaces.md) .

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

{style=&quot;table-layout:auto&quot;}

## Schemi B2B

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che può essere contenuto all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi dello schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta le [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi B2B.

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Nome dello schema | Classe base | Gruppi di campi | [!DNL Profile] in Schema | Identità principale | Spazio dei nomi identità principale | Identità secondaria | Spazio dei nomi identità secondario | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Conto B2B | Account aziendale XDM | Dettagli account aziendale XDM | Abilitata | `accountKey.sourceKey` nella classe base | Conto B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Conto B2B | <ul><li>`accountParentKey.sourceKey` nel gruppo di campi Dettagli account business XDM</li><li>Proprietà di destinazione: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li></ul> |
| B2B Persona | Profilo individuale XDM | <ul><li>Dettagli sulle persone aziendali XDM</li><li>Componenti per Business Person XDM</li><li>IdentityMap</li><li>Dettagli su consenso e preferenza</li></ul> | Abilitata | `b2b.personKey.sourceKey` nel gruppo di campi Dettagli persona commerciale XDM | B2B Persona | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` Gruppo di campi Dettagli persona commerciale XDM</li><li>`workEmail.address` Gruppo di campi Dettagli persona commerciale XDM</ol></li> | <ol><li>B2B Persona</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` Gruppo di campi Componenti Business Person XDM</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li><li>Proprietà di destinazione: accountKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Opportunità B2B | Opportunità aziendali XDM | Dettagli opportunità di business XDM | Abilitata | `opportunityKey.sourceKey` nella classe base | Opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Opportunità B2B | <ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Conto B2B</li><li>Namespace: Conto B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul> |
| Relazione personale opportunità B2B | Relazione personale opportunità di business XDM | Nessuna | Abilitata | `opportunityPersonKey.sourceKey` nella classe base | Relazione personale opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Relazione personale opportunità B2B | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: b2b.personKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Opportunità</li></ul>**Seconda relazione**<ul><li>`opportunityKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Opportunità B2B </li><li>Namespace: Opportunità B2B </li><li>Proprietà di destinazione: `opportunityKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Campagna B2B | Campagna aziendale XDM | Dettagli della campagna aziendale XDM | Abilitata | `campaignKey.sourceKey` nella classe base | Campagna B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Campagna B2B |
| Membro della campagna B2B | Membro della campagna aziendale XDM | Dettagli membri della campagna aziendale XDM | Abilitata | `ccampaignMemberKey.sourceKey` nella classe base | Membro della campagna B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Membro della campagna B2B | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Campagne</li></ul>**Seconda relazione**<ul><li>`campaignKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Campagna B2B</li><li>Namespace: Campagna B2B</li><li>Proprietà di destinazione: `campaignKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Campaign</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |
| Elenco di marketing B2B | Elenco di marketing aziendale XDM | Nessuna | Abilitata | `marketingListKey.sourceKey` nella classe base | Elenco di marketing B2B | Nessuna | Nessuna | Nessuna | L’elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un’identità secondaria. |
| Membro della lista di marketing B2B | Membri elenco marketing commerciale XDM | Nessuna | Abilitata | `marketingListMemberKey.sourceKey` nella classe base | Membro della lista di marketing B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`PersonKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: B2B Persona</li><li>Namespace: B2B Persona</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Elenchi di marketing</li></ul>**Seconda relazione**<ul><li>`marketingListKey.sourceKey` nella classe base</li><li>Tipo: Many-to-one (Da molti a uno)</li><li>Schema di riferimento: Elenco di marketing B2B</li><li>Namespace: Elenco di marketing B2B</li><li>Proprietà di destinazione: `marketingListKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Elenco marketing</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> | Il membro dell’elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un’identità secondaria. |
| Attività B2B | ExperienceEvent XDM | <ul><li>Visita WebPage</li><li>Nuovo lead</li><li>Converti lead</li><li>Aggiungi all’elenco</li><li>Rimuovi da elenco</li><li>Aggiungi a opportunità</li><li>Rimuovi da opportunità</li><li>Modulo compilato</li><li>Clic sui collegamenti</li><li>E-mail consegnata</li><li>E-mail aperta</li><li>E-mail selezionata</li><li>E-mail rimbalzata</li><li>E-mail - Soft rimbalzato</li><li>E-mail annullata</li><li>Punteggio modificato</li><li>Opportunità aggiornata</li><li>Stato in progressione campagna modificato</li><li>Identificatore persona</li><li>URL web Marketo</li><li>Momento interessante</li></ul> | Abilitata | `personKey.sourceKey` del gruppo di campi ID persona | B2B Persona | Nessuna | Nessuna | **Prima relazione**<ul><li>`listOperations.listKey.sourceKey` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Elenco di marketing B2B</li><li>Namespace: Elenco di marketing B2B</li></ul>**Seconda relazione**<ul><li>`opportunityEvent.opportunityKey.sourceKey` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Opportunità B2B</li><li>Namespace: Opportunità B2B</li></ul>**Terza relazione**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` o in un altro campo</li><li>Tipo: uno a uno</li><li>Schema di riferimento: Campagna B2B</li><li>Namespace: Campagna B2B</li></ul> | `ExperienceEvent` è diverso dalle entità. L’identità dell’evento di esperienza è la persona che ha eseguito l’attività. |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Per informazioni su come collegare i dati [!DNL Marketo] a Platform, consulta l’esercitazione su [creazione di un connettore sorgente Marketo nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
