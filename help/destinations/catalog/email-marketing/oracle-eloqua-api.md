---
title: (API) Connessione Eloqua Oracle
description: La destinazione Oracle Eloqua (API) consente di esportare i dati dell’account e attivarli in Oracle Eloqua in base alle esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 4%

---


# Connessione [!DNL (API) Oracle Eloqua]

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) consente agli addetti marketing di pianificare ed eseguire campagne durante la distribuzione di un&#39;esperienza cliente personalizzata per i loro potenziali clienti. Grazie alla gestione integrata dei lead e alla facile creazione delle campagne, gli esperti di marketing possono coinvolgere il pubblico giusto al momento giusto nel percorso dell’acquirente e scalare in modo elegante, per raggiungere il pubblico su tutti i canali, comprese e-mail, ricerche per display, video e dispositivi mobili. I team di vendita possono chiudere più offerte a una velocità più elevata, aumentando il ROI del marketing attraverso approfondimenti in tempo reale.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta l&#39;operazione [Aggiorna un contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) dall&#39;API REST [!DNL Oracle Eloqua], che consente di **aggiornare le identità** all&#39;interno di un pubblico in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utilizza l&#39;autenticazione di base [](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) per comunicare con l&#39;API REST [!DNL Oracle Eloqua]. Le istruzioni per l&#39;autenticazione nell&#39;istanza [!DNL Oracle Eloqua] sono riportate di seguito, nella sezione [Autentica nella destinazione](#authenticate).

## Casi d’uso {#use-cases}

Il reparto marketing di una piattaforma online desidera trasmettere una campagna di marketing basata su e-mail a un pubblico curato di lead. Il team marketing della piattaforma può aggiornare le informazioni sui lead esistenti tramite Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviarli a [!DNL Oracle Eloqua], che può quindi essere utilizzato per inviare l&#39;e-mail della campagna di marketing.

## Prerequisiti {#prerequisites}

### Experience Platform prerequisiti {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL Oracle Eloqua], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creati in [!DNL Experience Platform].

Se hai bisogno di indicazioni sugli stati del pubblico, consulta la documentazione dell&#39;Experience Platform per il gruppo di campi [Dettagli appartenenza pubblico](/help/xdm/field-groups/profile/segmentation.md).

### [!DNL Oracle Eloqua] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform all&#39;account [!DNL Oracle Eloqua], è necessario disporre di un account [!DNL Oracle Eloqua].

Inoltre, è necessario almeno *&quot;Advanced Users - Marketing permissions&quot;* per l&#39;istanza [!DNL Oracle Eloqua]. Consultare la sezione *&quot;Gruppi di sicurezza&quot;* nella pagina [Accesso utente protetto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) per ulteriori informazioni. L&#39;accesso è richiesto dalla destinazione per [determinare a livello di programmazione l&#39;URL di base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) quando si richiama l&#39;API [!DNL Oracle Eloqua].

#### Raccogli [!DNL Oracle Eloqua] credenziali {#gather-credentials}

Annotare gli elementi riportati di seguito prima di eseguire l&#39;autenticazione nella destinazione [!DNL Oracle Eloqua]:

| Credenziali | Descrizione |
| --- | --- |
| `Company Name` | Il nome società associato al tuo account [!DNL Oracle Eloqua]. <br>In seguito, utilizzerai `Company Name` e [!DNL Oracle Eloqua] `Username` come stringa concatenata da utilizzare come **[!UICONTROL Nome utente]** durante l&#39;autenticazione [nella destinazione](#authenticate). |
| `Username` | Il nome utente dell&#39;account [!DNL Oracle Eloqua]. |
| `Password` | La password del tuo account [!DNL Oracle Eloqua]. |
| `Pod` | [!DNL Oracle Eloqua] supporta più data center, ciascuno con un nome di dominio univoco. [!DNL Oracle Eloqua] si riferisce a questi come &quot;pod&quot;, sono attualmente sette in totale: p01, p02, p03, p04, p06, p07 e p08. Per ottenere il POD a cui accedi, accedi a [!DNL Oracle Eloqua] e annota l&#39;URL nel browser dopo aver effettuato l&#39;accesso. Ad esempio, se l&#39;URL del browser è `secure.p01.eloqua.com`, `pod` è `p01`. Per ulteriori informazioni, consultare la pagina [determinazione del POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua). |

