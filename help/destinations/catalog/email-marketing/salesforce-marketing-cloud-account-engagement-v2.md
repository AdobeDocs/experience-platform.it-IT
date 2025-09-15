---
title: (V2) Coinvolgimento Dell'Account Marketing Cloud Di Salesforce
description: Scopri come utilizzare la destinazione (V2) Salesforce Marketing Cloud Account Engagement (precedentemente nota come Pardot) per esportare i dati del profilo e attivarli in Salesforce Marketing Cloud Account Engagement utilizzando l’elaborazione batch per le tue esigenze aziendali.
badge: label="Alpha" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: d1405237698271607fa672ccae1ac731d66df263
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 3%

---

# Connessione [!DNL (V2) Salesforce Marketing Cloud Account Engagement]

La destinazione [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) (precedentemente nota come [!DNL Pardot]) consente di esportare i dati del profilo Adobe Experience Platform nella piattaforma di automazione del marketing B2B di Salesforce.

Questa integrazione consente la sincronizzazione diretta dei dati tra i profili cliente in Adobe Experience Platform e le campagne marketing in [!DNL Salesforce Marketing Cloud Account Engagement].

Questa destinazione utilizza [[!DNL Salesforce Import API v5]](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html) per elaborare in modo efficiente le esportazioni di dati batch.


>[!IMPORTANT]
> 
> Versione V2 della destinazione [Salesforce Marketing Cloud Account Engagement](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md). Questa versione sostituisce la destinazione precedente ed è attualmente in versione Alpha.
> &#x200B;> <br>
> &#x200B;> Se utilizzi la versione precedente della destinazione [Salesforce Marketing Cloud Account Engagement](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md), devi eseguire la migrazione a questa versione V2 prima del **gennaio 2026**. Dopo gennaio 2026, Adobe disattiverà la versione precedente e non sarà più disponibile.


## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione [!DNL (V2) Marketing Cloud Account Engagement], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Gestione lead B2B {#use-case-lead-management}

Sincronizzare i dati dei lead da Adobe Experience Platform a [!DNL Salesforce Marketing Cloud Account Engagement] per lo sviluppo e il punteggio dei lead completi. Il team marketing può creare profili di pubblico avanzati in Experience Platform ed esportarli in [!DNL Salesforce Marketing Cloud Account Engagement] per campagne di marketing B2B automatizzate.

### Automazione delle campagne {#use-case-campaign-automation}

È possibile attivare le campagne di marketing in [!DNL Salesforce Marketing Cloud Account Engagement] utilizzando i tipi di pubblico definiti in Adobe Experience Platform. Dopo aver esportato i tipi di pubblico di destinazione in [!DNL Salesforce], puoi utilizzarli per eseguire campagne e-mail e gestire i lead tramite lo sviluppo, il punteggio e la segmentazione della campagna.

### Arricchimento del profilo {#use-case-profile-enrichment}

Migliora i profili dei potenziali clienti [!DNL Salesforce Marketing Cloud Account Engagement] con dati completi sui clienti provenienti da Adobe Experience Platform. Esporta attributi di profilo completi per creare record di prospect più dettagliati in [!DNL Salesforce Marketing Cloud Account Engagement] per migliorare il targeting e la personalizzazione.

## Prerequisiti {#prerequisites}

Consultare le sezioni seguenti per eventuali prerequisiti da impostare in Experience Platform e [!DNL Salesforce] e per informazioni da raccogliere prima di lavorare con la destinazione [!DNL (V2) Marketing Cloud Account Engagement].

### Prerequisiti di Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL (V2) Marketing Cloud Account Engagement], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](../../../catalog/datasets/overview.md) e [tipi di pubblico](../../../segmentation/types/overview.md) creati in [!DNL Experience Platform].

### [!DNL Salesforce Marketing Cloud Account Engagement] prerequisiti {#prerequisites-destination}

Per esportare i dati da Experience Platform al tuo account [!DNL Marketing Cloud Account Engagement], tieni presente i seguenti prerequisiti:

#### Devi avere un account [!DNL Marketing Cloud Account Engagement] {#prerequisites-account}

