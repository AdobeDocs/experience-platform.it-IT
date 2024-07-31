---
keywords: crm;CRM;destinazioni crm;Outreach;Outreach crm destination
title: Connessione di uscita
description: La destinazione Outreach ti consente di esportare i dati del tuo account e attivarli in Outreach per le tue esigenze aziendali.
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# Connessione [!DNL Outreach]

## Panoramica {#overview}

[[!DNL Outreach]](https://www.outreach.io/) è una piattaforma di esecuzione delle vendite con i dati di interazione più B2B tra acquirenti e venditori al mondo e investimenti significativi in tecnologie di intelligenza artificiale proprietarie per tradurre i dati di vendita in informazioni. [!DNL Outreach] consente alle organizzazioni di automatizzare il coinvolgimento nelle vendite e di agire sulla base delle informazioni sui ricavi per migliorare l&#39;efficienza, la prevedibilità e la crescita.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta l&#39;API [aggiornamento risorsa di Outreach](https://api.outreach.io/api/v2/docs#update-an-existing-resource), che consente di aggiornare le identità all&#39;interno di un pubblico corrispondente ai potenziali clienti in [!DNL Outreach].

[!DNL Outreach] utilizza OAuth 2 con concessione di autorizzazione come meccanismo di autenticazione per comunicare con [!DNL Outreach] [!DNL Update Resource API]. Le istruzioni per l&#39;autenticazione nell&#39;istanza [!DNL Outreach] sono riportate di seguito, nella sezione [Autentica nella destinazione](#authenticate).

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi fornire esperienze personalizzate ai potenziali clienti, in base agli attributi dei loro profili Adobe Experience Platform. Puoi creare tipi di pubblico dai dati offline e inviarli a [!DNL Outreach] per visualizzarli nei feed dei potenziali clienti non appena i tipi di pubblico e i profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

### Experience Platform prerequisiti {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL Outreach], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creati in [!DNL Experience Platform].

Se hai bisogno di indicazioni sugli stati del pubblico, consulta la documentazione di Adobe per il gruppo di campi dello schema [Dettagli appartenenza a pubblico](/help/xdm/field-groups/profile/segmentation.md).

### Prerequisiti per l’estensione {#prerequisites-destination}

Per esportare i dati da Platform al tuo account [!DNL Outreach], tieni presente i seguenti prerequisiti in [!DNL Outreach]:

#### Devi avere un account Outreach {#prerequisites-account}

Vai alla pagina [!DNL Outreach] [accedi](https://accounts.outreach.io/users/sign_in) per registrarti e creare un account, se non ne hai già uno. Per ulteriori dettagli, vedere anche il supporto [!DNL Outreach] [pagina](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account).

Annotare gli elementi riportati di seguito prima di eseguire l&#39;autenticazione nella destinazione CRM [!DNL Outreach]:

| Credenziali | Descrizione |
|---|---|
| E-mail | Indirizzo e-mail dell&#39;account [!DNL Outreach] |
| Password | Password dell&#39;account [!DNL Outreach] |

#### Impostare le etichette per i campi personalizzati {#prerequisites-custom-fields}

[!DNL Outreach] supporta campi personalizzati per [potenziali](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Per ulteriori informazioni, consultare [Come aggiungere un campo personalizzato in Outreach](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach). Per facilitare l’identificazione, si consiglia di aggiornare manualmente le etichette ai nomi del pubblico corrispondenti, anziché mantenere le impostazioni predefinite. Ad esempio:

Pagina delle impostazioni [!DNL Outreach] per i potenziali clienti che visualizzano campi personalizzati.
![Schermata dell&#39;interfaccia utente di Outreach che mostra i campi personalizzati nella pagina delle impostazioni.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

Pagina delle impostazioni [!DNL Outreach] per i potenziali clienti che visualizzano campi personalizzati con *etichette intuitive* corrispondenti ai nomi del pubblico. Puoi visualizzare lo stato del pubblico nella pagina del prospect in base a queste etichette.
![Schermata dell&#39;interfaccia utente di Outreach che mostra i campi personalizzati con le etichette associate nella pagina delle impostazioni.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> I nomi delle etichette sono solo a scopo di identificazione. Non vengono utilizzati per aggiornare i potenziali clienti.

## Guardrail

L&#39;API [!DNL Outreach] ha un limite di velocità di 10.000 richieste all&#39;ora per utente. Se raggiungi questo limite, riceverai una risposta `429` con il seguente messaggio: `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Se hai ricevuto questo messaggio, devi aggiornare la pianificazione dell’esportazione del pubblico per adeguarla alla soglia della tariffa.

Per ulteriori informazioni, consulta la [[!DNL Outreach] documentazione](https://api.outreach.io/api/v2/docs#rate-limiting).

## Identità supportate {#supported-identities}

[!DNL Outreach] supporta l&#39;aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| `OutreachId` | <ul><li>Identificatore [!DNL Outreach]. Si tratta di un valore numerico corrispondente al profilo del prospect.</li><li>L&#39;ID deve corrispondere all&#39;ID all&#39;interno dell&#39;URL [!DNL Outreach] per il prospect da aggiornare.</li><li>Per ulteriori informazioni, consulta la [[!DNL Outreach] documentazione](https://api.outreach.io/api/v2/docs#update-an-existing-resource).</li></ul> | Obbligatorio |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li> Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Ogni stato del segmento in [!DNL Outreach] viene aggiornato con lo stato del pubblico corrispondente da Platform, in base al valore [!UICONTROL ID mappatura] fornito durante il passaggio [pianificazione del pubblico](#schedule-segment-export-example).</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | <ul><li> Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
> Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestione destinazioni]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

All&#39;interno di **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL Outreach]. In alternativa, è possibile individuarlo nella categoria CRM.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.

![Schermata dell&#39;interfaccia utente di Platform che mostra come eseguire l&#39;autenticazione in Outreach.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Verrà visualizzata la pagina di accesso [!DNL Outreach]. Immetti l’e-mail.

![Schermata dell&#39;interfaccia utente di Outreach che mostra il campo per l&#39;immissione dell&#39;e-mail per l&#39;autenticazione in Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

Immetti la password.

![Schermata dell&#39;interfaccia utente di uscita che mostra il campo per l&#39;immissione della password passaggio per l&#39;autenticazione in Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Nome utente]**: indirizzo e-mail dell&#39;account [!DNL Outreach].
* **[!UICONTROL Password]**: password dell&#39;account [!DNL Outreach].

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **Connesso** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell&#39;interfaccia utente di Platform che mostra come compilare i dettagli per la destinazione di Outreach.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](../../ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL Outreach], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM ai campi di destinazione [!DNL Outreach], effettua le seguenti operazioni:

1. Nel passaggio [!UICONTROL Mapping], fare clic su **[!UICONTROL Aggiungi nuovo mapping]**. Viene visualizzata una nuova riga di mappatura.
   ![Schermata dell&#39;interfaccia utente di Platform che mostra come aggiungere una nuova mappatura](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. Nella finestra [!UICONTROL Seleziona campo di origine], scegli la categoria **[!UICONTROL Seleziona spazio dei nomi identità]** e aggiungi i mapping desiderati.
   ![Schermata dell&#39;interfaccia utente di Platform che mostra la mappatura di Source](../../assets/catalog/crm/outreach/source-mapping.png)

1. Nella finestra [!UICONTROL Seleziona campo di destinazione], seleziona il tipo di campo di destinazione a cui vuoi mappare il campo di origine.
   * **[!UICONTROL Seleziona lo spazio dei nomi delle identità]**: seleziona questa opzione per mappare il campo di origine a uno spazio dei nomi delle identità dall&#39;elenco.
     ![Schermata dell&#39;interfaccia utente di Platform che mostra la mappatura di Target tramite OutreachId.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Aggiungi la seguente mappatura tra lo schema del profilo XDM e l&#39;istanza [!DNL Outreach]:

     | Schema profilo XDM | Istanza [!DNL Outreach] | Obbligatorio |
     |---|---|---|
     | `Oid` | `OutreachId` | Sì |

   * **[!UICONTROL Seleziona attributi personalizzati]**: seleziona questa opzione per mappare il campo di origine a un attributo personalizzato definito nel campo [!UICONTROL Nome attributo]. Per un elenco completo degli attributi supportati, consulta la [[!DNL Outreach] documentazione del prospect](https://api.outreach.io/api/v2/docs#prospect).
     ![Schermata dell&#39;interfaccia utente di Platform che mostra la mappatura di Target tramite LastName.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Ad esempio, a seconda dei valori che desideri aggiornare, aggiungi la seguente mappatura tra lo schema del profilo XDM e l&#39;istanza [!DNL Outreach]:

     | Schema profilo XDM | Istanza [!DNL Outreach] |
     |---|---|
     | `person.name.firstName` | `firstName` |
     | `person.name.lastName` | `lastName` |

   * Di seguito è riportato un esempio che utilizza queste mappature:
     ![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra le mappature di Target.](../../assets/catalog/crm/outreach/mappings.png)

### Esempio di esportazione e pianificazione di un pubblico {#schedule-segment-export-example}

* Durante l&#39;esecuzione del passaggio [Pianifica esportazione pubblico](../../ui/activate-segment-streaming-destinations.md) è necessario mappare manualmente i tipi di pubblico di Platform all&#39;attributo del campo personalizzato in [!DNL Outreach].

* A questo scopo, seleziona ogni segmento, quindi immetti il valore numerico corrispondente che corrisponde al campo *Campo personalizzato `N` Etichetta* di [!DNL Outreach] nel campo **[!UICONTROL ID mappatura]**.

  >[!IMPORTANT]
  >
  > * Il valore numerico *(`N`)* utilizzato all&#39;interno del [!UICONTROL ID mappatura] deve corrispondere alla chiave attributo personalizzata con suffisso al valore numerico all&#39;interno di [!DNL Outreach]. Esempio: *Etichetta `N` Campo Personalizzato*.
  > * È sufficiente specificare il valore numerico, non l’intera etichetta del campo personalizzato.
  > * [!DNL Outreach] supporta un massimo di 150 campi etichetta personalizzati.
  > * Per ulteriori informazioni, consulta la [[!DNL Outreach] documentazione del prospect](https://api.outreach.io/api/v2/docs#prospect).

   * Ad esempio:

     | Campo [!DNL Outreach] | ID mappatura piattaforma |
     |---|---|
     | Etichetta campo personalizzato `4` | `4` |

     ![Schermata dell&#39;interfaccia utente di Platform che mostra un ID di mappatura di esempio durante l&#39;esportazione pianificata del pubblico.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** per passare all&#39;elenco delle destinazioni.
   ![Schermata dell&#39;interfaccia utente di Platform che mostra le destinazioni di navigazione.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Selezionare la destinazione e verificare che lo stato sia **[!UICONTROL abilitato]**.
   ![Schermata dell&#39;interfaccia utente di Platform che mostra le destinazioni di esecuzione del flusso di dati per la destinazione selezionata.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Passa alla scheda **[!DNL Activation data]**, quindi seleziona un nome di pubblico.
   ![Schermata dell&#39;interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Controlla il riepilogo del pubblico e assicurati che il conteggio dei profili corrisponda al conteggio creato all’interno del segmento.
   ![Schermata dell&#39;interfaccia utente di Platform che mostra il riepilogo dei segmenti.](../../assets/catalog/crm/outreach/segment.png)

1. Accedi al sito Web [!DNL Outreach], quindi passa alla pagina [!DNL Apps] > [!DNL Contacts] e controlla se i profili del pubblico sono stati aggiunti. È possibile vedere che ogni stato del pubblico in [!DNL Outreach] è stato aggiornato con lo stato del pubblico corrispondente da Platform, in base al valore [!UICONTROL ID mappatura] fornito durante il passaggio [pianificazione del pubblico](#schedule-segment-export-example).

![Schermata dell&#39;interfaccia utente di Outreach che mostra la pagina Prospect di Outreach con gli stati di pubblico aggiornati.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Durante il controllo di un&#39;esecuzione del flusso di dati, è possibile che venga visualizzato il seguente messaggio di errore: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Schermata dell&#39;interfaccia utente di Platform che mostra l&#39;errore di richiesta non valida.](../../assets/catalog/crm/outreach/error.png)

Per correggere questo errore, verifica che l&#39;[!UICONTROL ID mappatura] fornito in Platform per il pubblico [!DNL Outreach] sia valido ed esista in [!DNL Outreach].

## Risorse aggiuntive {#additional-resources}

La [[!DNL Outreach] documentazione](https://api.outreach.io/api/v2/docs/) contiene dettagli su [Risposte di errore](https://api.outreach.io/api/v2/docs#error-responses) che puoi utilizzare per eseguire il debug di eventuali problemi.
