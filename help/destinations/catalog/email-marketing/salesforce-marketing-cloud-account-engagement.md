---
title: Coinvolgimento dell'account Marketing Cloud Salesforce
description: Scopri come utilizzare la destinazione Marketing Cloud Account Engagement (precedentemente nota come Pardot) per esportare i dati del tuo account e attivarli all’interno di Salesforce Marketing Cloud Account Engagement per le tue esigenze aziendali.
last-substantial-update: 2023-04-14T00:00:00Z
source-git-commit: 65feb905bfa7d663d1d463d94af428a04dc55b01
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] connection

Utilizza la [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(precedentemente noto come [!DNL Pardot])* destinazione per acquisire, tracciare, valutare e classificare i lead. Puoi anche progettare tracce principali per tutte le fasi della pipeline per segmenti di mercato e gruppi di clienti mirati tramite campagne di e-mail drip e lead management con sviluppo, punteggio e segmentazione delle campagne.

Confrontato con [!DNL Salesforce Marketing Cloud Engagement] più orientato verso **B2C** commercializzazione, [!DNL Marketing Cloud Account Engagement] è ideale per **B2B** casi d&#39;uso che coinvolgono più dipartimenti e responsabili decisionali che richiedono cicli di vendita e decisionali più lunghi. Inoltre, mantieni una maggiore vicinanza e integrazione con il tuo CRM per prendere decisioni di vendita e marketing appropriate. *Nota: Experience Platform dispone anche di connessioni per [!DNL Salesforce Marketing Cloud Engagement], è possibile controllarli nella [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) e [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) pagine.*

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) punto finale, **aggiungere o aggiornare i lead** dopo averli attivati in una nuova [!DNL Marketing Cloud Account Engagement] segmento.

[!DNL Marketing Cloud Account Engagement] utilizza il protocollo OAuth 2 con codice di autorizzazione per l’autenticazione nel [!DNL Account Engagement] API. Istruzioni per l&#39;autenticazione al tuo [!DNL Marketing Cloud Account Engagement] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Marketing Cloud Account Engagement] destinazione, ecco un esempio di caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Inviare e-mail ai contatti per le campagne di marketing {#use-case-send-emails}

Il reparto marketing di una piattaforma online vuole trasmettere una campagna di marketing basata su e-mail a un pubblico curato di lead B2B. Il team marketing della piattaforma può aggiungere nuovi lead o aggiornare le informazioni esistenti sui lead tramite Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti a [!DNL Marketing Cloud Account Engagement], che può quindi essere utilizzato per inviare l’e-mail della campagna di marketing.

## Prerequisiti {#prerequisites}

Consulta le sezioni seguenti per tutti i prerequisiti da configurare in Experience Platform e [!DNL Salesforce] e per informazioni che è necessario raccogliere prima di lavorare con il [!DNL Marketing Cloud Account Engagement] destinazione.

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Marketing Cloud Account Engagement] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

### Prerequisiti in [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Tieni presente i seguenti prerequisiti per esportare i dati da Platform al tuo [!DNL Marketing Cloud Account Engagement] account:

#### Devi avere un [!DNL Marketing Cloud Account Engagement] account {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] un account con sottoscrizione a [Coinvolgimento dell&#39;account Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) il prodotto è obbligatorio per procedere.

Le [!DNL Salesforce] l&#39;account deve avere [!DNL Salesforce] `Account Engagement Administrator role`. Questo è necessario per [creazione di campi di potenziale personalizzato](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Infine, il tuo account dovrebbe anche essere in grado di accedere al [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Rivolgiti a [[!DNL Salesforce] Supporto](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) o [!DNL Salesforce] amministratore dell&#39;account se non disponi di un account o se l&#39;account non è presente nel [!DNL Marketing Cloud Account Engagement] l&#39;abbonamento o [!DNL Account Engagement Administrator role].

#### Raccogli [!DNL Marketing Cloud Account Engagement] credenziali {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL Marketing Cloud Account Engagement] destinazione.

| Credenziali | Descrizione |
| --- | --- |
| `Username` | Le [!DNL Marketing Cloud Account Engagement] nome utente account. |
| `Password` | Le [!DNL Marketing Cloud Account Engagement] password dell&#39;account. |
| `Account Engagement Business Unit ID` | Per trovare l&#39;ID Business Unit di coinvolgimento dell&#39;account, utilizza l&#39;impostazione in [!DNL Salesforce]. Da Imposta, immetti *Configurazione dell&#39;unità aziendale* nella casella Ricerca rapida. L&#39;ID Business Unit di coinvolgimento dell&#39;account inizia con `0Uv` ed è lungo 18 caratteri. Se non è possibile accedere alle informazioni sull&#39;impostazione dell&#39;unità aziendale, chiedere [!DNL Salesforce] Amministratore dell&#39;account per fornirti `Account Engagement Business Unit ID`. Se hai bisogno di ulteriori informazioni, consulta la sezione [[!DNL Salesforce] Autenticazione](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) pagina delle linee guida. |