Per continuare, è obbligatorio un account [!DNL Marketing Cloud Account Engagement] con una sottoscrizione al prodotto [Marketing Cloud Account Engagement](https://www.salesforce.com/products/marketing-cloud/marketing-automation/).

#### Raccogli [!DNL Marketing Cloud Account Engagement] credenziali {#gather-credentials}

Annotare gli elementi seguenti prima di eseguire l&#39;autenticazione nella destinazione [!DNL (V2) Marketing Cloud Account Engagement].

| Credenziali | Descrizione |
| --- | --- |
| **[!UICONTROL ID Business Unit di coinvolgimento account]** | ID Business Unit del coinvolgimento dell&#39;account [!DNL Salesforce]. Per informazioni su come trovare l&#39;ID, consulta la [documentazione](https://help.salesforce.com/s/articleView?id=000381973&type=1) di Salesforce. |

{style="table-layout:auto"}

## Identità supportate {#supported-identities}

[!DNL (V2) Marketing Cloud Account Engagement] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Se viene trovata una corrispondenza utilizzando uno di questi identificatori, il record del prospect Account Engagement esistente verrà aggiornato con i dati di Adobe Experience Platform. Se non viene trovata alcuna corrispondenza, verrà creato un nuovo record prospect in Coinvolgimento account.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| `matchId` | ID potenziale cliente nel coinvolgimento dell’account | È necessaria almeno una di queste tre identità |
| `matchSalesforceId` | ID contatto/lead Salesforce del potenziale cliente potenziale | È necessaria almeno una di queste tre identità |
| `matchEmail` | Indirizzo e-mail del potenziale cliente | È necessaria almeno una di queste tre identità |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un pubblico, insieme ai campi di schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li>Questa destinazione supporta l’esportazione in batch dei dati del profilo utilizzando l’API di importazione Salesforce v5.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Batch]** | <ul><li>**Esportazione iniziale**: esportazione completa subito dopo la mappatura</li><li>**Esportazioni successive**: esportazioni incrementali ogni 3 ore</li><li>Questa pianificazione è fissa e non può essere personalizzata in Alpha</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.

![Flusso di lavoro della connessione di destinazione di Salesforce Marketing Cloud Account Engagement V2](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/connect-to-destination.png "Flusso di lavoro della connessione di destinazione di Salesforce Marketing Cloud Account Engagement V2")

Verrai reindirizzato alla pagina di accesso [!DNL Salesforce]. Immetti le credenziali del tuo account [!DNL Marketing Cloud Account Engagement] e seleziona **[!UICONTROL Accedi]**.

![Pagina di accesso di Salesforce](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/salesforce-auth.png "Pagina di accesso di Salesforce.")

Quindi, seleziona **[!UICONTROL Consenti]** di concedere le autorizzazioni all&#39;app **Adobe Experience Platform** per accedere al tuo account [!DNL Salesforce Marketing Cloud Account Engagement]. *Questa operazione deve essere eseguita una sola volta*.

![Finestra di conferma dello screenshot dell&#39;app Salesforce per concedere le autorizzazioni all&#39;accesso dell&#39;app Experience Platform al coinvolgimento dell&#39;account Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/allow-app.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato un messaggio: *Connessione all&#39;account di coinvolgimento dell&#39;account di Salesforce Marketing Cloud (V2)* completata e uno stato **[!UICONTROL Connessione]** con segno di spunta verde.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID Business Unit di coinvolgimento dell&#39;account]**: [!DNL Salesforce] `Account Engagement Business Unit ID`.
* **[!UICONTROL API di coinvolgimento account]**: selezionare se si desidera utilizzare gli endpoint di produzione (`https://pi.pardot.com`) o demo (`https://pi.demo.pardot.com`) dell&#39;API di coinvolgimento account.
* **[!UICONTROL ID campagna di coinvolgimento account]**: ogni [!DNL Account Engagement] potenziale cliente deve essere associato a una campagna. Se non imposti un ID campagna, Account Engagement tenterà di assegnarne uno automaticamente, se nel tuo account Salesforce è presente un ID predefinito.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL (V2) Marketing Cloud Account Engagement], è necessario mappare i campi dello schema Experience Data Model (XDM) ai campi corrispondenti nella destinazione.

