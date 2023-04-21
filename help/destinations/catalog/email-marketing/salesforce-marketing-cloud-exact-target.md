---
keywords: e-mail;e-mail;e-mail;destinazioni;salesforce;api salesforce destinazione marketing cloud
title: (API) Connessione al Marketing Cloud Salesforce
description: La destinazione del Marketing Cloud Salesforce (precedentemente nota come ExactTarget) ti consente di esportare i dati del tuo account e attivarli all’interno del Marketing Cloud Salesforce per le tue esigenze aziendali.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 877bf4886e563e8a571f067c06107776a0c81d5d
workflow-type: tm+mt
source-wordcount: '2911'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] connection

## Panoramica {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (precedentemente noto come [!DNL ExactTarget]) è una suite di marketing digitale che ti consente di creare e personalizzare percorsi per visitatori e clienti per personalizzare la loro esperienza.

>[!IMPORTANT]
>
>Notare la differenza tra questa connessione e l&#39;altra [[!DNL Salesforce Marketing Cloud] connection](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) presente nella sezione del catalogo di e-mail marketing . L’altra connessione al Marketing Cloud Salesforce ti consente di esportare i file in una posizione di archiviazione specifica, mentre questa è una connessione in streaming basata su API.

Confrontato con [!DNL Salesforce Marketing Cloud Account Engagement] più orientato verso **B2B** marketing, [!DNL (API) Salesforce Marketing Cloud] la destinazione è ideale per **B2C** casi d’uso con cicli decisionali transazionali più brevi. Puoi consolidare set di dati più grandi che rappresentano il comportamento del pubblico di destinazione per regolare e migliorare le campagne di marketing assegnando priorità e segmentando i contatti, soprattutto dai set di dati esterni [!DNL Salesforce]. *Nota: Experience Platform dispone anche di una connessione per il [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [!DNL Salesforce Marketing Cloud] [aggiornare i contatti](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, che consente di: **aggiungi contatti e aggiorna dati di contatto** per le tue esigenze aziendali dopo averle attivate in un nuovo [!DNL Salesforce Marketing Cloud] segmento.

[!DNL Salesforce Marketing Cloud] utilizza OAuth 2 con le credenziali client come meccanismo di autenticazione per comunicare con [!DNL Salesforce Marketing Cloud] API. Istruzioni per l&#39;autenticazione al tuo [!DNL Salesforce Marketing Cloud] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL (API) Salesforce Marketing Cloud] destinazione, ecco un esempio di caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Inviare e-mail ai contatti per le campagne di marketing {#use-case-send-emails}

Il reparto vendite di una piattaforma di noleggio di casa vuole trasmettere un&#39;e-mail di marketing a un pubblico di clienti mirati. Il team marketing della piattaforma può aggiungere nuovi contatti / aggiornare i contatti esistenti *(e i loro indirizzi e-mail)* tramite Adobe Experience Platform, crea segmenti dai propri dati offline e invia tali segmenti a [!DNL Salesforce Marketing Cloud], che può quindi essere utilizzato per inviare l’e-mail della campagna di marketing.

## Prerequisiti {#prerequisites}

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL (API) Salesforce Marketing Cloud] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

### Prerequisiti in [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Tieni presente i seguenti prerequisiti per esportare i dati da Platform al tuo [!DNL Salesforce Marketing Cloud] account:

#### Devi avere un [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] un account con sottoscrizione a [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) il prodotto è obbligatorio per procedere.

Rivolgiti a [[!DNL Salesforce] Supporto](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) se non hai un [!DNL Salesforce Marketing Cloud] l&#39;account o il tuo account mancano [!DNL Marketing Cloud Engagement] abbonamento al prodotto.

#### Crea attributi all’interno di [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Quando si attivano i segmenti nel [!DNL (API) Salesforce Marketing Cloud] di destinazione, è necessario inserire un valore nel **[!UICONTROL ID mappatura]** per ogni segmento attivato, nel **[Pianificazione del segmento](#schedule-segment-export-example)** passo.

[!DNL Salesforce] richiede questo valore per leggere e interpretare correttamente i segmenti provenienti da Experience Platform e per aggiornare il loro stato del segmento in [!DNL Salesforce Marketing Cloud]. Consulta la documentazione di Experience Platform per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

Per ogni segmento attivato da Platform a [!DNL Salesforce Marketing Cloud], è necessario creare un attributo del tipo `Text` entro [!DNL Salesforce]. Utilizza la [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] per creare gli attributi. I nomi dei campi attributo vengono utilizzati per [!DNL (API) Salesforce Marketing Cloud] campo di destinazione e deve essere creato sotto `[!DNL Email Demographics system attribute-set]`. Puoi definire il carattere di campo con un massimo di 4000 caratteri, in base alle tue esigenze aziendali. Consulta la sezione [!DNL Salesforce Marketing Cloud] [Tipi di dati delle estensioni dati](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) pagina di documentazione per ulteriori informazioni sui tipi di attributi.

Fai riferimento a [!DNL Salesforce Marketing Cloud] documentazione [creare attributi](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) se hai bisogno di indicazioni sulla creazione degli attributi.

Un esempio della schermata di Data Designer in [!DNL Salesforce Marketing Cloud], in cui aggiungi l’attributo , viene mostrato di seguito:
![Progettazione dati interfaccia utente Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Una vista del [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] set di attributi è mostrato di seguito:
![Set di attributi di dati demografici dell&#39;interfaccia utente di Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

La [!DNL (API) Salesforce Marketing Cloud] la destinazione utilizza [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) per recuperare dinamicamente gli attributi e i relativi set di attributi definiti in [!DNL Salesforce Marketing Cloud].

Vengono visualizzati nella **[!UICONTROL Campo di destinazione]** finestra di selezione quando si imposta [mappatura](#mapping-considerations-example) nel flusso di lavoro a [attiva i segmenti sulla destinazione](#activate). Tieni presente che solo le mappature per gli attributi definiti all’interno di [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` set di attributi supportati.

>[!IMPORTANT]
>
>Within [!DNL Salesforce Marketing Cloud], è necessario creare attributi con un **[!UICONTROL NOME CAMPO]** che corrisponde esattamente al valore specificato in **[!UICONTROL ID mappatura]** per ogni segmento Platform attivato. Ad esempio, la schermata seguente mostra un attributo denominato `salesforce_mc_segment_1`. Quando attivi un segmento a questa destinazione, aggiungi `salesforce_mc_segment_1` come **[!UICONTROL ID mappatura]** per popolare i tipi di pubblico dei segmenti da Experience Platform in questo attributo.

Un esempio di creazione di attributi in [!DNL Salesforce Marketing Cloud], è mostrato di seguito:
![Schermata dell’interfaccia utente del Marketing Cloud Salesforce che mostra un attributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Durante la creazione dell’attributo, non includere spazi bianchi nel nome del campo. Utilizza invece il carattere di sottolineatura `(_)` come separatore.
>* Per distinguere tra gli attributi utilizzati per i segmenti di Platform e altri attributi all’interno di [!DNL Salesforce Marketing Cloud], puoi includere un prefisso o un suffisso riconoscibile per gli attributi utilizzati per i segmenti di Adobe. Ad esempio, anziché `test_segment`, utilizza `Adobe_test_segment` o `test_segment_Adobe`.
>* Se sono già stati creati altri attributi in [!DNL Salesforce Marketing Cloud], puoi utilizzare lo stesso nome del segmento Platform per identificare facilmente il segmento in [!DNL Salesforce Marketing Cloud].


#### Assegnare ruoli utente e autorizzazioni in [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Come [!DNL Salesforce Marketing Cloud] supporta i ruoli personalizzati a seconda del caso d’uso; all’utente devono essere assegnati i ruoli pertinenti per aggiornare gli attributi all’interno di [!DNL Salesforce Marketing Cloud] set di attributi. Di seguito è riportato un esempio di ruoli assegnati a un utente:
![Interfaccia utente Marketing Cloud Salesforce per un utente selezionato che mostra i ruoli assegnati.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

A seconda dei ruoli [!DNL Salesforce Marketing Cloud] l&#39;utente è stato assegnato, è necessario anche assegnare le autorizzazioni al [!DNL Salesforce Marketing Cloud] set di attributi che contengono i campi che si desidera aggiornare.

Poiché questa destinazione richiede l’accesso al `[!DNL Email Demographics system attribute-set]`, è necessario consentire `Email` come mostrato di seguito:
![Interfaccia utente del Marketing Cloud Salesforce che mostra l’attributo e-mail impostato con le autorizzazioni consentite.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Per limitare il livello di accesso, puoi anche sovrascrivere singoli accessi utilizzando privilegi granulari.
![Interfaccia utente del Marketing Cloud Salesforce che mostra l’attributo e-mail impostato con autorizzazioni granulari.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Fai riferimento a [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) e [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) pagine per indicazioni dettagliate.

#### Raccogli [!DNL Salesforce Marketing Cloud] credenziali {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL (API) Salesforce Marketing Cloud] destinazione.

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Subdomain | Vedi [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) per scoprire come ottenere questo valore dal [!DNL Salesforce Marketing Cloud] interfaccia. | Se [!DNL Salesforce Marketing Cloud] dominio<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>è necessario fornire `mcq4jrssqdlyc4lph19nnqgzzs84` come valore. |
| ID client | Consulta la sezione [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) per scoprire come ottenere questo valore dal [!DNL Salesforce Marketing Cloud] interfaccia. | r23kxxxxxxxx0z05xxxxxx |
| Segreto client | Consulta la sezione [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) per scoprire come ottenere questo valore dal [!DNL Salesforce Marketing Cloud] interfaccia. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### Guardrail {#guardrails}

* Salesforce impone [limiti tariffari](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Fai riferimento a [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) per risolvere eventuali limiti probabili riscontrati e ridurre gli errori durante l’esecuzione.
   * Fai riferimento a [[!DNL Salesforce Marketing Cloud] Prezzi di coinvolgimento](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina a *Scarica il grafico di confronto Full Edition* come pdf che descrive i limiti imposti dal tuo piano.
   * La [Panoramica API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) dettagli pagina: limiti aggiuntivi.
   * Fai riferimento a [qui](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) per una pagina che raccoglie questi dettagli.
* Il conteggio di *campi personalizzati consentiti per oggetto* varia in base alla tua Salesforce Edition.
   * Fai riferimento a [!DNL Salesforce] [documentazione](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) per ulteriori indicazioni.
   * Se hai raggiunto il limite definito per *campi personalizzati consentiti per oggetto* entro [!DNL Salesforce Marketing Cloud] dovrai
      * Rimuovi gli attributi precedenti prima di aggiungere nuovi attributi in [!DNL Salesforce Marketing Cloud].
      * Aggiorna o rimuovi eventuali segmenti attivati nelle destinazioni Platform che utilizzano questi nomi di attributi precedenti come valore fornito per **[!UICONTROL ID mappatura]** durante il [programmazione dei segmenti](#schedule-segment-export-example) passo.

## Identità supportate {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Chiave di contatto. Fai riferimento a [!DNL Salesforce Marketing Cloud] [documentazione](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) se hai bisogno di ulteriori informazioni. | Obbligatorio |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Ogni stato di segmento in [!DNL Salesforce Marketing Cloud] viene aggiornato con lo stato del segmento corrispondente da Platform, in base alla **[!UICONTROL ID mappatura]** valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL (API) Salesforce Marketing Cloud]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL E-mail marketing]** categoria.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti di seguito e seleziona **[!UICONTROL Connetti alla destinazione]**. Fai riferimento a [Raccogli [!DNL Salesforce Marketing Cloud] credenziali](#gather-credentials) sezione per eventuali indicazioni.

| [!DNL (API) Salesforce Marketing Cloud] destinazione | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Le [!DNL Salesforce Marketing Cloud] prefisso del dominio. <br>Ad esempio, se il dominio è <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> è necessario fornire `mcq4jrssqdlyc4lph19nnqgzzs84` come valore. |
| **[!UICONTROL ID client]** | Il [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Segreto client]** | Il [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione nel Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

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

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL (API) Salesforce Marketing Cloud] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare correttamente i campi XDM su [!DNL (API) Salesforce Marketing Cloud] nei campi di destinazione, segui i passaggi seguenti.

>[!IMPORTANT]
>
>Anche se i nomi degli attributi sono uguali a quelli degli utenti [!DNL Salesforce Marketing Cloud] account, le mappature per entrambi `contactKey` e `personalEmail.address` sono obbligatori. Quando si mappano gli attributi, solo gli attributi dell’Experience Platform `Email Demographics` set di attributi deve essere utilizzato all’interno dei campi target.

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
   ![Esempio di schermata dell’interfaccia utente della piattaforma per Aggiungi nuova mappatura.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM o scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità.
1. In **[!UICONTROL Selezionare il campo di destinazione]** finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità o scegliere **[!UICONTROL Seleziona attributi personalizzati]** e seleziona un attributo dal `Email Demographics` gli attributi visualizzati in base alle esigenze. La [!DNL (API) Salesforce Marketing Cloud] la destinazione utilizza [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) per recuperare dinamicamente gli attributi e i relativi set di attributi definiti in [!DNL Salesforce Marketing Cloud]. Vengono visualizzati nella **[!UICONTROL Campo di destinazione]** quando si imposta la finestra a comparsa [mappatura](#mapping-considerations-example) in [attivare segmenti nel flusso di lavoro](#activate). Nota: solo le mappature per gli attributi definiti all’interno della variabile [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` set di attributi supportati.

   * Ripeti questi passaggi per aggiungere le seguenti mappature tra lo schema del profilo XDM e [!DNL (API) Salesforce Marketing Cloud]: |Campo di origine|Campo di destinazione| Obbligatorio| |—|—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - |
|`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra le mappature di Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

### Pianificare l’esportazione dei segmenti e l’esempio {#schedule-segment-export-example}

Quando si eseguono le [Esportazione di segmenti programmata](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) , devi mappare manualmente i segmenti di Platform su [attributes](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

A questo scopo, seleziona ogni segmento, quindi inserisci il nome dell’attributo da [!DNL Salesforce Marketing Cloud] in [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID mappatura]** campo . Fai riferimento a [Crea attributo in [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) sezione per istruzioni e best practice sulla creazione di attributi in [!DNL Salesforce Marketing Cloud].

Ad esempio, se [!DNL Salesforce Marketing Cloud] attributo `salesforce_mc_segment_1`, specifica questo valore nel [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID mappatura]** per popolare i tipi di pubblico dei segmenti da Experience Platform in questo attributo.

Attributo di esempio da [!DNL Salesforce Marketing Cloud] è mostrato di seguito:
![Schermata dell’interfaccia utente del Marketing Cloud Salesforce che mostra un attributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Un esempio che indica la posizione del [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID mappatura]** è mostrato di seguito:
![Esempio di schermata dell’interfaccia utente della piattaforma che mostra la pianificazione dell’esportazione di segmenti.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Come mostrato nella [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID mappatura]** deve corrispondere esattamente al valore specificato in [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME CAMPO]**.

Ripeti questa sezione per ogni segmento Platform attivato.

A seconda del caso d’uso, tutti i segmenti attivati possono essere mappati sullo stesso [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME CAMPO]** o a diversi **[!UICONTROL NOME CAMPO]** in [!DNL (API) Salesforce Marketing Cloud]. Un esempio tipico basato sull&#39;immagine mostrata sopra potrebbe essere.
| [!DNL (API) Salesforce Marketing Cloud] nome del segmento | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME CAMPO]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID mappatura]** | | — | — | — | | segmento mc di vendita 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | segmento 2 di vendita mc | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

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

* Quando controlli un&#39;esecuzione di un flusso di dati, potresti riscontrare il seguente messaggio di errore: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Schermata dell’interfaccia utente della piattaforma che mostra l’errore.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Per correggere questo errore, verifica che il **[!UICONTROL ID mappatura]** che hai fornito nel flusso di lavoro di attivazione al [!DNL (API) Salesforce Marketing Cloud] la destinazione corrisponde esattamente al nome dell&#39;attributo creato in [!DNL Salesforce Marketing Cloud]. Fai riferimento a [Crea attributo in [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) sezione di orientamento.

* Quando attivi un segmento, potresti ricevere un messaggio di errore: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Per correggere questo errore, contatta il tuo [!DNL Salesforce Marketing Cloud] amministratore dell&#39;account da aggiungere [Experience Platform di indirizzi IP](/help/destinations/catalog/streaming/ip-address-allow-list.md) al tuo [!DNL Salesforce Marketing Cloud] gli intervalli IP affidabili degli account. Fai riferimento a [!DNL Salesforce Marketing Cloud] [Indirizzi IP per l’inclusione negli Inserire nell&#39;elenco Consentiti nel Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) se hai bisogno di ulteriori informazioni.

## Risorse aggiuntive {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentazione](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) spiegando in che modo i contatti vengono aggiornati con le informazioni specificate nei gruppi di attributi specificati.

### Changelog {#changelog}

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti della documentazione effettuati al connettore di destinazione.

+++ Visualizza la finestra delle modifiche

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2023 | Aggiornamento della documentazione | <ul><li>È stata corretta un&#39;istruzione e un collegamento di riferimento nel [Prerequisiti nel Marketing Cloud Salesforce (API)](#prerequisites-destination) sezione per richiamarlo [!DNL Salesforce Marketing Cloud Engagement] è un abbonamento obbligatorio per utilizzare questa destinazione. La sezione precedentemente richiamava erroneamente che gli utenti avevano bisogno di un abbonamento al Marketing Cloud **Account** Impegno a procedere.</li> <li>Abbiamo aggiunto una sezione in [prerequisiti](#prerequisites) per [ruoli e autorizzazioni](#prerequisites-roles-permissions) da assegnare alla [!DNL Salesforce] per il funzionamento di questa destinazione. (PLATIR-26299)</li></ul> |
| Febbraio 2023 | Aggiornamento della documentazione | Abbiamo aggiornato il [Prerequisiti nel Marketing Cloud Salesforce (API)](#prerequisites-destination) sezione per includere un collegamento di riferimento che indica che [!DNL Salesforce Marketing Cloud Engagement] è un abbonamento obbligatorio per utilizzare questa destinazione. |
| Febbraio 2023 | Aggiornamento delle funzionalità | È stato risolto un problema a causa del quale una configurazione errata nella destinazione causava l’invio a Salesforce di un JSON non valido. A causa di ciò, alcuni utenti visualizzavano un numero elevato di identità non riuscite all&#39;attivazione. (PLATIR-26299) |
| Gennaio 2023 | Aggiornamento della documentazione | <ul><li>Abbiamo aggiornato il [Prerequisiti in [!DNL Salesforce]](#prerequisites-destination) per richiamare che gli attributi devono essere creati nella sezione [!DNL Salesforce] lato. Questa sezione include ora istruzioni dettagliate su come eseguire questa operazione e best practice per la denominazione degli attributi in [!DNL Salesforce]. (PLATIR-25602)</li><li>Sono state aggiunte chiare istruzioni sull’utilizzo dell’ID mappatura per ogni segmento attivato nella [programmazione dei segmenti](#schedule-segment-export-example) passo. (PLATIR-25602)</li></ul> |
| Ottobre 2022 | Versione iniziale | Pubblicazione iniziale della destinazione e della documentazione. |

{style="table-layout:auto"}

+++
