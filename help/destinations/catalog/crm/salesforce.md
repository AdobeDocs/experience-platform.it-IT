---
keywords: crm;CRM;crm destinazioni;salesforce crm;salesforce crm destinazione
title: Connessione Salesforce CRM
description: La destinazione di Salesforce CRM ti consente di esportare i dati del tuo account e di attivarli in Salesforce CRM per le tue esigenze aziendali.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 27f2b28d924fbd85eefbea5a65d1ee9249bafa87
workflow-type: tm+mt
source-wordcount: '2734'
ht-degree: 1%

---

# Connessione [!DNL Salesforce CRM]

## Panoramica {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) è una popolare piattaforma di gestione delle relazioni con i clienti (CRM) e supporta i tipi di profili descritti di seguito:

* [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Un lead è il nome di una persona o di un&#39;azienda che potrebbe essere interessata ai prodotti o ai servizi venduti.
* [Contatti](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Un contatto è una persona con cui uno dei tuoi rappresentanti ha stabilito una relazione ed è stato qualificato come potenziale cliente.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), che supporta entrambi i tipi di profili descritti in precedenza.

Quando [attivi segmenti](#activate), puoi selezionare lead o contatti e aggiornare attributi e dati sul pubblico in [!DNL Salesforce CRM].

[!DNL Salesforce CRM] utilizza OAuth 2 con concessione password come meccanismo di autenticazione per comunicare con l&#39;API REST di Salesforce. Le istruzioni per l&#39;autenticazione nell&#39;istanza [!DNL Salesforce CRM] sono riportate di seguito, nella sezione [Autentica nella destinazione](#authenticate).

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi fornire esperienze personalizzate ai tuoi utenti, in base agli attributi dei loro profili Adobe Experience Platform. Puoi creare tipi di pubblico dai dati offline e inviarli a Salesforce CRM per aggiornare l’iscrizione a CRM non appena tipi di pubblico e profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione di Salesforce CRM, è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creati in [!DNL Experience Platform].

### Prerequisiti in [!DNL Salesforce CRM] {#prerequisites-destination}

Per esportare i dati da Experience Platform al tuo account Salesforce, tieni presente i seguenti prerequisiti in [!DNL Salesforce CRM]:

#### Devi avere un account [!DNL Salesforce] {#prerequisites-account}

Vai alla pagina [!DNL Salesforce] [prova](https://www.salesforce.com/in/form/signup/freetrial-sales/) per registrarti e creare un account [!DNL Salesforce], se non ne hai già uno.

#### Configurare un&#39;app connessa in [!DNL Salesforce] {#prerequisites-connected-app}

Devi innanzitutto configurare un&#39;app [[!DNL Salesforce] connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&language=en_US&r=https%3A%2F%2Fhelp.salesforce.com%2F&type=5) nel tuo account [!DNL Salesforce], se non ne hai già una. [!DNL Salesforce CRM] sfrutterà l&#39;app connessa per connettersi a [!DNL Salesforce].

Quindi, abilitare [!DNL OAuth Settings for API Integration] per [!DNL Salesforce connected app]. Consulta la documentazione di [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&type=5&language=en_US) per maggiori informazioni.

Inoltre, assicurati che [ambiti](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&type=5&language=en_US) menzionati di seguito siano selezionati per [!DNL Salesforce connected app].

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

Infine, assicurati che la sovvenzione `password` sia abilitata nel tuo account [!DNL Salesforce]. Per informazioni sugli scenari speciali[!DNL Salesforce], consulta la documentazione [ ](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&type=5)Flusso nome utente-password OAuth 2.0.

>[!IMPORTANT]
>
>Se l&#39;amministratore dell&#39;account [!DNL Salesforce] ha limitato l&#39;accesso agli intervalli IP attendibili, è necessario contattarli per inserire nell&#39;elenco Consentiti [gli IP di Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md). Se hai bisogno di ulteriori indicazioni, consulta la documentazione [!DNL Salesforce] [Limita l&#39;accesso agli intervalli IP attendibili per un&#39;app connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5).

#### Crea campi personalizzati in [!DNL Salesforce] {#prerequisites-custom-field}

Quando si attivano i tipi di pubblico nella destinazione [!DNL Salesforce CRM], è necessario immettere un valore nel campo **[!UICONTROL Mapping ID]** per ogni pubblico attivato, nel passaggio **[Pianificazione pubblico](#schedule-segment-export-example)**.

[!DNL Salesforce CRM] richiede questo valore per leggere e interpretare correttamente i tipi di pubblico provenienti da Experience Platform e per aggiornare il loro stato di pubblico entro [!DNL Salesforce]. Se hai bisogno di indicazioni sugli stati del pubblico, consulta la documentazione di Experience Platform per il gruppo di campi dello schema [Dettagli sull&#39;iscrizione al pubblico](/help/xdm/field-groups/profile/segmentation.md).

Per ogni pubblico che si attiva da Experience Platform a [!DNL Salesforce CRM], è necessario creare un campo personalizzato di tipo `Text Area (Long)` entro [!DNL Salesforce]. Puoi definire la lunghezza del carattere di campo di qualsiasi dimensione compresa tra 256 e 131.072 caratteri in base alle tue esigenze aziendali. Per ulteriori informazioni sui tipi di campi personalizzati, vedere la pagina della documentazione [!DNL Salesforce] [Tipi di campi personalizzati](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&type=5). Consulta anche la documentazione di [!DNL Salesforce] per [creare campi personalizzati](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&type=5&language=en_US) in caso di assistenza nella creazione dei campi.

>[!IMPORTANT]
>
>Non includere spazi nel nome del campo. Utilizzare invece il carattere di sottolineatura `(_)` come separatore.
>In [!DNL Salesforce] è necessario creare campi personalizzati con un **[!UICONTROL Field Name]** che corrisponda esattamente al valore specificato in **[!UICONTROL Mapping ID]** per ogni segmento Experience Platform attivato. Ad esempio, la schermata seguente mostra un campo personalizzato denominato `crm_2_seg`. Quando si attiva un pubblico in questa destinazione, aggiungere `crm_2_seg` come **[!UICONTROL Mapping ID]** per popolare i tipi di pubblico da Experience Platform in questo campo personalizzato.

Di seguito è riportato un esempio di creazione di campi personalizzati in [!DNL Salesforce], *Passaggio 1 - Seleziona il tipo di dati*:
![Schermata dell&#39;interfaccia utente di Salesforce che mostra la creazione di campi personalizzati, passaggio 1 - Selezionare il tipo di dati.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Di seguito è riportato un esempio di creazione di campi personalizzati in [!DNL Salesforce], *Passaggio 2 - Immettere i dettagli per il campo personalizzato*:
![Schermata dell&#39;interfaccia utente di Salesforce che mostra la creazione di campi personalizzati, passaggio 2 - Immetti i dettagli per il campo personalizzato.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Per distinguere tra i campi personalizzati utilizzati per i tipi di pubblico di Experience Platform e altri campi personalizzati all&#39;interno di [!DNL Salesforce], è possibile includere un prefisso o un suffisso riconoscibile durante la creazione del campo personalizzato. Ad esempio, invece di `test_segment`, utilizzare `Adobe_test_segment` o `test_segment_Adobe`
>* Se in [!DNL Salesforce] sono già stati creati altri campi personalizzati, è possibile utilizzare lo stesso nome del segmento Experience Platform per identificare facilmente il pubblico in [!DNL Salesforce].

>[!NOTE]
>
>* Gli oggetti in Salesforce sono limitati a 25 campi esterni. Vedere [Attributi di campo personalizzati](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5).
>* Questa restrizione implica che puoi avere solo un massimo di 25 iscrizioni di pubblico Experience Platform attive in qualsiasi momento.
>* Se hai raggiunto questo limite in Salesforce, prima di poter utilizzare un nuovo **[!UICONTROL Mapping ID]** devi rimuovere da Salesforce gli attributi personalizzati utilizzati per memorizzare lo stato del pubblico rispetto ai tipi di pubblico meno recenti in Experience Platform.

#### Raccogli [!DNL Salesforce CRM] credenziali {#gather-credentials}

Annotare gli elementi riportati di seguito prima di eseguire l&#39;autenticazione nella destinazione [!DNL Salesforce CRM]:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Username` | Nome utente dell&#39;account [!DNL Salesforce]. | |
| `Password` | Password dell&#39;account [!DNL Salesforce]. | |
| `Security Token` | Il token di sicurezza [!DNL Salesforce] che verrà in seguito aggiunto alla fine della password [!DNL Salesforce] per creare una stringa concatenata da utilizzare come **[!UICONTROL Password]** durante l&#39;autenticazione [alla destinazione](#authenticate).<br> Consulta la documentazione di [!DNL Salesforce] per [reimpostare il token di sicurezza](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&type=5) per scoprire come rigenerarlo dall&#39;interfaccia di [!DNL Salesforce] se non disponi del token di sicurezza. |  |
| `Custom Domain` | Il prefisso del dominio [!DNL Salesforce]. <br> Per informazioni su come ottenere questo valore dall&#39;interfaccia [[!DNL Salesforce] , consulta la ](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&type=5)documentazione[!DNL Salesforce]. | Se il dominio [!DNL Salesforce] è <br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> come valore sarà necessario `d5i000000isb4eak-dev-ed`. |
| `Client ID` | Salesforce `Consumer Key`. <br> Per informazioni su come ottenere questo valore dall&#39;interfaccia [[!DNL Salesforce] , consulta la ](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&type=5)documentazione[!DNL Salesforce]. | |
| `Client Secret` | Salesforce `Consumer Secret`. <br> Per informazioni su come ottenere questo valore dall&#39;interfaccia [[!DNL Salesforce] , consulta la ](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&type=5)documentazione[!DNL Salesforce]. | |

### Guardrail {#guardrails}

[!DNL Salesforce] bilancia i carichi delle transazioni imponendo limiti di richiesta, frequenza e timeout. Per ulteriori informazioni, consulta [Limiti di richieste e allocazioni API](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm).

Se l&#39;amministratore dell&#39;account [!DNL Salesforce] ha applicato restrizioni IP, sarà necessario aggiungere [indirizzi IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) agli intervalli IP attendibili degli account [!DNL Salesforce]. Se hai bisogno di ulteriori indicazioni, consulta la documentazione [!DNL Salesforce] [Limita l&#39;accesso agli intervalli IP attendibili per un&#39;app connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5).

>[!IMPORTANT]
>
>Quando [si attivano i segmenti](#activate) è necessario selezionare tra i tipi *Contatto* o *Lead*. Assicurati che i tipi di pubblico dispongano della mappatura dei dati appropriata in base al tipo selezionato.

## Identità supportate {#supported-identities}

[!DNL Salesforce CRM] supporta l&#39;aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| `SalesforceId` | L&#39;identificatore [!DNL Salesforce CRM] per le identità di contatto o lead esportate o aggiornate tramite il segmento. | Obbligatorio |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Profile-based]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Ogni stato del pubblico in [!DNL Salesforce CRM] viene aggiornato con lo stato del pubblico corrispondente da Experience Platform, in base al valore **[!UICONTROL Mapping ID]** fornito durante il passaggio [pianificazione del pubblico](#schedule-segment-export-example).</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Entro **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, cerca [!DNL Salesforce CRM]. In alternativa, è possibile individuarlo nella categoria **[!UICONTROL CRM]**.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**. Per ulteriori informazioni, consulta la sezione [Raccogli [!DNL Salesforce CRM] credenziali](#gather-credentials).

| Credenziali | Descrizione |
| --- | --- |
| **[!UICONTROL Username]** | Nome utente dell&#39;account [!DNL Salesforce]. |
| **[!UICONTROL Password]** | Stringa concatenata composta dalla password dell&#39;account [!DNL Salesforce] a cui è stato aggiunto il token di sicurezza [!DNL Salesforce].<br>Il valore concatenato è `{PASSWORD}{TOKEN}`.<br> Nota: non utilizzare parentesi graffe o spazi.<br>Ad esempio, se la password [!DNL Salesforce] è `MyPa$$w0rd123` e il token di sicurezza [!DNL Salesforce] è `TOKEN12345....0000`, il valore concatenato che utilizzerai nel campo **[!UICONTROL Password]** è `MyPa$$w0rd123TOKEN12345....0000`. |
| **[!UICONTROL Custom Domain]** | Il prefisso del dominio [!DNL Salesforce]. <br>Ad esempio, se il tuo dominio è *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, devi fornire `d5i000000isb4eak-dev-ed` come valore. |
| **[!UICONTROL Client ID]** | L&#39;app [!DNL Salesforce] connessa a `Consumer Key`. |
| **[!UICONTROL Client Secret]** | L&#39;app [!DNL Salesforce] connessa a `Consumer Secret`. |

![Schermata dell&#39;interfaccia utente di Experience Platform che mostra come eseguire l&#39;autenticazione.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connected]** con un segno di spunta verde. È quindi possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Salesforce ID Type]**:

   * Selezionare **[!UICONTROL Contact]** se le identità da esportare o aggiornare sono di tipo *Contatto*.
   * Selezionare **[!UICONTROL Lead]** se le identità da esportare o aggiornare sono di tipo *Lead*.

![Schermata dell&#39;interfaccia utente di Experience Platform con i dettagli della destinazione.](../../assets/catalog/crm/salesforce/destination-details.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL Salesforce CRM], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Experience Platform e i corrispondenti equivalenti dalla destinazione.

Gli attributi specificati in **[!UICONTROL Target field]** devono essere denominati esattamente come descritto nella tabella dei mapping degli attributi, in quanto tali attributi formeranno il corpo della richiesta.

Gli attributi specificati in **[!UICONTROL Source field]** non seguono alcuna restrizione di questo tipo. Puoi mapparlo in base alle tue esigenze, ma assicurati che il formato dei dati di input sia valido in base alla [[!DNL Salesforce] documentazione](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5). Se i dati di input non sono validi, la chiamata di aggiornamento a [!DNL Salesforce] non riuscirà e i contatti/lead non verranno aggiornati.

Per mappare correttamente i campi XDM ai campi di destinazione [!DNL (API) Salesforce CRM], effettua le seguenti operazioni:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Add new mapping]**, verrà visualizzata una nuova riga di mappatura sullo schermo.
   ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform per aggiungere una nuova mappatura.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Nella finestra **[!UICONTROL Select source field]**, scegli la categoria **[!UICONTROL Select attributes]** e seleziona l&#39;attributo XDM oppure scegli **[!UICONTROL Select identity namespace]** e seleziona un&#39;identità.
1. Nella finestra **[!UICONTROL Select target field]**, scegli **[!UICONTROL Select identity namespace]** e seleziona un&#39;identità oppure scegli la categoria **[!UICONTROL Select custom attributes]** e seleziona un attributo o definiscine uno utilizzando il campo **[!UICONTROL Attribute name]** come necessario. Per informazioni sugli attributi supportati, consulta la [[!DNL Salesforce CRM] documentazione](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5).
   * Ripeti questi passaggi per aggiungere le seguenti mappature tra lo schema del profilo XDM e [!DNL (API) Salesforce CRM]:

   **Utilizzo dei contatti**

   * Se lavori con *Contatti* all&#39;interno del segmento, fai riferimento al Riferimento agli oggetti in Salesforce per [Contatto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) per definire i mapping per i campi da aggiornare.
   * Puoi identificare i campi obbligatori cercando la parola *Obbligatorio*, indicata nelle descrizioni dei campi nel collegamento precedente.
   * A seconda dei campi che desideri esportare o aggiornare, aggiungi mappature tra lo schema del profilo XDM e [!DNL (API) Salesforce CRM]:

     | Campo origine | Campo di destinazione | Note |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Cognome del contatto fino a 80 caratteri. |
     | `xdm: person.name.firstName` | `Attribute: FirstName` | Il nome del contatto può contenere un massimo di 40 caratteri. |
     | `xdm: personalEmail.address` | `Attribute: Email` | L’indirizzo e-mail del contatto. |

   * Di seguito è riportato un esempio che utilizza queste mappature:
     ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform che mostra le mappature di Target.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Utilizzo dei lead**

   * Se lavori con *Lead* all&#39;interno del segmento, fai riferimento al Riferimento agli oggetti in Salesforce per [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) per definire i mapping per i campi da aggiornare.
   * Puoi identificare i campi obbligatori cercando la parola *Obbligatorio*, indicata nelle descrizioni dei campi nel collegamento precedente.
   * A seconda dei campi che desideri esportare o aggiornare, aggiungi mappature tra lo schema del profilo XDM e [!DNL (API) Salesforce CRM]:

     | Campo origine | Campo di destinazione | Note |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Cognome della sequenza fino a 80 caratteri. |
     | `xdm: b2b.companyName` | `Attribute: Company` | `Mandatory`. L&#39;azienda del lead. |
     | `xdm: personalEmail.address` | `Attribute: Email` | Indirizzo e-mail del lead. |

   * Di seguito è riportato un esempio che utilizza queste mappature:
     ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform che mostra le mappature di Target.](../../assets/catalog/crm/salesforce/mappings-leads.png)

Dopo aver fornito i mapping per la connessione di destinazione, selezionare **[!UICONTROL Next]**.

### Esempio di esportazione e pianificazione di un pubblico {#schedule-segment-export-example}

Durante l&#39;esecuzione del passaggio [Pianifica esportazione pubblico](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) è necessario mappare manualmente i tipi di pubblico attivati da Experience Platform al campo personalizzato corrispondente in [!DNL Salesforce].

A questo scopo, selezionare ogni segmento, quindi immettere il nome del campo personalizzato da [!DNL Salesforce] nel campo [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**. Consulta la sezione [Creare campi personalizzati all&#39;interno di [!DNL Salesforce]](#prerequisites-custom-field) per indicazioni e best practice sulla creazione di campi personalizzati in [!DNL Salesforce].

Ad esempio, se il campo personalizzato [!DNL Salesforce] è `crm_2_seg`, specifica questo valore in [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** per popolare i tipi di pubblico da Experience Platform in questo campo personalizzato.

Di seguito è riportato un esempio di campo personalizzato da [!DNL Salesforce]:
Schermata dell&#39;interfaccia utente ![[!DNL Salesforce] che mostra il campo personalizzato.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Di seguito è riportato un esempio che indica la posizione di [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**:
![Esempio di schermata dell&#39;interfaccia utente di Experience Platform che mostra l&#39;esportazione pianificata del pubblico.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Come mostrato sopra, [!DNL Salesforce] **[!UICONTROL Field Name]** corrisponde esattamente al valore specificato in [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**.

A seconda del caso d&#39;uso, tutti i tipi di pubblico attivati possono essere mappati allo stesso campo personalizzato [!DNL Salesforce] o a **[!UICONTROL Field Name]** diversi in [!DNL Salesforce CRM]. Un esempio tipico basato sull’immagine mostrata sopra potrebbe essere.

| Nome segmento [!DNL Salesforce CRM] | [!DNL Salesforce] **[!UICONTROL Field Name]** | [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Ripeti questa sezione per ogni segmento di Experience Platform attivato.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Selezionare **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** per passare all&#39;elenco delle destinazioni.
   ![Schermata dell&#39;interfaccia utente di Experience Platform che mostra le destinazioni di navigazione.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Selezionare la destinazione e verificare che lo stato sia **[!UICONTROL enabled]**.
   ![Schermata dell&#39;interfaccia utente di Experience Platform che mostra le destinazioni dell&#39;esecuzione del flusso di dati.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Passa alla scheda **[!UICONTROL Activation data]**, quindi seleziona un nome di pubblico.
   ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Controlla il riepilogo del pubblico e assicurati che il conteggio dei profili corrisponda al conteggio creato all’interno del segmento.
   ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform che mostra il segmento.](../../assets/catalog/crm/salesforce/segment.png)

1. Infine, accedi al sito web Salesforce e verifica se i profili del pubblico sono stati aggiornati.

   **Utilizzo dei contatti**

   * Se hai selezionato *Contatti* all&#39;interno del segmento Experience Platform, passa alla pagina **[!DNL Apps]** > **[!DNL Contacts]**.
     ![Schermata di Salesforce CRM che mostra la pagina dei contatti con i profili del segmento.](../../assets/catalog/crm/salesforce/contacts.png)

   * Seleziona un *Contatto* e verifica se i campi sono aggiornati. È possibile vedere che ogni stato del pubblico in [!DNL Salesforce CRM] è stato aggiornato con lo stato del pubblico corrispondente da Experience Platform, in base al valore **[!UICONTROL Mapping ID]** fornito durante la [pianificazione del pubblico](#schedule-segment-export-example).
     ![Schermata di Salesforce CRM che mostra la pagina Dettagli contatto con gli stati aggiornati del pubblico.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Utilizzo dei lead**

   * Se hai selezionato *Lead* nel segmento Experience Platform, passa alla pagina **[!DNL Apps]** > **[!DNL Leads]**.
     ![Schermata di Salesforce CRM che mostra la pagina Lead con i profili del segmento.](../../assets/catalog/crm/salesforce/leads.png)

   * Seleziona un *lead* e controlla se i campi sono aggiornati. È possibile vedere che ogni stato del pubblico in [!DNL Salesforce CRM] è stato aggiornato con lo stato del pubblico corrispondente da Experience Platform, in base al valore **[!UICONTROL Mapping ID]** fornito durante la [pianificazione del pubblico](#schedule-segment-export-example).
     ![Schermata di Salesforce CRM che mostra la pagina Dettagli lead con stati di pubblico aggiornati.](../../assets/catalog/crm/salesforce/lead-info.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

### Sono stati riscontrati errori sconosciuti durante la trasmissione degli eventi alla destinazione {#unknown-errors}

* Durante il controllo di un&#39;esecuzione del flusso di dati, è possibile che venga visualizzato il seguente messaggio di errore: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Schermata dell&#39;interfaccia utente di Experience Platform che mostra l&#39;errore.](../../assets/catalog/crm/salesforce/error.png)

   * Per correggere questo errore, verificare che **[!UICONTROL Mapping ID]** fornito nel flusso di lavoro di attivazione alla destinazione [!DNL Salesforce CRM] corrisponda esattamente al valore del tipo di campo personalizzato creato in [!DNL Salesforce]. Consulta la sezione [Creare campi personalizzati all&#39;interno di [!DNL Salesforce]](#prerequisites-custom-field).

* Quando si attiva un segmento, è possibile che venga visualizzato un messaggio di errore: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Per risolvere l&#39;errore, contattare l&#39;amministratore dell&#39;account [!DNL Salesforce] per aggiungere [indirizzi IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) agli intervalli IP attendibili degli account [!DNL Salesforce]. Se hai bisogno di ulteriori indicazioni, consulta la documentazione [!DNL Salesforce] [Limita l&#39;accesso agli intervalli IP attendibili per un&#39;app connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5).

## Risorse aggiuntive {#additional-resources}

Ulteriori informazioni utili dal [portale per sviluppatori di Salesforce](https://developer.salesforce.com/):

* [Guida introduttiva](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Crea un record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Tipi di pubblico per consigli personalizzati](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Utilizzo di risorse composite](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Questa destinazione sfrutta l&#39;API [Upsert Multiple Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) invece della chiamata API [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts).
