---
title: Panoramica Di Oracle Eloqua (V2) Source
description: Scopri come collegare Oracle Eloqua a Adobe Experience Platform.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 1%

---

# Panoramica sull&#39;origine di [!DNL Oracle Eloqua] (V2)

>[!IMPORTANT]
>
>L&#39;origine [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md) originale è stata rimossa a gennaio 2026. Nessuna migrazione disponibile per questa origine obsoleta. È necessario implementare nuovamente i dati utilizzando la nuova origine [!DNL Oracle Eloqua] (V2).

[!DNL Oracle Eloqua] è una potente piattaforma di automazione del marketing di livello enterprise progettata per aiutare le organizzazioni, principalmente nello spazio B2B, ad automatizzare e personalizzare il complesso processo di gestione dei lead e di orchestrazione dei percorsi di acquirenti. Funge da hub centrale in cui i team di marketing possono definire, distribuire e misurare campagne sofisticate su più canali digitali, garantendo che i potenziali clienti ricevano i contenuti giusti nel momento preciso in cui sono più coinvolti. Gli oggetti supportati per l&#39;acquisizione tramite [!DNL Eloqua] sono **Contatti**, **Account**, **Campagne** e **Attività**. Una volta completata l’acquisizione iniziale, tutti i dati modificati vengono importati utilizzando un processo incrementale pianificato.

È possibile utilizzare l&#39;origine [!DNL Eloqua] per connettere l&#39;account [!DNL Eloqua] a Adobe Experience Platform. Per informazioni su come iniziare, leggi la documentazione sottostante.

## Esempi di casi d’uso {#use-case-examples}

Di seguito è riportata una tabella che illustra gli oggetti di marketing supportati dall&#39;integrazione [!DNL Eloqua] (V2) con Adobe Experience Platform. Per ogni oggetto, troverai una descrizione insieme a casi d&#39;uso di esempio per illustrare come l&#39;integrazione dei dati di [!DNL Eloqua] con Real-Time CDP può migliorare l&#39;efficacia del marketing e i risultati della campagna.

| Oggetto | Descrizione | Esempi di casi d’uso |
| --- | --- | --- |
| Contatti | Acquisisci i dati di contatto (come nome, e-mail, numero di telefono e qualifica) in Real-Time CDP per creare profili cliente dettagliati e unificati che consolidino tutte le interazioni e i coinvolgimento con ogni singolo contatto. | **Ottimizzazione campagna:** Integrando i dati dei contatti di [!DNL Eloqua], il team marketing può identificare i potenziali clienti con priorità elevata in base ad attività recenti come l&#39;apertura di e-mail, l&#39;invio di moduli e la registrazione di eventi. Real-Time CDP fornisce una visualizzazione a 360° del comportamento di ogni contatto tramite e-mail, sito web e altri punti di contatto di marketing, consentendo ai team di marketing di personalizzare le campagne e ottimizzare la messaggistica per migliorare il coinvolgimento e la conversione. |
| Account | Acquisisci dati a livello di account (ad esempio nome della società, settore, dimensioni della società, ricavi, posizione) per creare strategie di marketing basate su account (ABM) in Real-Time CDP e consentire al team di eseguire il targeting e coinvolgere le organizzazioni giuste con messaggi pertinenti. | **Campagne ABM:** L&#39;integrazione dei dati account da [!DNL Eloqua] consente di creare campagne ABM mirate. Ad esempio, una società di software potrebbe utilizzare i dati dell’account per segmentare e inviare campagne e-mail personalizzate ai decision-maker delle aziende del settore finanziario, promuovendo nuove soluzioni su misura per il proprio settore. |
| Campagne | Acquisisci i dati della campagna (come nomi, tipi, obiettivi e metriche delle prestazioni delle campagne, come tassi di apertura, CTR) in Real-Time CDP per tracciare e ottimizzare le prestazioni della campagna su più canali. Utilizza questi dati per misurare il ROI e perfezionare le tue strategie. | **Attribuzione cross-channel:** se [!DNL Eloqua] invia i dati della campagna a Real-Time CDP, i team di marketing possono visualizzare le prestazioni delle campagne su vari canali (e-mail, social media, annunci e così via), attribuendo le conversioni ai punti di contatto giusti e perfezionando le strategie future basate su tale insight. |
| Attività | Acquisisci i dati dell’attività (ad esempio aperture di e-mail, clic, visite al sito web, invii di moduli, partecipazione a webinar) per monitorare il comportamento in tempo reale e i contatti tra diversi canali, creando opportunità per un coinvolgimento personalizzato in tempo reale. | **Intrattenimento in tempo reale:** Integrando i dati dell&#39;attività da [!DNL Eloqua], Real-Time CDP può attivare e-mail o notifiche personalizzate ai team di vendita quando un contatto è coinvolto con contenuti (ad esempio scaricando un white paper o facendo clic su un collegamento e-mail), consentendo un follow-up tempestivo e migliori opportunità di conversione. |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Leggi le sezioni seguenti per informazioni sui prerequisiti da completare per connettere l’origine ad Experience Platform.