Consulta [Accesso a [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) per maggiori informazioni.

## Guardrail {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] campi di contatto personalizzati vengono creati automaticamente utilizzando i nomi dei tipi di pubblico selezionati durante il passaggio **[!UICONTROL Seleziona segmenti]**.

* [!DNL Oracle Eloqua] ha un limite massimo di 250 campi contatto personalizzati.
* Prima di esportare nuovi tipi di pubblico, assicurati che il numero di tipi di pubblico di Platform e il numero di tipi di pubblico esistenti entro [!DNL Oracle Eloqua] non superino questo limite.
* Se questo limite viene superato, si verifica un errore in Experience Platform. L&#39;API [!DNL Oracle Eloqua] non riesce a convalidare la richiesta e risponde con - *400: si è verificato un errore di convalida* - messaggio di errore che descrive il problema.
* Se è stato raggiunto il limite specificato in precedenza, è necessario rimuovere le mappature esistenti dalla destinazione ed eliminare i campi dei contatti personalizzati corrispondenti nell&#39;account [!DNL Oracle Eloqua] prima di poter esportare altri segmenti.

* Per informazioni sui limiti aggiuntivi, vedere la pagina [[!DNL Oracle Eloqua] Creazione dei campi contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm).

## Identità supportate {#supported-identities}

[!DNL Oracle Eloqua] supporta l&#39;aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Obbligatorio |
|---|---|---|
| `EloquaId` | Identificatore univoco del contatto. | Sì |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Per ogni pubblico selezionato in Platform, lo stato del segmento [!DNL Oracle Eloqua] corrispondente viene aggiornato da Platform in base allo stato del pubblico.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

All&#39;interno di **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL (API) Oracle Eloqua]. In alternativa, puoi trovarlo nella categoria **[!UICONTROL E-mail marketing]**.

### Autenticarsi nella destinazione {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nome società\Nome utente"
>abstract="Compila questo campo con il nome della tua società e il nome utente di Oracle Eloqua nel modulo `{COMPANY_NAME}\{USERNAME}`"

Compila i campi obbligatori di seguito. Per ulteriori informazioni, consulta la sezione [Raccogli [!DNL Oracle Eloqua] credenziali](#gather-credentials).
* **[!UICONTROL Password]**: la password del tuo account [!DNL Oracle Eloqua].
* **[!UICONTROL Nome utente]**: una stringa concatenata composta dal nome dell&#39;azienda [!DNL Oracle Eloqua] e dal nome utente [!DNL Oracle Eloqua].<br>Il valore concatenato è `{COMPANY_NAME}\{USERNAME}`.<br> Nota: non utilizzare parentesi graffe o spazi e mantenere `\`. <br>Ad esempio, se il nome società [!DNL Oracle Eloqua] è `MyCompany` e il nome utente [!DNL Oracle Eloqua] è `Username`, il valore concatenato che utilizzerai nel campo **[!UICONTROL Nome utente]** è `MyCompany\Username`.

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell&#39;interfaccia utente di Platform che mostra come eseguire l&#39;autenticazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Per trovare il numero del tuo pod, accedi a Oracle Eloqua. Osserva l’URL nel browser dopo aver effettuato correttamente l’accesso. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell&#39;interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Pod]**: per ottenere i `pod` a cui sei connesso, accedi a [!DNL Oracle Eloqua] e annota l&#39;URL nel browser dopo aver effettuato l&#39;accesso. Ad esempio, se l&#39;URL del browser è `secure.p01.eloqua.com` il valore `pod` da selezionare è `p01`. Consulta la sezione [Raccogliere [!DNL Oracle Eloqua] credenziali](#gather-credentials) per ulteriori informazioni.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL Oracle Eloqua], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare i campi XDM ai campi di destinazione [!DNL Oracle Eloqua], effettua le seguenti operazioni:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Viene visualizzata una nuova riga di mappatura.
1. Nella finestra **[!UICONTROL Seleziona campo di origine]**, scegli la categoria **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM oppure scegli lo spazio dei nomi **[!UICONTROL Seleziona identità]** e seleziona un&#39;identità.
1. Nella finestra **[!UICONTROL Seleziona campo di destinazione]**, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona un&#39;identità oppure scegli **[!UICONTROL Seleziona attributi personalizzati]** e digita il nome dell&#39;attributo desiderato nel campo **[!UICONTROL Nome attributo]**. Il nome attributo specificato deve corrispondere a un attributo contatto esistente in [!DNL Oracle Eloqua]. Vedere [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) per i nomi di attributo esatti utilizzabili in [!DNL Oracle Eloqua].

   * Ripeti questi passaggi per aggiungere i mapping di attributi richiesti e desiderati tra lo schema del profilo XDM e [!DNL Oracle Eloqua]:

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
     ![Esempio di schermata dell&#39;interfaccia utente di Platform con mappature di attributi.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

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

Al termine della fornitura dei mapping per la connessione di destinazione, selezionare **[!UICONTROL Avanti]**.

>[!NOTE]
>
>La destinazione aggiunge automaticamente un identificatore univoco ai nomi del pubblico selezionato in ogni esecuzione durante l&#39;invio delle informazioni del campo del contatto a [!DNL Oracle Eloqua]. In questo modo i nomi dei campi contatto corrispondenti ai nomi del pubblico non si sovrappongono. Consulta l&#39;[Esempio di schermata della sezione Convalida esportazione dati](#exported-data) di una pagina Dettagli contatto [!DNL Oracle Eloqua] con un campo contatto personalizzato creato utilizzando i nomi del pubblico.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all&#39;elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa alla scheda **[!UICONTROL Dati attivazione]**, quindi seleziona un nome di pubblico.
   ![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Controlla il riepilogo del pubblico e assicurati che il conteggio dei profili corrisponda al conteggio all’interno del segmento.
   ![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra il segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Accedi al sito Web [!DNL Oracle Eloqua], quindi passa alla pagina **[!UICONTROL Panoramica contatti]** per verificare se i profili del pubblico sono stati aggiunti. Per visualizzare lo stato del pubblico, approfondisci una pagina **[!UICONTROL Dettagli contatto]** e verifica se il campo del contatto con il nome del pubblico selezionato come prefisso è stato creato.

![Schermata dell&#39;interfaccia utente Eloqua di Oracle che mostra la pagina Dettagli contatto con il campo contatto personalizzato creato con il nome del pubblico.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Durante la creazione della destinazione, è possibile che venga visualizzato uno dei messaggi di errore seguenti: `400: There was a validation error` o `400 BAD_REQUEST`. Ciò si verifica quando si supera il limite di 250 campi contatto personalizzati, come descritto nella sezione [guardrail](#guardrails). Per correggere l&#39;errore, assicurarsi di non superare il limite del campo contatto personalizzato in [!DNL Oracle Eloqua].
![Schermata dell&#39;interfaccia utente di Platform che mostra l&#39;errore.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Per un elenco completo dei codici di stato e di errore con relative spiegazioni, consultare le pagine [[!DNL Oracle Eloqua] Codici di stato HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Errori di convalida](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html).

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli, vedere la documentazione di [!DNL Oracle Eloqua]:

* [Oracle di automazione marketing Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST per Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti alla documentazione apportati al connettore di destinazione.

+++ Visualizza changelog

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2023 | Aggiornamento della documentazione | <ul><li>Abbiamo aggiornato la sezione [casi d&#39;uso](#use-cases) con un esempio più chiaro di quando i clienti trarrebbero vantaggio dall&#39;utilizzo di questa destinazione.</li> <li>La sezione [mapping](#mapping-considerations-example) è stata aggiornata con chiari esempi di mapping obbligatori e facoltativi.</li> <li>La sezione [Connetti alla destinazione](#connect) è stata aggiornata con un esempio su come creare il valore concatenato per il campo **[!UICONTROL Nome utente]** utilizzando il nome società [!DNL Oracle Eloqua] e il nome utente [!DNL Oracle Eloqua]. (PLATIR-28343)</li><li>Sono state aggiornate le sezioni [Gather [!DNL Oracle Eloqua] credentials](#gather-credentials) e [Fill in destination details](#destination-details) con indicazioni sulla selezione di [!DNL Oracle Eloqua] **[!UICONTROL Pod]**. Il valore *&quot;Pod&quot;* viene utilizzato dalla destinazione per creare l&#39;URL di base per le chiamate API. La sezione [[!DNL Oracle Eloqua] prerequisiti](#prerequisites-destination) è stata inoltre aggiornata con indicazioni sull&#39;assegnazione di *&quot;Utenti avanzati - Autorizzazioni di marketing&quot;* come *&quot;Gruppi di sicurezza&quot;* obbligatori per l&#39;istanza [!DNL Oracle Eloqua].</li></ul> |
| Marzo 2023 | Versione iniziale | Versione di destinazione iniziale e pubblicazione della documentazione. |

{style="table-layout:auto"}

+++