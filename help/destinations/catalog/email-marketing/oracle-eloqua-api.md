---
title: (API) Connessione Oracle Eloqua
description: La destinazione Oracle Eloqua (API) consente di esportare i dati dell’account e attivarli in Oracle Eloqua in base alle esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 4%

---


# Connessione [!DNL (API) Oracle Eloqua]

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) Consente agli esperti di marketing di pianificare ed eseguire campagne, offrendo al contempo un esperienza del cliente personalizzato per i loro potenziali clienti. Con la gestione integrata dei lead e la facile creazione di campagne, aiuta gli esperti di marketing a coinvolgere il pubblico giusto al momento giusto nel percorso dell&#39;acquirente e si adatta in modo elegante per raggiungere il pubblico attraverso i canali, tra cui e-mail, display ricerca, video e dispositivi mobili. I team di vendita possono concludere più trattative a un ritmo più veloce, aumentando marketing ROI attraverso informazione approfondita in tempo reale.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta l&#39;operazione [Aggiorna un contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) dall&#39;API [!DNL Oracle Eloqua] REST, che consente di **aggiornare le identità** all&#39;interno di un pubblico in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utilizza [Basic Authentication](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) per comunicare con l&#39;API [!DNL Oracle Eloqua] REST. Le istruzioni per eseguire l&#39;autenticazione al proprio [!DNL Oracle Eloqua] istanza sono disponibili più avanti, nella sezione Autenticare fino alla destinazione[&#128279;](#authenticate).

## Casi d’uso {#use-cases}

Il reparto marketing di una piattaforma online vuole trasmettere un&#39;e-mail basata sulla campagna di marketing a un pubblico curato di lead. Il team marketing della piattaforma può aggiornare le informazioni lead esistenti tramite Adobe Experience Platform, versione i tipi di pubblico dai propri dati offline e inviare questi tipi di pubblico a [!DNL Oracle Eloqua], che può quindi essere utilizzato per inviare l&#39;e-mail campagna di marketing.

## Prerequisiti {#prerequisites}

### Prerequisiti di Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL Oracle Eloqua], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=it) e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=it) creati in [!DNL Experience Platform].

