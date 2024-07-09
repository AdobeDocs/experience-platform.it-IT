---
title: Tag Mailchimp
description: La destinazione Mailchimp Tags ti consente di esportare i dati del tuo account e attivarli all’interno di Mailchimp per interagire con i contatti.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# [!DNL Mailchimp Tags] connessione

[[!DNL Mailchimp]](https://mailchimp.com) *(noto anche come [!DNL Intuit Mailchimp])* è una piattaforma di automazione del marketing e un servizio di e-mail marketing utilizzato dalle aziende per gestire e comunicare con i contatti *(clienti, clienti o altre parti interessate)* utilizzo di mailing list e campagne di e-mail marketing.

[!DNL Mailchimp Tags] utilizza [audience](https://mailchimp.com/help/getting-started-audience/) e [tag](https://mailchimp.com/help/getting-started-tags/) per gestire le informazioni di contatto. I tag sono etichette che consentono di organizzare i contatti e di etichettarli per la categorizzazione interna in [!DNL Mailchimp].

Confrontato con [!DNL Mailchimp Interest Categories] che utilizzeresti per ordinare i tuoi contatti in base ai loro interessi e preferenze, [!DNL Mailchimp Tags] ha lo scopo di gestire gli abbonamenti ad argomenti di interesse per i tuoi contatti. *Experience Platform dispone anche di una connessione per [!DNL Mailchimp Interest Categories], è possibile visualizzarlo in [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) pagina.*

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) endpoint. È possibile **aggiungi nuovi contatti** o **aggiorna i tag di esistenti [!DNL Mailchimp] contatti** all&#39;interno di un [!DNL Mailchimp] dopo averli attivati all’interno di un nuovo pubblico. [!DNL Mailchimp Tags] utilizza i nomi del pubblico selezionati da Platform come nomi di tag in [!DNL Mailchimp].

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Mailchimp Tags] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Invia e-mail ai contatti per campagne di marketing {#use-case-send-emails}

Il reparto vendite di un’organizzazione desidera trasmettere una campagna di marketing basata su e-mail a un elenco curato di contatti. Gli elenchi di contatti vengono ricevuti in batch da diverse origini offline e devono pertanto essere tracciati. Il team identifica un [!DNL Mailchimp] e inizia a creare i tipi di pubblico Experienci Platform in cui vengono aggiunti i contatti di ogni elenco. Dopo aver inviato questi tipi di pubblico a [!DNL Mailchimp Tags], se non esistono contatti nel [!DNL Mailchimp] pubblico, vengono aggiunti con un tag associato che include il nome del pubblico a cui appartiene il contatto. Se esistono già contatti in [!DNL Mailchimp] audience viene aggiunto un nuovo tag con il nome del pubblico. Poiché le etichette sono visibili in [!DNL Mailchimp] le sorgenti offline sono facilmente identificabili. Dopo l’invio dei dati a [!DNL Mailchimp] inviano l’e-mail della campagna di marketing al pubblico.

## Prerequisiti {#prerequisites}

Consulta le sezioni seguenti per eventuali prerequisiti da impostare in Experience Platform e [!DNL Mailchimp] e per le informazioni da raccogliere prima di lavorare con [!DNL Mailchimp Tags] destinazione.

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Mailchimp Tags] destinazione, è necessario disporre di un [schema](/help/xdm/schema/composition.md), a [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [audience](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) creato in [!DNL Experience Platform].

### Prerequisiti per [!DNL Mailchimp Tags] destinazione {#prerequisites-destination}

Prendi nota dei seguenti prerequisiti per esportare i dati da Platform al tuo [!DNL Mailchimp Tags] account:

#### Devi avere un [!DNL Mailchimp] account {#prerequisites-account}

Prima di creare un [!DNL Mailchimp Tags] destinazione, devi prima assicurarti di disporre di un [!DNL Mailchimp] account. Se non ne hai già una, visita il [[!DNL Mailchimp] pagina di registrazione](https://login.mailchimp.com/signup/) per registrarti e creare il tuo account.

#### Raccogli [!DNL Mailchimp] Chiave API {#gather-credentials}

Hai bisogno del tuo [!DNL Mailchimp] **Chiave API** per autenticare [!DNL Mailchimp Interest Categories] destinazione rispetto al tuo [!DNL Mailchimp] account. Il **Chiave API** funge da **Password** quando [autentica la destinazione](#authenticate).

Se non si dispone di **Chiave API**, accedere al [!DNL Mailchimp] e fare riferimento al [!DNL Mailchimp] documentazione su [come generare la chiave API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Un esempio di chiave API è `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Se si genera **Chiave API**, annotalo in quanto non potrai più accedervi dopo la generazione.

#### Identificare [!DNL Mailchimp] data center {#identify-data-center}

Quindi, devi identificare il tuo [!DNL Mailchimp] data center. Per eseguire questa operazione, accedi al tuo [!DNL Mailchimp] account e passare al **Sezione chiavi API** del tuo account.

L’ID del centro dati è la prima sezione dell’URL visualizzato nel browser. Se l’URL è *https://`us14`.mailchimp.com/account/api/*, il centro dati è `us14`.

L’ID del datacenter viene anche aggiunto alla chiave API nel modulo *key-dc*; Ad esempio, se la chiave API è `0123456789abcdef0123456789abcde-us14`, il centro dati è `us14`.

Annotare il valore del centro dati *(`us14` in questo esempio)*. Questo valore è necessario quando [compila i dettagli della destinazione](#destination-details).

Per ulteriori informazioni, consultare [[!DNL Mailchimp] Documentazione di base](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrail {#guardrails}

Consulta la sezione [!DNL Mailchimp] [limiti di tariffa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) per informazioni dettagliate sui limiti imposti dalla [!DNL Mailchimp] API.

## Identità supportate {#supported-identities}

[!DNL Mailchimp] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | L’indirizzo e-mail del contatto. | Obbligatorio |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un pubblico, insieme ai campi di schema desiderati *ad esempio: indirizzo e-mail, numero di telefono, cognome*, in base alla mappatura del campo.</li><li> Per ogni pubblico selezionato in Platform, la [!DNL Mailchimp Tags] Lo stato del segmento viene aggiornato con lo stato del pubblico da Platform.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Entro **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL Mailchimp Tags]. In alternativa, è possibile posizionarlo sotto il **[!UICONTROL E-mail marketing]** categoria.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti di seguito e seleziona **[!UICONTROL Connetti alla destinazione]**.

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome utente]** | Il tuo [!DNL Mailchimp] nome utente. |
| **[!UICONTROL Password]** | Il tuo [!DNL Mailchimp] **Chiave API**, che hai annotato in [Raccogli [!DNL Mailchimp] credenziali](#gather-credentials) sezione.<br> La chiave API assume la forma di `{KEY}-{DC}`, in cui `{KEY}` porzione si riferisce al valore annotato in basso nel [[!DNL Mailchimp] Chiave API](#gather-credentials) sezione e `{DC}` porzione si riferisce al [[!DNL Mailchimp] data center](#identify-data-center). <br>È possibile specificare `{KEY}` parte o l&#39;intero modulo.<br> Ad esempio, se la chiave API è <br>*`0123456789abcdef0123456789abcde-us14`*,<br> puoi fornire *`0123456789abcdef0123456789abcde`*o *`0123456789abcdef0123456789abcde-us14`*come valore. |

{style="table-layout:auto"}

![Schermata dell’interfaccia utente di Platform che mostra come eseguire l’autenticazione.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Se i dettagli forniti sono validi, nell’interfaccia utente viene visualizzato un **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dell’interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Un nome con cui riconoscerai questa destinazione in futuro. |
| **[!UICONTROL Descrizione]** | Una descrizione che ti aiuterà a identificare questa destinazione in futuro. |
| **[!UICONTROL Data center]** | Il tuo [!DNL Mailchimp] account `data center`. Consulta la sezione [Identificare [!DNL Mailchimp] data center](#identify-data-center) sezione per eventuali indicazioni. |
| **[!UICONTROL Nome pubblico (immetti prima il centro dati)]** | Dopo aver inserito **[!UICONTROL Data center]**, questo menu a discesa viene compilato automaticamente con i nomi del pubblico del tuo [!DNL Mailchimp] account. Seleziona il pubblico da aggiornare con i dati di Platform. |

{style="table-layout:auto"}

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attivare i tipi di pubblico nelle destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform a [!DNL Mailchimp Tags] destinazione, devi passare attraverso il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare correttamente i campi XDM su [!DNL Mailchimp Tags] campi di destinazione, segui i passaggi seguenti:

1. In **[!UICONTROL Mappatura]** passaggio, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Viene visualizzata una nuova riga di mappatura.
1. In **[!UICONTROL Seleziona campo di origine]** finestra, scegli **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona la `Email` spazio dei nomi dell’identità.

   ![Schermata dell’interfaccia utente di Platform con il campo Source e-mail dallo spazio dei nomi delle identità.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. In **[!UICONTROL Seleziona campo di destinazione]** finestra, scegli **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona la `Email` spazio dei nomi dell’identità.

   ![Schermata dell’interfaccia utente di Platform con il campo Target come E-mail dallo spazio dei nomi dell’identità.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Le mappature tra lo schema del profilo XDM e [!DNL Mailchimp Tags] sarà il seguente: | Campo Source | Campo di destinazione | Obbligatorio | | — | — | — | |`IdentityMap: Email`|`Identity: Email`| Sì |

   Di seguito è riportato un esempio con le mappature completate:
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra le mappature dei campi.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Accedi al tuo [[!DNL Mailchimp]](https://login.mailchimp.com/) account. Quindi vai al **[!DNL Audience]** > **[!DNL All Contacts]** e verificare se i contatti del pubblico sono stati aggiunti e quelli del pubblico sono stati aggiornati con il nome del pubblico.
   ![Schermata dell’interfaccia utente Mailchimp che mostra la pagina Pubblico.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Consulta la sezione [[!DNL Mailchimp] pagina errori](https://mailchimp.com/developer/marketing/docs/errors/) per un elenco completo dei codici di stato e di errore, con relative spiegazioni.

## Risorse aggiuntive {#additional-resources}

Ulteriori informazioni utili da [!DNL Mailchimp] la documentazione è riportata di seguito:
* [Guida introduttiva a [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Guida introduttiva a Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Creare un pubblico](https://mailchimp.com/help/create-audience/)
* [Guida introduttiva ai tag](https://mailchimp.com/help/getting-started-tags/)
* [API di marketing](https://mailchimp.com/developer/marketing/api/)