Per un elenco completo dei campi supportati, consulta la [documentazione di Salesforce Prospect API v5](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html). [i campi personalizzati](https://developer.salesforce.com/docs/marketing/pardot/guide/custom-field-v5.html) non sono supportati nella versione di Alpha.

#### Attributi supportati {#supported-attributes}

La destinazione Salesforce Marketing Cloud Account Engagement supporta gli attributi di destinazione descritti nella tabella seguente.

| Attributo | Tipo | Descrizione |
|---------|----------|----------|
| `salesforceId` | Stringa | ID Salesforce del prospect |
| `salesforceOwnerId` | Intero | ID utente Salesforce del proprietario del prospect |
| `salutation` | Stringa | Saluto del potenziale cliente (ad esempio, Sig., Sig.ra, Dott.) |
| `score` | Intero | Punteggio del potenziale cliente nel coinvolgimento dell’account |
| `source` | Stringa | Origine del record del prospect |
| `state` | Stringa | Stato/provincia del prospect |
| `territory` | Stringa | Il territorio assegnato al prospect |
| `userId` | Intero | ID utente associato al prospect |
| `website` | Stringa | URL del sito web del potenziale cliente |
| `yearsInBusiness` | Stringa | Il numero di anni di attività del prospect |
| `zip` | Stringa | Codice postale del prospect |

#### Mappature richieste {#required-mappings}

Prima di iniziare la mappatura dei dati, controlla le mappature dei campi richieste di seguito.

| Campo di destinazione | Tipo | Obbligatorio | Modalità di utilizzo |
|---|---|---|---|
| `email` | Attributo | Sempre obbligatorio | L’indirizzo e-mail del potenziale cliente. Questo è l&#39;identificatore principale per trovare e abbinare i record prospect in Account Engagement quando non si dispone di `matchId` o `matchSalesforceId`. <br> **Nota:** con la funzione &quot;Consenti più potenziali clienti con lo stesso indirizzo e-mail&quot; di Account Engagement, affidarsi esclusivamente all&#39;e-mail può portare ad ambiguità se ci sono più potenziali clienti con la stessa e-mail. In questi casi, il Coinvolgimento dell’account di solito esegue per impostazione predefinita l’aggiornamento del prospect con l’attività più recente. |
| `matchId` | Identità | È necessaria almeno una di queste tre identità | Un identificatore univoco generato da Account Engagement per ogni singolo record prospect. Utilizzalo quando disponi già dell’ID potenziale di coinvolgimento dell’account e desideri garantire che gli aggiornamenti vengano applicati al potenziale cliente corretto, in particolare quando più potenziali clienti condividono lo stesso indirizzo e-mail. |
| `matchSalesforceId` | Identità | È necessaria almeno una di queste tre identità | ID Salesforce di un lead o contatto in Salesforce. Utilizzalo quando un potenziale cliente è già sincronizzato con Salesforce per mantenere la coerenza dei dati tra Account Engagement e Salesforce. |
| `matchEmail` | Identità | È necessaria almeno una di queste tre identità | L’indirizzo e-mail del potenziale cliente utilizzato per la corrispondenza. Utilizza questo come identificatore alternativo se non disponi dell’ID potenziale di Account Engagement specifico o di Salesforce ID. Nota: se più potenziali clienti condividono lo stesso indirizzo e-mail, per impostazione predefinita il coinvolgimento dell’account aggiorna il potenziale cliente con l’attività più recente. |

Segui i passaggi seguenti per mappare i campi corretti.

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Viene visualizzata una nuova riga di mappatura.
1. Nella finestra **[!UICONTROL Seleziona campo di origine]**, scegli la categoria **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM oppure scegli lo spazio dei nomi **[!UICONTROL Seleziona identità]** e seleziona un&#39;identità.
1. Nella finestra **[!UICONTROL Seleziona campo di destinazione]**, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona un&#39;identità oppure scegli **[!UICONTROL Seleziona attributi personalizzati]** categoria e specifica dall&#39;elenco dei campi prospect standard di Account Engagement.

![Mappatura di campi e identità XDM su campi di Salesforce Marketing Cloud Account Engagement V2](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/mapping.png "Esempio di mappatura di campi e identità XDM su campi di Salesforce Marketing Cloud Account Engagement V2")

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Passa a uno dei tipi di pubblico selezionati. Seleziona la scheda **[!DNL Activation data]**. La colonna **[!UICONTROL ID mapping]** visualizza il nome del campo personalizzato generato nella pagina [!DNL Marketing Cloud Account Engagement Prospects].
   ![Esempio di schermata dell&#39;interfaccia utente di Experience Platform che mostra l&#39;ID di mappatura per un segmento selezionato.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/selected-segment-mapping-id.png)

1. Accedere al sito Web [[!DNL Salesforce]](https://login.salesforce.com/). Quindi passa alla pagina **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** e controlla se i potenziali clienti del pubblico sono stati aggiunti/aggiornati. In alternativa, è possibile accedere a [[!DNL Account Engagement]](https://pi.pardot.com/) e alla pagina **[!DNL Prospects]**.
   ![Schermata dell&#39;interfaccia utente di Salesforce che mostra la pagina Prospect.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospects.png)

1. Per verificare se i potenziali clienti sono stati aggiornati, seleziona un potenziale cliente e verifica se il campo del potenziale cliente personalizzato è stato aggiornato con lo stato del pubblico di Experience Platform.
   ![Schermata dell&#39;interfaccia utente di Salesforce che mostra la pagina del prospect selezionata. Il campo del prospect personalizzato è stato aggiornato con lo stato del pubblico.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospect.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentazione API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)
* [Documentazione di Salesforce Import API v5](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)
* [Documentazione di Salesforce Prospect API v5](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)