---
title: (API) Oracle di connessione Eloqua
description: La destinazione (API) Oracle Eloqua ti consente di esportare i dati del tuo account e attivarli all’interno di Oracle Eloqua per le tue esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 3d54b89ab5f956710ad595a0e8d3567e1e773d0a
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) consente agli esperti di marketing di pianificare ed eseguire campagne offrendo al tempo stesso un’esperienza cliente personalizzata per i loro potenziali clienti. Grazie alla gestione integrata dei lead e alla creazione semplice delle campagne, gli esperti di marketing possono coinvolgere il pubblico giusto al momento giusto nel percorso dell’acquirente e raggiungere in modo elegante il pubblico su più canali, tra cui e-mail, ricerca display, video e dispositivi mobili. I team di vendita possono chiudere più offerte a un ritmo più veloce, aumentando il ROI del marketing attraverso informazioni in tempo reale.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [Aggiornare un contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) dal [!DNL Oracle Eloqua] API REST, che consente di: **aggiorna identità** all’interno di un segmento in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utilizza [Autenticazione di base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) comunicare con [!DNL Oracle Eloqua] API REST. Istruzioni per l&#39;autenticazione al tuo [!DNL Oracle Eloqua] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

Il reparto marketing di una piattaforma online vuole trasmettere una campagna di marketing basata su e-mail a un pubblico specifico di lead. Il team marketing della piattaforma può aggiornare le informazioni sui lead esistenti tramite Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti a [!DNL Oracle Eloqua], che può quindi essere utilizzato per inviare l’e-mail della campagna di marketing.

## Prerequisiti {#prerequisites}

### Prerequisiti per l’Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Oracle Eloqua] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

Consulta la documentazione di Experience Platform per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

### [!DNL Oracle Eloqua] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform al tuo [!DNL Oracle Eloqua] account necessario [!DNL Oracle Eloqua] conto.

