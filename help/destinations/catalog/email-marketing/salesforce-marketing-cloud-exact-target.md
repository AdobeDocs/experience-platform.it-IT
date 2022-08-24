---
keywords: e-mail;e-mail;e-mail;destinazioni;salesforce;api salesforce destinazione marketing cloud
title: (API) Connessione al Marketing Cloud Salesforce
description: La destinazione del Marketing Cloud Salesforce (precedentemente nota come ExactTarget) ti consente di esportare i dati del tuo account e attivarli all’interno del Marketing Cloud Salesforce per le tue esigenze aziendali.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2dda77c3d9a02b53a02128e835abf77ab97ad033
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL (API) Salesforce Marketing Cloud] connection

## Panoramica {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (precedentemente noto come ExactTarget) è una suite di marketing digitale che consente di creare e personalizzare percorsi per visitatori e clienti per personalizzare la loro esperienza.

>[!IMPORTANT]
> 
> Notare la differenza tra questa connessione e l&#39;altra [Collegamento Marketing Cloud Salesforce](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/salesforce-marketing-cloud.html?lang=en) presente nella sezione del catalogo di e-mail marketing . L’altra connessione al Marketing Cloud Salesforce ti consente di esportare i file in una posizione di archiviazione specifica, mentre questa è una connessione in streaming basata su API.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [API REST contatti aggiornamento Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), che ti consente di aggiungere contatti/aggiornare i dati di contatto per le tue esigenze aziendali dopo averli attivati all’interno di un nuovo segmento Salesforce.