Se hai bisogno di indicazioni sugli stati del pubblico, consulta la documentazione di Experience Platform per il gruppo di campi dello schema [Dettagli sull&#39;iscrizione al pubblico](/help/xdm/field-groups/profile/segmentation.md).

### [!DNL Oracle Eloqua] prerequisiti {#prerequisites-destination}

Per esportare dati da Experience Platform all&#39;account [!DNL Oracle Eloqua], è necessario disporre di un account [!DNL Oracle Eloqua].

Inoltre, hai bisogno almeno delle *&quot;Avanzate istanza utenti - autorizzazioni marketing&quot;* per il tuo [!DNL Oracle Eloqua] . Per istruzioni, consultate la *[sezione &quot;Gruppi di sicurezza&quot;* nella pagina accesso](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) utente protette. Il accesso è richiesto dalla destinazione per determinare a [livello di codice il URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) di base quando si richiama l&#39;API [!DNL Oracle Eloqua] .

#### Raccogli [!DNL Oracle Eloqua] credenziali {#gather-credentials}

Annotare gli elementi riportati di seguito prima di eseguire l&#39;autenticazione nella destinazione [!DNL Oracle Eloqua]:

| Credenziali | Descrizione |
| --- | --- |
| `Company Name` | Il nome della società associata al account [!DNL Oracle Eloqua] . <br>In seguito utilizzerai la `Company Name` e [!DNL Oracle Eloqua] `Username` come stringa concatenata da utilizzare come **[!UICONTROL nome]** utente durante [l&#39;autenticazione alla destinazione](#authenticate). |
| `Username` | Il nome utente del tuo [!DNL Oracle Eloqua] account. |
| `Password` | La password del tuo [!DNL Oracle Eloqua] account. |
| `Pod` | [!DNL Oracle Eloqua] Supporta più data center, ognuno con un nome di dominio univoco. [!DNL Oracle Eloqua] si riferisce a questi come &quot;pod&quot;, ce ne sono attualmente sette in totale: P01, P02, P03, P04, P06, P07 e P08. Per ottenere su quale POD ti trovi, login e [!DNL Oracle Eloqua] annota il URL nella tua browser dopo aver effettuato correttamente l&#39;accesso. Ad esempio, se l&#39;URL del browser è `secure.p01.eloqua.com`, `pod` è `p01`. Per ulteriori informazioni, consultare la pagina [determinazione del POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua). |

Consulta [Accesso a [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) per maggiori informazioni.

## Guardrail {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] campi di contatto personalizzati vengono creati automaticamente utilizzando i nomi dei tipi di pubblico selezionati durante il passaggio **[!UICONTROL Seleziona segmenti]**.

* [!DNL Oracle Eloqua] ha un limite massimo di 250 campi contatto personalizzati.
* Prima di esportare nuovi tipi di pubblico, assicurati che il numero di tipi di pubblico di Experience Platform e il numero di tipi di pubblico esistenti entro [!DNL Oracle Eloqua] non superino questo limite.
* Se questo limite viene superato, si verificherà un errore in Experience Platform. Questo perché l&#39;API [!DNL Oracle Eloqua] non riesce a convalidare il richiesta e risponde con un - *400: si è verificato un errore convalida* - messaggio di errore che descrive il problema.
* Se è stato raggiunto il limite specificato in precedenza, è necessario rimuovere le mappature esistenti dalla destinazione ed eliminare i campi dei contatti personalizzati corrispondenti nell&#39;account [!DNL Oracle Eloqua] prima di poter esportare altri segmenti.

* Per informazioni sui limiti aggiuntivi, vedere la pagina [[!DNL Oracle Eloqua] Creazione dei campi contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm).

## Identità supportate {#supported-identities}

[!DNL Oracle Eloqua] Supporta l&#39;aggiornamento delle identità descritte nella tabella seguente. Scopri di più sulle [identità](/help/identity-service/features/namespaces.md).

| Identità Target | Descrizione | Obbligatorio |
|---|---|---|
| `EloquaId` | Identificatore univoco del contatto. | Sì |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Per ogni pubblico selezionato in Experience Platform, lo stato del segmento [!DNL Oracle Eloqua] corrispondente viene aggiornato da Experience Platform in base allo stato del pubblico.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l&#39;aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle destinazioni in [&#128279;](/help/destinations/destination-types.md#streaming-destinations)streaming.</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[[!UICONTROL autorizzazioni]](/help/access-control/home.md#permissions) Visualizza Destinazioni&rbrack;** e **[!UICONTROL Gestisci destinazioni]** [accesso controllo. Leggi la panoramica](/help/access-control/ui/overview.md) sul &lbrack;controllo accesso o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

All&#39;interno di **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL (API) Oracle Eloqua]. In alternativa, puoi trovarlo nella categoria **[!UICONTROL E-mail marketing]**.

### Autenticarsi nella destinazione {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nome società\Nome utente"
>abstract="Compila questo campo con il nome della tua società e il nome utente di Oracle Eloqua nel modulo `{COMPANY_NAME}\{USERNAME}`"

Compila i campi obbligatori di seguito. Per eventuali indicazioni, consulta la [sezione Raccogli [!DNL Oracle Eloqua] le credenziali](#gather-credentials) .
* **[!UICONTROL Password]**: la password del tuo [!DNL Oracle Eloqua] account.
* **&#x200B;**&#x200B;Nome utente: una stringa concatenata composta dal nome della società [!DNL Oracle Eloqua] e dal [!DNL Oracle Eloqua] nome utente.<br>Il valore concatenato assume la forma di `{COMPANY_NAME}\{USERNAME}`.<br>Nota, non utilizzare parentesi graffe o spazi e conservare .`\` <br>Ad esempio, se il nome della società è e il nome utente è `Username`, il valore concatenato che verrà utilizzato nel **[!UICONTROL campo Nome]** utente è `MyCompany\Username`.[!DNL Oracle Eloqua] `MyCompany` [!DNL Oracle Eloqua]

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell&#39;interfaccia utente di Experience Platform che mostra come eseguire l&#39;autenticazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Per trovare il numero del tuo pod, accedi a Oracle Eloqua. Osserva l’URL nel browser dopo aver effettuato correttamente l’accesso. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell&#39;interfaccia utente di Experience Platform con i dettagli della destinazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Pod]**: per ottenere i `pod` a cui sei connesso, accedi a [!DNL Oracle Eloqua] e annota l&#39;URL nel browser dopo aver effettuato l&#39;accesso. Ad esempio, se il browser URL è `secure.p01.eloqua.com` il `pod` valore da selezionare è `p01`. Per ulteriori indicazioni, consulta la [sezione Raccolta [!DNL Oracle Eloqua] delle credenziali](#gather-credentials) .

### Abilitare gli avvisi {#enable-alerts}

È possibile abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la destinazione. Seleziona un avviso dall&#39;elenco a cui iscriverti per ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida sulla [sottoscrizione agli avvisi relativi alle destinazioni utilizzando il interfaccia](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, selezionare **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico dal Adobe Experience Platform alla [!DNL Oracle Eloqua] destinazione, è necessario eseguire la fase di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Experience Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare i campi XDM ai campi di destinazione [!DNL Oracle Eloqua], effettua le seguenti operazioni:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Viene visualizzata una nuova riga di mappatura.
1. **[!UICONTROL Nella finestra Seleziona campo sorgente]**, scegliere la **[!UICONTROL categoria Seleziona attributi]** e selezionare l&#39;attributo XDM oppure selezionare lo spazio **dei nomi Seleziona identità e selezionare un&#39;identità**.
1. **[!UICONTROL Nella finestra Seleziona campo destinazione]** scegliere **[!UICONTROL Seleziona spazio]** dei nomi identità e selezionare un&#39;identità oppure scegliere **[!UICONTROL Seleziona attributi]** personalizzati e digitare il nome dell&#39;attributo desiderato nel **[!UICONTROL campo Nome attributo]**. Il nome dell&#39;attributo fornito deve corrispondere a un attributo di contatto esistente in [!DNL Oracle Eloqua]. Vedere [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) i nomi esatti degli attributi che è possibile utilizzare in [!DNL Oracle Eloqua].

   * Ripeti questi passaggi per aggiungere la mappatura degli attributi richiesta e quella desiderata tra lo schema del profilo XDM e [!DNL Oracle Eloqua]:

     | Campo origine | Campo di destinazione | Obbligatorio |
     |---|---|---|
     | `IdentityMap: Eid` | `Identity: EloquaId` | Sì |
     | `xdm: personalEmail.address` | `Attribute: emailAddress` | Sì |
     | `xdm: personName.firstName` | `Attribute: firstName` | |
     | `xdm: personName.lastName` | `Attribute: lastName` | |
     | `xdm: workAddress.street1` | `Attribute: address1` | |
     | `xdm: workAddress.street2` | `Attribute: address2` | |
     | `xdm: workAddress.street3` | `Attribute: address3` | |
     | `xdm: workAddress.postalCode` | `Attribute: postalCode` | |
     | `xdm: workAddress.country` | `Attribute: country` | |
     | `xdm: workAddress.city` | `Attribute: city` | |

   * Di seguito è riportato un esempio con le mappature di cui sopra:

     ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform con mappature di attributi.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Gli attributi specificati nel campo **[!UICONTROL Target]** devono essere denominati esattamente come specificato in [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html), in quanto formeranno il corpo della richiesta.
>* Gli attributi specificati nel campo **[!UICONTROL Source]** non seguono alcuna restrizione di questo tipo. È possibile eseguirne la mappatura in base alle proprie esigenze. Tuttavia, se il formato dei dati non è corretto al momento del push in [!DNL Oracle Eloqua], si verificherà un errore. Ad esempio, è possibile mappare il **[!UICONTROL campo Source]** spazio dei nomi dell&#39;identità `contact key`, `ABC ID` ecc. al **[!UICONTROL campo di destinazione]**: `EloquaId` dopo aver verificato che i valori ID corrispondano al formato accettato da [!DNL Oracle Eloqua].
>* Il mapping `EloquaID` è obbligatorio per aggiornare gli attributi corrispondenti all&#39;identità.
>* Il mapping `emailAddress` è obbligatorio. Senza di esso, l’API genera un errore come mostrato di seguito:
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

Al termine delle mappature per la connessione di destinazione, selezionare **[!UICONTROL Successivo]**.

>[!NOTE]
>
>La destinazione suffissa automaticamente un identificatore univoco ai nomi dei destinatari selezionati in ogni esecuzione quando si inviano le informazioni sul campo contatto a [!DNL Oracle Eloqua]. Ciò garantisce che i nomi dei campi di contatto corrispondenti ai nomi dei tipi di pubblico non si sovrappongano. Fare riferimento alla [sezione Convalida esportazione dati](#exported-data) schermata esempio di pagina [!DNL Oracle Eloqua] Dettagli contatto con campo contatto personalizzato creato utilizzando i nomi del pubblico.

## Convalidare l&#39;esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, seguire i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all&#39;elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa alla scheda **[!UICONTROL Dati attivazione]**, quindi seleziona un nome di pubblico.
   ![Experience Platform interfaccia schermata esempio che mostra Destinazioni Activation dati.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitora il riepilogo del pubblico e assicurati che il conteggio dei profili corrisponda al conteggio all&#39;interno del segmento.
   ![Experience Platform interfaccia schermata esempio che mostra Segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Accedi al [!DNL Oracle Eloqua] sito Web, quindi vai alla **[!UICONTROL pagina Panoramica]** contatti per verificare se i profili del pubblico sono stati aggiunti. Per visualizzare lo stato del pubblico, analizzare in profondità in una **[!UICONTROL pagina Dettagli]** contatto e controlla se il campo contatto con il nome del pubblico selezionato come prefisso è stato creato.

![Oracle Eloqua interfaccia schermata che mostra la pagina Dettagli contatto con il campo contatto personalizzato creato con il nome dell&#39;audience.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le [!DNL Adobe Experience Platform] destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedere Cenni preliminari[&#128279;](/help/data-governance/home.md) sulla governance dei dati.

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Durante la creazione della destinazione, è possibile che venga visualizzato uno dei messaggi di errore seguenti: `400: There was a validation error` o `400 BAD_REQUEST`. Ciò si verifica quando si supera il limite di 250 campi contatto personalizzati, come descritto nella sezione [guardrail](#guardrails). Per correggere l&#39;errore, assicurarsi di non superare il limite del campo contatto personalizzato in [!DNL Oracle Eloqua].
![Experience Platform interfaccia schermata che mostra un errore.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Fare riferimento alle [[!DNL Oracle Eloqua] pagine Codici](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) di stato HTTP ed [[!DNL Oracle Eloqua] Errori](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) di convalida per un elenco completo dei codici di stato ed errore con le spiegazioni.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta la [!DNL Oracle Eloqua] documentazione:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST per il servizio Oracle Eloqua Marketing Cloud](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

In questa sezione vengono acquisite le funzionalità e gli aggiornamenti significativi della documentazione apportati a questo connettore di destinazione.

+++ Visualizza changelog

| Mese di uscita | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2023 | Aggiornamento della documentazione | <ul><li>Abbiamo aggiornato la sezione dei casi[&#128279;](#use-cases) d&#39;uso con un esempio più chiaro di quando i clienti trarrebbero vantaggio dall&#39;utilizzo di questa destinazione.</li> <li>La sezione [mapping](#mapping-considerations-example) è stata aggiornata con chiari esempi di mapping obbligatori e facoltativi.</li> <li>La sezione [Connetti alla destinazione](#connect) è stata aggiornata con un esempio su come creare il valore concatenato per il campo **[!UICONTROL Nome utente]** utilizzando il nome società [!DNL Oracle Eloqua] e il nome utente [!DNL Oracle Eloqua]. (PLATIR-28343)</li><li>Sono state aggiornate le sezioni [Gather [!DNL Oracle Eloqua] credentials](#gather-credentials) e [Fill in destination details](#destination-details) con indicazioni sulla selezione di [!DNL Oracle Eloqua] **[!UICONTROL Pod]**. Il valore *&quot;Pod&quot;* viene utilizzato dalla destinazione per creare l&#39;URL di base per le chiamate API. La sezione [[!DNL Oracle Eloqua] prerequisiti](#prerequisites-destination) è stata inoltre aggiornata con indicazioni sull&#39;assegnazione di *&quot;Utenti avanzati - Autorizzazioni di marketing&quot;* come *&quot;Gruppi di sicurezza&quot;* obbligatori per l&#39;istanza [!DNL Oracle Eloqua].</li></ul> |
| Marzo 2023 | Versione iniziale | Versione di destinazione iniziale e pubblicazione della documentazione. |

{style="table-layout:auto"}

+++