Inoltre, è necessario almeno *&quot;Utenti avanzati - Autorizzazioni di marketing&quot;* per [!DNL Oracle Eloqua] istanza. Fai riferimento a *&quot;Gruppi di sicurezza&quot;* sezione [Accesso sicuro degli utenti](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) pagina guida. L’accesso è richiesto dalla destinazione a livello di programmazione [determinare l&#39;URL di base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) quando si richiama il [!DNL Oracle Eloqua] API.

#### Raccogli [!DNL Oracle Eloqua] credenziali {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL Oracle Eloqua] destinazione:

| Credenziali | Descrizione |
| --- | --- |
| `Company Name` | Il nome dell&#39;azienda associato al tuo [!DNL Oracle Eloqua] conto. <br>In seguito, utilizzerai le `Company Name` e [!DNL Oracle Eloqua] `Username` come stringa concatenata da utilizzare come **[!UICONTROL Nome utente]** quando [autenticazione alla destinazione](#authenticate). |
| `Username` | Il nome utente del tuo [!DNL Oracle Eloqua] conto. |
| `Password` | La password della [!DNL Oracle Eloqua] conto. |
| `Pod` | [!DNL Oracle Eloqua] supporta più data center, ciascuno con un nome di dominio univoco. [!DNL Oracle Eloqua] si riferisce a questi come &quot;baccelli&quot;, ci sono attualmente sette in totale - p01, p02, p03, p04, p06, p07 e p08. Per ottenere il POD su cui ti trovi, accedi a [!DNL Oracle Eloqua] e prendi nota dell’URL nel browser dopo aver effettuato l’accesso. Ad esempio, se l’URL del browser è `secure.p01.eloqua.com` le `pod` è `p01`. Fai riferimento a [determinazione del POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) per ulteriori informazioni. |

Fai riferimento a [Accesso a [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) a titolo indicativo.

## Guardrail {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] i campi di contatto personalizzati vengono creati automaticamente utilizzando i nomi dei segmenti selezionati durante il **[!UICONTROL Selezionare segmenti]** passo.


* [!DNL Oracle Eloqua] ha un limite massimo di 250 campi di contatto personalizzati.
* Prima di esportare nuovi segmenti, assicurati che il numero di segmenti di Platform e il numero di segmenti esistenti all’interno di [!DNL Oracle Eloqua] non superare questo limite.
* Se questo limite viene superato, si verifica un errore nell’Experience Platform. Questo perché il [!DNL Oracle Eloqua] L’API non convalida la richiesta e risponde con un - *400 Errore di convalida* - messaggio di errore che descrive il problema.
* Se hai raggiunto il limite sopra specificato, devi rimuovere le mappature esistenti dalla tua destinazione ed eliminare i campi di contatto personalizzati corrispondenti nel tuo [!DNL Oracle Eloqua] prima di poter esportare altri segmenti.

* Fai riferimento a [[!DNL Oracle Eloqua] Creazione di campi di contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) per informazioni sui limiti aggiuntivi.

## Identità supportate {#supported-identities}

[!DNL Oracle Eloqua] supporta l’aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Obbligatorio |
|---|---|---|
| `EloquaId` | Identificatore univoco del contatto. | Sì |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Per ogni segmento selezionato in Platform, il corrispondente [!DNL Oracle Eloqua] lo stato del segmento viene aggiornato con il relativo stato del segmento da Platform.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cercare [!DNL (API) Oracle Eloqua]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL Marketing e-mail]** categoria.

### Autentica a destinazione {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nome società\Nome utente"
>abstract="Compila questo campo con il nome società e il nome utente di Oracle Eloqua nel modulo `{COMPANY_NAME}\{USERNAME}`"

Compila i campi richiesti di seguito. Fai riferimento a [Raccogli [!DNL Oracle Eloqua] credenziali](#gather-credentials) sezione per eventuali indicazioni.
* **[!UICONTROL Password]**: La password della [!DNL Oracle Eloqua] conto.
* **[!UICONTROL Nome utente]**: Una stringa concatenata composta da [!DNL Oracle Eloqua] Nome della società e [!DNL Oracle Eloqua] Nome utente.<br>Il valore concatenato assume la forma di `{COMPANY_NAME}\{USERNAME}`.<br> Nota: non utilizzare parentesi graffe o spazi e non mantenere il `\`. <br>Ad esempio, se [!DNL Oracle Eloqua] Il nome della società è `MyCompany` e [!DNL Oracle Eloqua] Nome utente `Username`, il valore concatenato utilizzato nella variabile **[!UICONTROL Nome utente]** campo `MyCompany\Username`.

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **[!UICONTROL Connesso]** stato con un segno di spunta verde. Puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Per trovare il numero del tuo pod, accedi all&#39;Oracle Eloqua. Osserva l’URL nel browser dopo aver effettuato l’accesso. "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge Base - scopri il tuo numero di Pod"

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Pod]**: Per ottenere `pod` attivato, accedere a [!DNL Oracle Eloqua] e prendi nota dell’URL nel browser dopo aver effettuato l’accesso. Ad esempio, se l’URL del browser è `secure.p01.eloqua.com` la `pod` valore da selezionare `p01`. Fai riferimento a [Raccogli [!DNL Oracle Eloqua] credenziali](#gather-credentials) sezione per ulteriori informazioni.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Oracle Eloqua] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare i campi XDM su [!DNL Oracle Eloqua] campi di destinazione, segui questi passaggi:

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM o scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità.
1. In **[!UICONTROL Selezionare il campo di destinazione]** finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità, oppure scegliere **[!UICONTROL Seleziona attributi personalizzati]** e digita il nome dell&#39;attributo desiderato nel **[!UICONTROL Nome attributo]** campo . Il nome dell&#39;attributo fornito deve corrispondere a un attributo di contatto esistente in [!DNL Oracle Eloqua]. Vedi [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) per i nomi degli attributi esatti che è possibile utilizzare in [!DNL Oracle Eloqua].
   * Ripeti questi passaggi per aggiungere le mappature degli attributi necessarie e desiderate tra lo schema del profilo XDM e [!DNL Oracle Eloqua]: | Campo di origine | Campo di destinazione | Obbligatorio | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| Sì | |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sì | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * Di seguito è riportato un esempio con le mappature precedenti:
      ![Esempio di schermata dell’interfaccia utente della piattaforma con mappature degli attributi.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Attributi specificati nel **[!UICONTROL Campo di destinazione]** devono essere denominati esattamente come specificato nel [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) poiché questi attributi formano il corpo della richiesta.
>* Attributi specificati nel **[!UICONTROL Campo di origine]** non seguire alcuna restrizione di questo tipo. Puoi mapparla in base alle tue esigenze, tuttavia se il formato dei dati non è corretto quando viene inviato a [!DNL Oracle Eloqua] si tradurrà in un errore. Ad esempio, puoi mappare il **[!UICONTROL Campo di origine]** spazio dei nomi identità `contact key`, `ABC ID` ecc. a **[!UICONTROL Campo di destinazione]** : `EloquaId` dopo aver verificato che i valori ID corrispondano al formato accettato da [!DNL Oracle Eloqua].
>* La `EloquaID` la mappatura è obbligatoria per aggiornare gli attributi corrispondenti all&#39;identità.
>* La `emailAddress` la mappatura è obbligatoria. In caso contrario, l’API genera un errore come mostrato di seguito:
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

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

>[!NOTE]
>
>La destinazione aggiunge automaticamente un identificatore univoco ai nomi dei segmenti selezionati in ogni esecuzione quando invia le informazioni sul campo di contatto a [!DNL Oracle Eloqua]. In questo modo i nomi dei campi di contatto corrispondenti ai nomi dei segmenti non si sovrappongono. Fai riferimento a [Convalida esportazione dati](#exported-data) esempio di schermata di una sezione [!DNL Oracle Eloqua] Pagina Dettagli contatto con campo di contatto personalizzato creato utilizzando i nomi dei segmenti.

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all’elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa alla **[!UICONTROL Dati di attivazione]** , quindi seleziona un nome di segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio all’interno del segmento.
   ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra il segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Accedi a [!DNL Oracle Eloqua] , quindi passare al **[!UICONTROL Panoramica dei contatti]** per verificare se sono stati aggiunti i profili dal segmento. Per visualizzare lo stato del segmento, approfondire **[!UICONTROL Dettaglio contatto]** e controlla se è stato creato il campo contatto con il nome del segmento selezionato come prefisso.

![Schermata dell’interfaccia utente Eloqua di Oracle che mostra la pagina Dettagli contatto con il campo di contatto personalizzato creato con il nome del segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Durante la creazione della destinazione, potresti ricevere uno dei seguenti messaggi di errore: `400: There was a validation error` o `400 BAD_REQUEST`. Questo accade quando superi il limite di 250 campi di contatto personalizzati, come descritto nel [guardrail](#guardrails) sezione . Per correggere questo errore, assicurati di non superare il limite del campo di contatto personalizzato in [!DNL Oracle Eloqua].
![Schermata dell’interfaccia utente della piattaforma che mostra l’errore.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Fai riferimento a [[!DNL Oracle Eloqua] Codici di stato HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Errori di convalida](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) pagine per un elenco completo di stato e codici di errore con spiegazioni.

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli, consulta la sezione [!DNL Oracle Eloqua] documentazione:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST per Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti della documentazione effettuati al connettore di destinazione.

+++ Visualizza la finestra delle modifiche

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2023 | Aggiornamento della documentazione | <ul><li>Abbiamo aggiornato il [casi d’uso](#use-cases) con un esempio più chiaro di quando i clienti trarrebbero vantaggio dall’utilizzo di questa destinazione.</li> <li>Abbiamo aggiornato il [mappatura](#mapping-considerations-example) con esempi chiari di mappature obbligatorie e facoltative.</li> <li>Abbiamo aggiornato il [Collegati alla destinazione](#connect) con un esempio su come creare il valore concatenato per il **[!UICONTROL Nome utente]** utilizzando [!DNL Oracle Eloqua] Nome della società e [!DNL Oracle Eloqua] Nome utente. (PLATIR-28343)</li><li>Abbiamo aggiornato il [Raccogli [!DNL Oracle Eloqua] credenziali](#gather-credentials) e [Compila i dettagli della destinazione](#destination-details) sezioni con orientamenti [!DNL Oracle Eloqua] **[!UICONTROL Pod]** selezione. La *&quot;Pod&quot;* viene utilizzato dalla destinazione per creare l’URL di base per le chiamate API. La [[!DNL Oracle Eloqua] prerequisiti](#prerequisites-destination) è stata inoltre aggiornata la sezione con istruzioni sull’assegnazione *&quot;Utenti avanzati - Autorizzazioni di marketing&quot;* come richiesto *&quot;Gruppi di sicurezza&quot;* per [!DNL Oracle Eloqua] istanza.</li></ul> |
| Marzo 2023 | Versione iniziale | Pubblicazione iniziale della destinazione e della documentazione. |

{style="table-layout:auto"}

+++