{style="table-layout:auto"}

### Guardrail {#guardrails}

Fai riferimento a [!DNL Marketing Cloud Account Engagement] [limiti tariffari](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) che specifica i limiti imposti dal tuo piano e si applicherebbe anche alle esecuzioni Experienci Platform.

>[!IMPORTANT]
>
>Se [!DNL Salesforce] l&#39;amministratore dell&#39;account ha limitato l&#39;accesso agli intervalli IP attendibili, è necessario contattarli per ottenere [IP di Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) inserito nell&#39;elenco Consentiti. Fai riferimento a [!DNL Salesforce] [Limitare l&#39;accesso agli intervalli IP attendibili per un&#39;app connessa](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) se hai bisogno di ulteriori informazioni.

## Identità supportate {#supported-identities}

[!DNL Marketing Cloud Account Engagement] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | Indirizzo e-mail previsto | Obbligatorio |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Per ogni segmento selezionato in Platform, il corrispondente [!DNL Salesforce Marketing Cloud Account Engagement] lo stato del segmento viene aggiornato con il relativo stato del segmento da Platform.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL Salesforce Marketing Cloud Account Engagement]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL E-mail marketing]** categoria.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**. Verrà visualizzata la pagina [!DNL Salesforce] pagina di accesso. Inserisci il tuo [!DNL Marketing Cloud Account Engagement] credenziali account e seleziona [!DNL Log In].

![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione per Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Quindi, seleziona [!UICONTROL Consenti] nella finestra successiva per assegnare le autorizzazioni al **Adobe Experience Platform** per accedere al tuo [!DNL Salesforce Marketing Cloud Account Engagement] conto. *Dovrai farlo una sola volta*.

![Finestra a comparsa di conferma dello screenshot dell&#39;app Salesforce per dare le autorizzazioni all&#39;accesso dell&#39;app Experience Platform al coinvolgimento dell&#39;account Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un messaggio: *Connessione all&#39;account di coinvolgimento dell&#39;account di Marketing Cloud Salesforce* messaggio e **[!UICONTROL Connesso]** con un segno di spunta verde, puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio. Fai riferimento a [Raccogli [!DNL Marketing Cloud Account Engagement] credenziali](#gather-credentials) sezione per eventuali indicazioni.

![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Nome con cui riconoscerai questa destinazione in futuro. |
| **[!UICONTROL Descrizione]** | Una descrizione che ti aiuterà a identificare questa destinazione in futuro. |
| **[!UICONTROL ID Business Unit di coinvolgimento dell&#39;account]** | Il [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Marketing Cloud Account Engagement] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare correttamente i campi XDM su [!DNL Marketing Cloud Account Engagement] nei campi di destinazione, segui i passaggi seguenti.

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM o scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità.
1. In **[!UICONTROL Selezionare il campo di destinazione]** finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità o scegliere **[!UICONTROL Seleziona attributi personalizzati]** e specificare dall&#39;elenco di [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) dallo schema disponibile.

   * Ripeti questi passaggi per aggiungere eventuali mappature tra lo schema del profilo XDM e [!DNL Marketing Cloud Account Engagement]: | Campo di origine | Campo di destinazione | Obbligatorio | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Sì | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * Di seguito è riportato un esempio con le mappature precedenti:
      ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra le mappature di Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Passa a uno dei segmenti selezionati. Seleziona la scheda **[!DNL Activation data]**. La **[!UICONTROL ID mappatura]** visualizza il nome del campo personalizzato generato all’interno della colonna [!DNL Marketing Cloud Account Engagement Prospects] pagina.
   ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra l’ID di mappatura per un segmento selezionato.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Accedi a [[!DNL Salesforce]](https://login.salesforce.com/) sito web. Quindi passa alla **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** e controlla se i potenziali clienti del segmento sono stati aggiunti o aggiornati. In alternativa è possibile accedere a [[!DNL Salesforce Pardot]](https://pi.pardot.com/) e l&#39;accesso ai **[!DNL Prospects]** pagina.
   ![Schermata dell’interfaccia utente di Salesforce che mostra la pagina Prospettive .](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Per verificare se i potenziali clienti sono stati aggiornati, seleziona un potenziale e verifica se il campo del potenziale cliente personalizzato è stato aggiornato con lo stato del segmento di Experience Platform.
   ![Schermata dell’interfaccia utente di Salesforce che mostra la pagina Prospect selezionata, il campo del prospect personalizzato viene aggiornato con lo stato del segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentazione API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).