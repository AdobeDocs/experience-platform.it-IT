---
keywords: e-mail;e-mail;e-mail;destinazioni;salesforce;api salesforce destinazione marketing cloud
title: (API) Connessione al Marketing Cloud Salesforce
description: La destinazione del Marketing Cloud Salesforce (precedentemente nota come ExactTarget) ti consente di esportare i dati del tuo account e attivarli all’interno del Marketing Cloud Salesforce per le tue esigenze aziendali.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2c778fe087a04261c79b9daf8579666cd0794eb4
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] connection

## Panoramica {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (precedentemente noto come [!DNL ExactTarget]) è una suite di marketing digitale che ti consente di creare e personalizzare percorsi per visitatori e clienti per personalizzare la loro esperienza.

>[!IMPORTANT]
>
>Notare la differenza tra questa connessione e l&#39;altra [[!DNL Salesforce Marketing Cloud] connection](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) presente nella sezione del catalogo di e-mail marketing . L’altra connessione al Marketing Cloud Salesforce ti consente di esportare i file in una posizione di archiviazione specifica, mentre questa è una connessione in streaming basata su API.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [!DNL Salesforce Marketing Cloud] [aggiornare i contatti](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, che ti consente di aggiungere contatti / aggiornare dati di contatto per le tue esigenze aziendali dopo averli attivati in un nuovo [!DNL Salesforce Marketing Cloud] segmento.

[!DNL Salesforce Marketing Cloud] utilizza OAuth 2 con le credenziali client come meccanismo di autenticazione per comunicare con [!DNL Salesforce Marketing Cloud] API. Istruzioni per l&#39;autenticazione al tuo [!DNL Salesforce Marketing Cloud] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Salesforce Marketing Cloud] destinazione, ecco un esempio di caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Inviare e-mail ai contatti per le campagne di marketing {#use-case-send-emails}

Il reparto vendite di una piattaforma di noleggio di casa vuole trasmettere un&#39;e-mail di marketing a un pubblico di clienti mirati. Il team marketing della piattaforma può aggiungere nuovi contatti / aggiornare i contatti esistenti *(e i loro indirizzi e-mail)* tramite Adobe Experience Platform, crea segmenti dai propri dati offline e invia tali segmenti a [!DNL Salesforce Marketing Cloud], che può quindi essere utilizzato per inviare l’e-mail della campagna di marketing.

## Prerequisiti {#prerequisites}

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Salesforce Marketing Cloud] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

### Prerequisiti in [!DNL Salesforce Marketing Cloud] {#prerequisites-destination}

Tieni presente i seguenti prerequisiti per esportare i dati da Platform al tuo [!DNL Salesforce Marketing Cloud] account:

#### Devi avere un [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

Rivolgiti al tuo [!DNL Salesforce Account Executive] per iscriversi al [!DNL Salesforce Marketing Cloud Account Engagement] se non lo hai già.

#### Crea campo personalizzato all’interno di [!DNL Salesforce Marketing Cloud] {#prerequisites-custom-field}