### Imposta l&#39;applicazione per l&#39;autenticazione

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Eloqua] e connettersi ad Experience Platform utilizzando l&#39;autenticazione di base.

Per iniziare, accedi all&#39;istanza di [!DNL Eloqua] come amministratore (o come utente con accesso per creare utenti, gruppi di sicurezza e app).

![Il Mio Cruscotto Eloqua.](../../images/tutorials/create/eloqua/admin.png)

Passa a **Impostazioni** > **Estensioni piattaforma** > **Sviluppatore cloud app** > **Crea app**. Fornisci i dettagli dell&#39;app, tra cui nome, descrizione, icona e l&#39;URL di callback OAuth. Al termine, seleziona **Salva**.

![Il pannello Sviluppatore app e il pulsante Crea app nel dashboard di Eloqua.](../../images/tutorials/create/eloqua/create-app.png)

| Proprietà | Descrizione |
| --- | --- |
| Nome | Nome dell’app. |
| Descrizione | Breve descrizione dell’app. |
| Icona | URL dell&#39;icona. |
| URL richiamata OAuth | URL a cui devono essere reindirizzati gli utenti dopo l&#39;installazione dell&#39;app e l&#39;autenticazione con [!DNL Eloqua]. |

![Finestra Crea app in Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

Dopo aver creato l&#39;app, passa a [!DNL Authentication to Eloqua] e recupera **ID client** e **Segreto client** dalla nuova app creata. Questi valori verranno utilizzati in seguito durante la connessione ad Experience Platform.

![L&#39;ID client e il segreto client in Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

I gruppi di sicurezza consentono agli amministratori di controllare i livelli di accesso degli utenti a risorse, funzionalità, interfacce e così via. Per creare un gruppo di sicurezza, passa a **Impostazioni** > **Utenti**. Quindi, seleziona la scheda **Gruppo** nel pannello a sinistra, quindi seleziona **Crea nuovo gruppo di sicurezza**.

![Dashboard di gestione utenti in Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Utilizza la finestra **[!DNL Security Group Overview]** per fornire un nome e un acronimo per il gruppo di sicurezza. Dopo la creazione, passa a [!DNL Action Permissions] e aggiungi l&#39;autorizzazione API [!DNL Consume] dall&#39;elenco, quindi seleziona **Salva**.

![Finestra di panoramica sul gruppo di sicurezza in Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![Finestra di selezione per utilizzare API](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>L&#39;API [!DNL Consume] è un&#39;autorizzazione obbligatoria, ma puoi aggiungere altre autorizzazioni a seconda dell&#39;utilizzo dell&#39;app.

Per acquisire i dati della campagna, passa all&#39;interfaccia **Modifica utente** e aggiungi [!DNL Guided Campaigns] al gruppo di sicurezza selezionato.

![Gruppo di sicurezza con campagne guidate aggiunto.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

Facoltativamente, puoi creare un altro utente e aggiungerlo a un gruppo di sicurezza. Per i passaggi dettagliati, leggere la documentazione di [!DNL Eloqua] su [creazione di un utente](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) e [assegnazione di un utente a un gruppo di sicurezza](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Raccogli le credenziali richieste

Per connettere [!DNL Eloqua] ad Experience Platform è necessario fornire i valori per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| ID client | L&#39;identificatore pubblicamente esposto utilizzato da [!DNL Eloqua] per identificare l&#39;account quando si autorizza Experience Platform. |
| Segreto client | Chiave riservata nota solo all&#39;applicazione client e al server di autorizzazione. Questa chiave è necessaria insieme all’ID client per autenticare il tuo account. |
| Nome utente | Il nome utente associato al tuo account [!DNL Eloqua]. Viene utilizzato per verificare e autorizzare l’accesso. Il nome utente segue il formato di `CompanyName\Username`. |
| Password | La password associata al tuo account [!DNL Eloqua]. Insieme al nome utente, consente di accedere all’ambiente Eloqua. |
| Endpoint base | Prefisso dell&#39;URI di base per l&#39;autenticazione per [!DNL Eloqua]. L&#39;endpoint base non deve includere `http://` o `https://` durante l&#39;autenticazione. |

## Guida alla mappatura di [!DNL Eloqua]

>[!NOTE]
>
>Di seguito sono riportati i campi delta utilizzati internamente per il caricamento di dati incrementali:
>
>- **Contatti:** `C_DateModified`
>- **Account:** `M_DateModified`
>- **Attività:** `CreatedAt`
>- **Oggetti personalizzati:** `UpdatedAt`
>- **Campagna:** `updatedAt`

Le tabelle seguenti forniscono mappature dettagliate tra i campi di origine [!DNL Eloqua] e i corrispondenti campi di destinazione Experience Data Model (XDM) in Experience Platform. Ogni riga descrive la logica di trasformazione, indica se il campo è immutabile e fornisce note aggiuntive per aiutarti a comprendere come i tuoi dati di [!DNL Eloqua] verranno acquisiti e strutturati in Experience Platform.

### Account

| Colonna Eloqua Source | Percorso di destinazione XDM | Note |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Questo campo è sempre impostato sul valore fisso &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Il connettore non è in grado di rilevare automaticamente l&#39;ID istanza CRM. È necessario sostituire manualmente `${CRM_INSTANCE_ID}` con l&#39;ID istanza CRM effettivo, sia con l&#39;ID istanza Salesforce che con l&#39;ID istanza Dynamics. Durante l&#39;acquisizione, se `M_SFDCAccountID` è presente, il connettore genera la chiave esterna utilizzando tale valore e aggiunge `\@CRM_INSTANCE_ID.Salesforce`. Se il campo è vuoto, il connettore utilizzerà `M_MSCRMAccountID` e aggiungerà `\@CRM_INSTANCE_ID.Dynamics`. Se entrambi i campi sono vuoti, questo campo verrà impostato su null. |

{style="table-layout:auto"}

### Attività

| Colonna Eloqua Source | Percorso di destinazione XDM | Note |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Questo campo è sempre impostato sul valore fisso &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | In base all’ActivityType, verrà popolato il valore eventType di Experience Platform corrispondente. Per ExternalActivities, non esiste alcun eventType in Experience Platform. Puoi modificare questa mappatura per gestire più tipi. |
| `ActivityDate` | timestamp | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Campagne

| Colonna Eloqua Source | Percorso di destinazione XDM | Note |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Questo campo è sempre impostato sul valore fisso &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Contatti

| Colonna Eloqua Source | Percorso di destinazione XDM | Note |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Questo campo è sempre impostato sul valore fisso &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID` verrà automaticamente sostituito dal connettore. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Se l&#39;istanza [!DNL Eloqua] è sincronizzata con Salesforce, mantenere questa mappatura. In caso contrario, rimuoverlo. Il connettore non dispone di un modo per determinare CRM_INSTANCE_ID, pertanto devi sostituire ${CRM_INSTANCE_ID} con l&#39;ID istanza di Salesforce sincronizzato. La stessa mappatura si applica a personComponents e extSourceSystemAudit, quindi mantieni entrambi. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Se l&#39;istanza [!DNL Eloqua] è sincronizzata con Dynamics, mantenere questa mappatura. In caso contrario, rimuoverlo. Il connettore non dispone di un modo per determinare CRM_INSTANCE_ID, pertanto devi sostituire ${CRM_INSTANCE_ID} con l&#39;ID istanza sincronizzato di Dynamics. La stessa mappatura si applica a personComponents e extSourceSystemAudit, quindi mantieni entrambi. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Se l&#39;istanza [!DNL Eloqua] è sincronizzata con Salesforce, mantenere questa mappatura. In caso contrario, rimuoverlo. Il connettore non dispone di un modo per determinare CRM_INSTANCE_ID, pertanto devi sostituire ${CRM_INSTANCE_ID} con l&#39;ID istanza di Salesforce sincronizzato. La stessa mappatura si applica a personComponents e extSourceSystemAudit, quindi mantieni entrambi. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Se l&#39;istanza [!DNL Eloqua] è sincronizzata con Dynamics, mantenere questa mappatura. In caso contrario, rimuoverlo. Il connettore non dispone di un modo per determinare CRM_INSTANCE_ID, pertanto devi sostituire ${CRM_INSTANCE_ID} con l&#39;ID istanza sincronizzato di Dynamics. La stessa mappatura si applica a personComponents e extSourceSystemAudit, quindi mantieni entrambi. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | Il connettore non dispone di un modo per determinare CRM_INSTANCE_ID, pertanto è necessario sostituire ${CRM_INSTANCE_ID} con l&#39;ID istanza CRM sincronizzato, ovvero l&#39;ID istanza di Salesforce o l&#39;ID istanza di Dynamics. La stessa mappatura si applica sia a b2b.accountKey che a personComponents.sourceAccountKey, pertanto mantieni entrambi. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | Il connettore non dispone di un modo per determinare CRM_INSTANCE_ID, pertanto è necessario sostituire ${CRM_INSTANCE_ID} con l&#39;ID istanza CRM sincronizzato, ovvero l&#39;ID istanza di Salesforce o l&#39;ID istanza di Dynamics. La stessa mappatura si applica sia a b2b.accountKey che a personComponents.sourceAccountKey, pertanto mantieni entrambi. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Riferimento mappatura tipo di attività

| Eloqua ActivityType | EventType XDM |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | pass-through così com&#39;è |

{style="table-layout:auto"}

### Segnaposto variabili

I modelli di mappatura utilizzano i seguenti segnaposto di variabili che vengono sostituiti una volta eseguito un flusso di dati:

| Segnaposto | Descrizione | Utilizzo |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | ID univoco per l’istanza sorgente Eloqua | Utilizzato nelle chiavi di origine |
| `${CRM_INSTANCE_ID}` | ID univoco per il sistema CRM (Salesforce/Dynamics) | Utilizzato nelle chiavi esterne |

## Connetti [!DNL Eloqua] ad Experience Platform

Procedi alla configurazione della connessione di origine [!DNL Eloqua] in Experience Platform. Per una guida dettagliata sulla configurazione della connessione tramite l&#39;interfaccia utente, consulta l&#39;[esercitazione](../../tutorials/ui/create/marketing-automation/eloqua.md). Leggi questa esercitazione per scoprire come connettere il tuo account [!DNL Eloqua], selezionare dati, mappare campi, pianificare acquisizioni e monitorare i flussi di dati.