Il Marketing Cloud Salesforce utilizza OAuth 2 con le credenziali client come meccanismo di autenticazione per comunicare con l’API REST di Salesforce. Le istruzioni per l’autenticazione nella tua istanza Salesforce sono più avanti qui sotto, nella [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione del Marketing Cloud Salesforce, ecco un esempio di caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Inviare e-mail ai contatti per le campagne di marketing {#use-case-send-emails}

Il reparto vendite di una piattaforma di noleggio di casa vuole trasmettere un&#39;e-mail di marketing a un pubblico di clienti mirati. Il team marketing della piattaforma può aggiungere nuovi contatti / aggiornare i contatti esistenti *(e i loro indirizzi e-mail)* tramite Adobe Experience Platform, crea segmenti dai propri dati offline e invia tali segmenti al Marketing Cloud Salesforce, che può quindi essere utilizzato per inviare l’e-mail della campagna di marketing.

## Prerequisiti {#prerequisites}

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione del Marketing Cloud Salesforce, è necessario disporre di un [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

### Prerequisiti in CRM Salesforce {#prerequisites-destination}

Tieni presente i seguenti prerequisiti in Salesforce, per esportare i dati da Platform al tuo account di Marketing Cloud Salesforce:

#### Devi avere un account Salesforce {#prerequisites-account}

Vai alla Salesforce [processo](https://www.salesforce.com/in/form/signup/freetrial-sales/) per registrare e creare un account Salesforce, se non ne hai già uno.

#### Crea un campo personalizzato all’interno di Salesforce {#prerequisites-custom-field}

È necessario creare un attributo personalizzato del tipo `Text Area Long`, che verrà utilizzato dall’Experience Platform per aggiornare lo stato del segmento all’interno del Marketing Cloud Salesforce. Nel flusso di lavoro per attivare i segmenti sulla destinazione , nella **[Pianificazione del segmento](#schedule-segment-export-example)** in questo passaggio, utilizzerai l’attributo personalizzato come ID di mappatura per ogni segmento attivato.

Consulta la documentazione del Marketing Cloud Salesforce per [creare campi personalizzati](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) se hai bisogno di ulteriori informazioni.

>[!IMPORTANT]
>
> Assicurati di creare l’attributo personalizzato sotto l’attributo &quot;E-mail DemoGraphics&quot; impostato all’interno dell’account del Marketing Cloud Salesforce.

>[!NOTE]
>
> * Il numero di attributi personalizzati consentiti per oggetto varia a seconda della versione di Salesforce. Consulta la documentazione di Salesforce per [campi personalizzati consentiti per oggetto](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) se hai bisogno di ulteriori informazioni.
> * Se hai raggiunto questo limite all’interno di Salesforce, dovrai rimuovere l’attributo personalizzato da Salesforce che è stato utilizzato per memorizzare lo stato del segmento rispetto ai segmenti più vecchi all’interno di Experience Platform prima di poter utilizzare un nuovo mappingId.


Consulta la documentazione Adobe Experience Platform per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

#### Raccogli credenziali Salesforce {#gather-credentials}

Prendi nota degli elementi seguenti prima di eseguire l’autenticazione nella destinazione del Marketing Cloud Salesforce.

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| <ul><li>Prefisso Marketing Cloud Salesforce</li></ul> | Vedi [Prefisso dominio Marketing Cloud Salesforce](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) per ulteriori indicazioni. | <ul><li>Se il tuo dominio è come indicato di seguito, devi utilizzare il valore evidenziato.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com</i></li></ul> |
| <ul><li>ID client</li><li>Segreto client</li></ul> | Fai riferimento a [Documentazione di Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) se hai bisogno di ulteriori informazioni. | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Identità supportate {#supported-identities}

Il Marketing Cloud Salesforce supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| contactKey | Chiave di contatto Salesforce. Fai riferimento a [Documentazione di Salesforce](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) se hai bisogno di ulteriori informazioni. | Obbligatorio |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

![Catalogo](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/catalog.png)

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Schermata di esempio che mostra come eseguire l’autenticazione al Marketing Cloud Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL Sottodominio]**: Prefisso del dominio del Marketing Cloud Salesforce. Ad esempio, se il dominio è *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, è necessario il valore evidenziato.
* **[!UICONTROL ID client]**: Il tuo ID client Salesforce.
* **[!UICONTROL Segreto client]**: Segreto client Salesforce.

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **Connesso** con un segno di spunta verde, puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata di esempio che mostra come compilare i dettagli per il Marketing Cloud Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Nome cliente]**: Può essere qualsiasi valore, tuttavia un valore è obbligatorio. In caso contrario, l’attivazione della destinazione non riuscirà.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform alla destinazione del Marketing Cloud Salesforce, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM sui campi di destinazione del Marketing Cloud Salesforce, segui i passaggi riportati di seguito.

Elenco di mappature attributo che è possibile impostare per [API REST Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) è riportato di seguito. La destinazione utilizza il [API REST per definizione set di attributi di ricerca Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) per recuperare gli attributi definiti in Salesforce per i contatti e specifici per il tuo account.

>[!IMPORTANT]
> 
> Anche se i nomi degli attributi sono uguali al tuo account Salesforce, le mappature per `contactKey` e `personalEmail.address` sono obbligatori.

1. Nel passaggio Mappatura , fai clic su **[!UICONTROL Aggiungi nuova mappatura]**. È ora possibile visualizzare una nuova riga di mappatura sullo schermo.
   ![Aggiungi nuova mappatura](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. Nella finestra seleziona campo di origine, quando selezioni il campo di origine, scegli la **[!UICONTROL Seleziona attributi]** e aggiungi le mappature desiderate.
   ![Mappatura origine](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. Nella finestra seleziona il campo di destinazione, seleziona il campo di destinazione e scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e aggiungi le mappature desiderate.
   ![Mappatura del target](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

1. Per mappare eventuali attributi personalizzati, seleziona la finestra del campo di destinazione, seleziona il campo di destinazione e scegli la **[!UICONTROL Seleziona attributi]** > **Dati demografici e-mail** categoria. Fornisci quindi il nome dell’attributo di destinazione desiderato e aggiungi le mappature desiderate.
   ![Mappatura del target](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

1. Ad esempio, puoi aggiungere la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Salesforce Marketing Cloud] istanza:

   |  | Schema del profilo XDM | [!DNL Salesforce Marketing Cloud] Istanza | Obbligatorio |
   |---|---|---|---|
   | Attributi | <ul><li>person.name.firstName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>Email Demografiche.Nome</code></li><li>Indirizzo e-mail.Indirizzo e-mail</code></li></ul> | <ul><li>-</li><li>Sì</code></li></ul> |
   | Identità | <ul><li>contactKey</code></li></ul> | <ul><li>salesforceContactKey</code></li></ul> | Sì |

1. Di seguito è riportato un esempio che utilizza queste mappature:
   ![Mappatura del target LastName](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### Pianificare l’esportazione dei segmenti e l’esempio {#schedule-segment-export-example}

Quando si eseguono le [Esportazione di segmenti programmata](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) a questo punto, devi mappare manualmente i segmenti di Platform sull’attributo personalizzato in Salesforce.

A questo scopo, seleziona ogni segmento, quindi inserisci l’attributo personalizzato corrispondente da Salesforce nel **[!UICONTROL ID mappatura]** campo .

>[!IMPORTANT]
>
> Il valore utilizzato per l’ID mappatura deve corrispondere esattamente al nome dell’attributo personalizzato creato in Salesforce sotto l’attributo impostato &quot;E-mail DemoGraphics&quot;.

Di seguito è riportato un esempio:
![Esportazione di segmenti programmata](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** per passare all’elenco delle destinazioni.

   ![Sfoglia destinazioni](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selezionare la destinazione e verificare che lo stato sia **[!UICONTROL abilitato]**.

   ![Esecuzione del flusso di dati sulle destinazioni](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Passa alla **[!DNL Activation data]** , quindi seleziona un nome di segmento.

   ![Dati di attivazione delle destinazioni](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio creato all’interno del segmento.

   ![Segmento](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Accedi al sito web del Marketing Cloud Salesforce. Quindi passa alla **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** e controlla se i profili del segmento sono stati aggiunti.

   ![Contatti Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Per verificare se sono stati aggiornati dei profili, passa alla **[!DNL Email]** controlla se i valori attributo del profilo del segmento sono stati aggiornati.

   ![Contatti Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

### Errori sconosciuti durante il push degli eventi al Marketing Cloud Salesforce {#unknown-errors}

Quando controlli un’esecuzione di un flusso di dati, se vedi il messaggio di errore seguente, verifica che l’ID di mappatura fornito in [!DNL Salesforce CRM] per il segmento Platform è valido ed esiste in [!DNL Salesforce CRM].
![Errore](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

## Risorse aggiuntive {#additional-resources}

* [Portale per sviluppatori Salesforce](https://developer.salesforce.com/)

### Limiti {#limits}

* Salesforce impone [limiti tariffari](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
* Fai riferimento a [errori dei limiti di velocità](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) per controllare eventuali errori riscontrati.
* Fai riferimento a [Prezzi di coinvolgimento Marketing Cloud Salesforce](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina a *Scarica il grafico di confronto Full Edition* come pdf che descrive i limiti imposti dal tuo piano.
* La [Panoramica API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) dettagli pagina: limiti aggiuntivi.
* È disponibile un elemento KB che raccoglie questi dettagli [qui](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits#:~:text=Day%2FHour%2FMinute%20Limit&amp;text=We%20recommend%20a%20limit%20of,per%20minute%20for%20SOAP%20calls.&amp;text=As%20has%20be%20added%20in, interazione%20with%20the%20REST%2DAPI).