È necessario creare un attributo personalizzato del tipo `Text Area Long`, quale Experience Platform utilizzerà per aggiornare lo stato del segmento in [!DNL Salesforce Marketing Cloud]. Nel flusso di lavoro per attivare i segmenti sulla destinazione , nella **[Pianificazione del segmento](#schedule-segment-export-example)** utilizza l’attributo personalizzato come **[!UICONTROL ID mappatura]** per ogni segmento attivato.

Fai riferimento a [!DNL Salesforce Marketing Cloud] documentazione [creare campi personalizzati](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) se hai bisogno di ulteriori informazioni.

>[!IMPORTANT]
>
> Assicurati di creare l&#39;attributo personalizzato sotto la variabile `Email Demographics` set di attributi nel [!DNL Salesforce Marketing Cloud] conto.

Consulta la documentazione Adobe Experience Platform per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

#### Raccogli credenziali Salesforce {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL Salesforce Marketing Cloud] destinazione.

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| <ul><li>[!DNL Salesforce Marketing Cloud] Prefisso</li></ul> | Vedi [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) per ulteriori indicazioni. | <ul><li>Se il tuo dominio è come indicato di seguito, devi utilizzare il valore evidenziato.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com</i></li></ul> |
| <ul><li>ID client</li><li>Segreto client</li></ul> | Fai riferimento a [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) se hai bisogno di ulteriori informazioni. | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Limiti in [!DNL Salesforce Marketing Cloud] {#limits}

* Salesforce impone [limiti tariffari](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Fai riferimento a [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) per risolvere eventuali limiti probabili riscontrati e ridurre gli errori durante l’esecuzione.
   * Fai riferimento a [[!DNL Salesforce Marketing Cloud] Prezzi di coinvolgimento](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina a *Scarica il grafico di confronto Full Edition* come pdf che descrive i limiti imposti dal tuo piano.
   * La [Panoramica API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) dettagli pagina: limiti aggiuntivi.
   * Fai riferimento a [qui](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) per una pagina che raccoglie questi dettagli.
* Il conteggio di *campi personalizzati consentiti per oggetto* varia in base alla tua Salesforce Edition.
   * Fai riferimento a [!DNL Salesforce] [documentazione](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) per ulteriori indicazioni.
   * Se hai raggiunto il limite definito per *campi personalizzati consentiti per oggetto* entro [!DNL Salesforce Marketing Cloud] dovrai
      * Rimuovi i campi personalizzati precedenti prima di aggiungere nuovi campi personalizzati in [!DNL Salesforce Marketing Cloud].
      * Aggiorna o rimuovi eventuali destinazioni in Platform che utilizzano questi nomi di campo personalizzati precedenti come valore fornito per **[!UICONTROL ID mappatura]** durante il [programmazione dei segmenti](#schedule-segment-export-example) passo.

## Identità supportate {#supported-identities}

[!DNL Salesforce Marketing Cloud] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Chiave di contatto. Fai riferimento a [!DNL Salesforce Marketing Cloud] [documentazione](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) se hai bisogno di ulteriori informazioni. | Obbligatorio |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Ogni stato di segmento in [!DNL Salesforce Marketing Cloud] viene aggiornato con lo stato del segmento corrispondente da Platform, in base alla **[!UICONTROL ID mappatura]** valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL (API) Salesforce Marketing Cloud]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL E-mail marketing]** categoria.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione nel Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL Sottodominio]**: Le [!DNL Salesforce Marketing Cloud] prefisso del dominio. Ad esempio, se il dominio è *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, è necessario il valore evidenziato.
* **[!UICONTROL ID client]**: Le [!DNL Salesforce Marketing Cloud] ID client.
* **[!UICONTROL Segreto client]**: Le [!DNL Salesforce Marketing Cloud] Segreto client.

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **[!UICONTROL Connesso]** con un segno di spunta verde, puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Salesforce Marketing Cloud] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM su [!DNL Salesforce Marketing Cloud] nei campi di destinazione, segui i passaggi seguenti.

>[!IMPORTANT]
>
>Anche se i nomi degli attributi sono uguali a quelli degli utenti [!DNL Salesforce Marketing Cloud] account, le mappature per entrambi `contactKey` e `personalEmail.address` sono obbligatori.

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
   ![Esempio di schermata dell’interfaccia utente della piattaforma per Aggiungi nuova mappatura.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** categoria e seleziona `contactKey`.
   ![Esempio di schermata dell’interfaccia utente della piattaforma per la mappatura sorgente.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. In **[!UICONTROL Selezionare il campo di destinazione]** selezionare il tipo di campo di destinazione in cui si desidera mappare il campo di origine.
   * **[!UICONTROL Seleziona spazio dei nomi identità]**: selezionare questa opzione per mappare il campo di origine a uno spazio dei nomi di identità dall’elenco.
      ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target per salesforceContactKey.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

   * Aggiungi la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Salesforce Marketing Cloud] istanza: Schema del profilo XDM|[!DNL Salesforce Marketing Cloud] Istanza| Obbligatoria| |—|—|—| |`contactKey`|`salesforceContactKey`| Sì |

   * **[!UICONTROL Seleziona attributi personalizzati]**: seleziona questa opzione per mappare il campo di origine a un attributo personalizzato definito in **[!UICONTROL Nome attributo]** campo . Fai riferimento a [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) per un elenco degli attributi supportati. Inoltre, la destinazione utilizza il [API REST per definizione set di attributi di ricerca Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) per recuperare gli attributi definiti in Salesforce per i contatti e specifici per il tuo account.
      ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

   * Ad esempio, a seconda dei valori che desideri aggiornare, aggiungi la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Salesforce Marketing Cloud] istanza: Schema del profilo XDM|[!DNL Salesforce Marketing Cloud] Istanza| |—|—| |`person.name.firstName`|`Email Demographics.First Name`| |`personalEmail.address`|`Email Addresses.Email Address`|

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra le mappature di Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### Pianificare l’esportazione dei segmenti e l’esempio {#schedule-segment-export-example}

Quando si eseguono le [Esportazione di segmenti programmata](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) , devi mappare manualmente i segmenti di Platform su [attributo personalizzato](#prerequisites-custom-field) a Salesforce.

A questo scopo, seleziona ogni segmento, quindi inserisci l’attributo personalizzato corrispondente da Salesforce nel **[!UICONTROL ID mappatura]** campo .

>[!IMPORTANT]
>
>Il valore utilizzato per l’ID mappatura deve corrispondere esattamente al nome dell’attributo personalizzato creato in Salesforce sotto l’attributo impostato &quot;E-mail DemoGraphics&quot;.

Di seguito è riportato un esempio:
![Esempio di schermata dell’interfaccia utente della piattaforma che mostra la pianificazione dell’esportazione di segmenti.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** per passare all’elenco delle destinazioni.
   ![Schermata dell’interfaccia utente della piattaforma che mostra le destinazioni di navigazione.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selezionare la destinazione e verificare che lo stato sia **[!UICONTROL abilitato]**.
   ![Schermata dell’interfaccia utente della piattaforma che mostra l’esecuzione del flusso di dati delle destinazioni.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Passa alla **[!DNL Activation data]** , quindi seleziona un nome di segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio creato all’interno del segmento.
   ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra il segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Accedi a [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) sito web. Quindi passa alla **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** e controlla se i profili del segmento sono stati aggiunti.
   ![Schermata dell’interfaccia utente del Marketing Cloud Salesforce che mostra la pagina Contatti con i profili utilizzati nel segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Per verificare se sono stati aggiornati dei profili, passa alla **[!UICONTROL E-mail]** e verifica se i valori attributo del profilo del segmento sono stati aggiornati. In caso di esito positivo, puoi vedere che lo stato di ciascun segmento in [!DNL Salesforce Marketing Cloud] è stato aggiornato con lo stato del segmento corrispondente da Platform, in base alla **[!UICONTROL ID mappatura]** il valore fornito nella [programmazione dei segmenti](#schedule-segment-export-example) passo.
   ![Schermata dell’interfaccia utente del Marketing Cloud Salesforce che mostra la pagina e-mail Contatti selezionata con stati di segmento aggiornati.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

### Errori sconosciuti durante il push degli eventi al Marketing Cloud Salesforce {#unknown-errors}

Quando controlli un&#39;esecuzione di un flusso di dati, potresti riscontrare il seguente messaggio di errore: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![Schermata dell’interfaccia utente della piattaforma che mostra l’errore.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

Per correggere questo errore, verifica che il **[!UICONTROL ID mappatura]** che hai fornito in [!DNL Salesforce Marketing Cloud] per il segmento Platform è valido ed esiste in [!DNL Salesforce Marketing Cloud].

## Risorse aggiuntive {#additional-resources}

* [[!DNL Salesforce Marketing Cloud] API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
